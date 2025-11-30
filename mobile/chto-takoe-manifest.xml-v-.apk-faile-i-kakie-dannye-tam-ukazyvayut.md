# Что такое Manifest.xml в .apk файле и какие данные там указывают?

**`AndroidManifest.xml`** — это основной конфигурационный файл Android-приложения. Он описывает структуру приложения, его компоненты и права доступа, необходимые системе для корректного запуска и взаимодействия.

Файл обязательно присутствует в каждом `.apk` и считывается системой **до установки и запуска приложения**.

***

### **Основные задачи `AndroidManifest.xml`**

1. Определяет **идентичность и структуру** приложения.
2. Сообщает системе, **какие компоненты** входят в приложение (activity, service и т.д.).
3. Указывает **разрешения**, необходимые приложению.
4. Определяет **минимальные требования** (версию Android, используемые библиотеки).
5. Задает **точку входа** — activity, которая открывается при запуске.

***

### **Структура и ключевые теги**

#### **1. `<manifest>`**

Корневой элемент, содержит базовую информацию:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.myapp"
    android:versionCode="3"
    android:versionName="1.2.1">
```

* `package` — уникальный идентификатор приложения.
* `versionCode` — технический номер версии (для обновлений).
* `versionName` — отображаемая версия.

***

#### **2. `<uses-sdk>`**

Минимальная и целевая версия Android:

```xml
<uses-sdk
    android:minSdkVersion="21"
    android:targetSdkVersion="34" />
```

***

#### **3. `<uses-permission>`**

Права, запрашиваемые приложением:

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

***

#### **4. `<application>`**

Описывает само приложение и его компоненты:

```xml
<application
    android:label="@string/app_name"
    android:icon="@mipmap/ic_launcher"
    android:theme="@style/AppTheme">
```

***

#### **5. `<activity>`**

Каждый экран (Activity) описывается отдельно:

```xml
<activity android:name=".MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

* Здесь определяется **точка входа** (`MAIN` + `LAUNCHER`).

***

#### **6. `<service>`, `<receiver>`, `<provider>`**

Определяют фоновые компоненты:

```xml
<service android:name=".SyncService" />
<receiver android:name=".AlarmReceiver" />
<provider android:name=".DatabaseProvider" />
```

***

#### **7. `<meta-data>`**

Дополнительные данные (например, ключи API):

```xml
<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="@string/google_maps_key" />
```

***

### **Что важно тестировщику**

* Проверить наличие нужных **разрешений** (например, `INTERNET`, `CAMERA`).
* Проверить **main activity** — правильно ли настроен запуск приложения.
* Убедиться, что нет **лишних экспортируемых компонентов** (`android:exported="true"`), создающих риски безопасности.
* Сверить **minSdkVersion/targetSdkVersion** с заявленной поддержкой устройства.

***

Итог:\
`AndroidManifest.xml` — это **“паспорт” Android-приложения**, в котором описываются компоненты, разрешения, версии, зависимости и параметры запуска, обеспечивая корректную интеграцию приложения с системой.
