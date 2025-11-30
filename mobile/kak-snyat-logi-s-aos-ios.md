# Как снять логи с AOS/IOS?

Для Android и iOS логирование и снятие логов отличается из-за архитектуры ОС и инструментов, но принцип один — нужно получать события системы, приложения и сетевые/креш-логи.

***

### **Android (AOS)**

#### 1. **Использование `adb logcat`**

* Подключаем устройство или эмулятор к компьютеру.
* Команда для просмотра логов:

```bash
adb logcat
```

* Чтобы фильтровать только ваше приложение:

```bash
adb logcat | grep com.example.app
```

* Для сохранения в файл:

```bash
adb logcat -v time > logs.txt
```

#### 2. **Фильтры по тегам и уровням**

* Уровни: `V`(Verbose), `D`(Debug), `I`(Info), `W`(Warn), `E`(Error), `F`(Fatal)
* Пример:

```bash
adb logcat MyAppTag:D *:S
```

* Это покажет только сообщения с тегом `MyAppTag` на уровне Debug и выше, остальные скрыты.

#### 3. **Системные логи**

* Для ошибок системы (`ANR`, `Crash`):

```bash
adb bugreport bugreport.zip
```

* В архиве будут логи, stacktrace и системные события.

#### 4. **Логи сетевого трафика**

* Использовать **mitmproxy**, **Charles Proxy**, **tcpdump** для сниффинга HTTPS/HTTP.
* `adb shell tcpdump` можно для сниффинга на устройстве с root.

***

### **iOS**

#### 1. **Через Xcode**

* Подключить устройство к Mac, открыть **Xcode → Window → Devices and Simulators → Device Logs**.
* Здесь можно просматривать **crash logs, системные события, консоль приложения**.
* Для сохранения лога: **Export** или copy/paste.

#### 2. **Через Console.app (macOS)**

* Запустить Console → выбрать устройство → смотреть live-логи приложения.
* Фильтровать по `process` или `bundle ID`.

#### 3. **Через idevice\_syslog (libimobiledevice)**

* На Mac/Linux:

```bash
idevice_syslog
```

* Фильтрация по приложению:

```bash
idevice_syslog | grep com.example.app
```

#### 4. **Crash Logs**

* На устройстве: **Settings → Privacy → Analytics & Improvements → Analytics Data**
* Или через Xcode / Organizer → Devices → View Device Logs.

#### 5. **Сетевой трафик**

* Использовать **Charles Proxy, mitmproxy** или встроенные инструменты Xcode для Network Link Conditioner.

***

#### **Рекомендации для QA**

1. Для регрессионного тестирования и CI: сохранять логи в отдельный файл при каждом запуске тестов.
2. При крэше — всегда прикладывать **stacktrace + логи до крэша**.
3. Для мобильных багрепортов: использовать **лог + скриншоты/видео**.
4. Фильтруйте логи по тегам или bundle ID, чтобы уменьшить шум.
