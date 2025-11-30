# Что такое утечки памяти? Как найти?

Утечка памяти — это ситуация, когда приложение удерживает ссылки на объекты, которые больше не нужны, из-за чего сборщик мусора (GC) не может освободить соответствующую память. В результате память растёт со временем, появляются OOM-крэши, деградация производительности и повышенное энергопотребление.

Ниже — сжатое, практическое руководство: что бывает, почему, как обнаружить и как лечить (для Android/Java/Kotlin, с общими замечаниями для нативного кода).

## 1. Типы и причины утечек (коротко)

* **Долгоживущие ссылки на короткоживущие объекты**: статические коллекции, singletons, кеши без лимита.
* **Контекст (Context) утечки**: хранение Activity/View в статике, в длительных объектах → удержание всей Activity.
* **Неправильные слушатели/коллбэки**: не отписались от BroadcastReceiver, Rx, Observer, слушателей View.
* **Анонимные/внутренние классы**: non-static inner class внутри Activity удерживает ссылку на внешнюю Activity.
* **Неправильная работа с ресурсами**: не закрытые Cursors, Streams, FileDescriptors.
* **Bitmap / large native buffers**: большие изображения, native allocations (NDK) — часто вне внимания JVM.
* **Native leaks**: утечки в C/C++ (malloc без free) — память вне Java heap.
* **Неправильный lifecycle**: async-таски (Handler, Runnable, coroutines) удерживают Activity после уничтожения.

## 2. Признаки утечки

* Постоянный рост потребления памяти (heap) при использовании фичи/длительном запуске.
* Частые GC, ухудшение FPS, подвисания, OutOfMemoryError.
* Нарастающие списки объектов одного типа в heap dump.

## 3. Стратегия поиска (практический чек-лист)

1. **Воспроизвести**: воспроизведите сценарий, где память растёт (например, открыть/закрыть экран 50 раз).
2. **Собрать метрики**: использовать Android Profiler → Memory -> record allocation / monitor heap live. Наблюдать рост heap size и native memory.
3. **Вызвать GC вручную** (в профайлере или `adb shell am send-trim-memory` не всегда нужен) и посмотреть, уменьшается ли heap. Если нет — возможен leak.
4. **Сделать heap dump**:
   * через Android Studio Profiler: Capture Heap Dump.
   *   или через adb:

       ```bash
       pid=$(pidof com.example.app)
       adb shell am dumpheap $pid /sdcard/heap.hprof
       adb pull /sdcard/heap.hprof
       ```
   * Конвертировать (если нужно) `hprof-conv heap.hprof converted.hprof`.
5. **Анализ heap dump**:
   * Открыть в Android Studio или в Eclipse MAT (Memory Analyzer Tool).
   * Смотреть _Dominator Tree_ / _Retained Set_ — какие объекты удерживают наибольшую память и кто их удерживает.
   * Ищите большие количества экземпляров одного класса и цепочки удержания (path to GC root).
6. **Использовать LeakCanary**: библиотека, автоматически детектирует утечки экранов/activities/fragments и показывает path to GC root с удобным стек-трейсом. Быстро и эффективно для большинства UI-утечек.
7. **Профилирование native memory**: Android Studio Native Memory Profiler, `malloc_info`, `simpleperf`, AddressSanitizer (для NDK). LeakCanary 2 умеет помогать и с native в некоторых случаях.
8. **Проверить логи/ANR/Crashlytics**: иногда OOM stacktrace указывает на причину и место.

## 4. Инструменты

* Android Studio — Memory Profiler (heap dumps, allocation tracking).
* LeakCanary — автоматическое выявление утечек на стадии разработки.
* Eclipse MAT — глубокий анализ hprof, Dominator Tree.
* adb (dumpheap, bugreport), hprof-conv.
* Native: Android Studio Native Memory Profiler, simpleperf, ASAN (AddressSanitizer), valgrind (на эмуляторе/спец. сборках).
* Firebase Test Lab / CI для регрессионного тестирования памяти.

## 5. Конкретные паттерны исправления

* **Отписывать** слушатели/Receiver/Callbacks в onPause/onDestroy/в соответствующем lifecycle.
* **Не хранить Activity/Context в static-полях**. Если нужен Context — использовать `applicationContext` для долговременных объектов.
* **Сделать внутренние классы static** и использовать `WeakReference` на Activity при необходимости.
* **Очистка коллекций** при закрытии компонента; использовать `WeakHashMap`/`WeakReference` где уместно.
* **Использовать библиотеки загрузки изображений** (Glide/Picasso) — они управляют кешами и ресурсами; явно освобождать большие Bitmap через `recycle()` при ручной работе.
* **Использовать lifecycle-aware компоненты** (LiveData, LifecycleOwner) и корутины с `lifecycleScope`/`viewLifecycleOwner`.
* **Ограничивать кеши** — LRUCache с размером.
* **Мокать/стабить внешние сети** в тестах, чтобы исключить hanging callbacks.

## 6. Быстрые команды и примеры

* Dump heap:

```bash
pid=$(pidof com.example.app)
adb shell am dumpheap $pid /sdcard/heap.hprof
adb pull /sdcard/heap.hprof
hprof-conv heap.hprof converted.hprof
# открыть converted.hprof в MAT или Android Studio
```

* LeakCanary добавление (пример Gradle):

```gradle
debugImplementation "com.squareup.leakcanary:leakcanary-android:2.x"
```

LeakCanary автоматом покажет уведомление о найденной утечке с анализом.

## 7. Советы по процессу тестирования памяти

* Инструментальный тест-кейc: циклически открывать/закрывать экраны, запускать стресс-тесты (Monkey) и собирать heap dumps через CI для регрессии.
* Установить порог роста памяти в CI (например, рост heap > X MB за N итераций — фейлить сборку).
* Фокусироваться сначала на больших утечках (быстро приводящих к OOM), затем на хронических «медленных» утечках.
* Документировать reproducer-steps и минимальный repro-apk для багов памяти.

## 8. Короткий чек-лист при нахождении подозрения на утечку

1. Повторить сценарий и зафиксировать рост memory.
2. Вызвать GC — если память не падает, делать heap dump.
3. Проанализировать Dominator Tree → найти GC root → понять, какая цепочка удерживает объект.
4. Исправить код (отписка, weak refs, static→non-static fix, закрыть ресурсы).
5. Повторно протестировать.

Это концентрированный план: диагностировать через Profiler → получить heap dump → анализ доминаторов → исправить источник удержания. Для UI-утечек LeakCanary даёт самый быстрый путь, а для нативных — Native Memory Profiler / ASAN / simpleperf.
