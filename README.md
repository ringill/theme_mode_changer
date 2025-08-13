# Настройка окружения

### JDK
Temurin 21.0.8+9-LTS - 07/22/2025

https://adoptium.net/temurin/releases?version=21&os=any&arch=any
```sh
java --version

openjdk 21.0.8 2025-07-15 LTS
OpenJDK Runtime Environment Temurin-21.0.8+9 (build 21.0.8+9-LTS)
OpenJDK 64-Bit Server VM Temurin-21.0.8+9 (build 21.0.8+9-LTS, mixed mode, sharing)
```

### Gradle
https://gradle.org/next-steps/?version=8.14.3&format=bin
```sh
gradle --version

------------------------------------------------------------
Gradle 8.14.3
------------------------------------------------------------

Build time:    2025-07-04 13:15:44 UTC
Revision:      e5ee1df3d88b8ca3a8074787a94f373e3090e1db

Kotlin:        2.0.21
Groovy:        3.0.24
Ant:           Apache Ant(TM) version 1.10.15 compiled on August 25 2024
Launcher JVM:  21.0.8 (Eclipse Adoptium 21.0.8+9-LTS)
Daemon JVM:    C:\Program Files\Eclipse Adoptium\jdk-21.0.8.9-hotspot (no JDK specified, using current Java home)
OS:            Windows 10 10.0 amd64
```

### Kotlin
https://github.com/JetBrains/kotlin/releases/tag/v1.9.25
```sh
kotlinc-native -version

info: kotlinc-native 1.9.25 (JRE 21.0.8+9-LTS)
Kotlin/Native: 1.9.25
```

### Android SDK

#### Скачать
commandlinetools-win-13114758_latest.zip
https://developer.android.com/studio

#### Правильно распаковать
https://developer.android.com/tools/sdkmanager

#### Установить компоненты
```sh
# Перейдите в папку cmdline-tools
cd C:/Users/User/AppData/Local/Android/Sdk/cmdline-tools/latest/bin

# Установите платформу Android 34
.\sdkmanager.bat "platforms;android-34"

# Установите Build Tools для Android 34 (последняя версия)
.\sdkmanager.bat "build-tools;34.0.0"

# Установите Android SDK Platform-Tools
.\sdkmanager.bat "platform-tools"

# Установите Android Emulator (если нужно)
.\sdkmanager.bat "emulator"

# Установите Android Support Repository
.\sdkmanager.bat "extras;android;m2repository"
```

# Сборка
```sh
gradle clean --refresh-dependencies
```
```sh
gradle assembleRelease
```
Результат ищем в папке ```./app/build/outputs/apk/release```

# Запуск

### Создание эмулятора

#### Установите необходимый образ системы
```sh
cd C:/Users/User/AppData/Local/Android/Sdk/cmdline-tools/latest/bin
.\sdkmanager.bat "system-images;android-34;google_apis;x86_64"
```
#### Создайте AVD с помощью avdmanager
```sh
.\avdmanager.bat create avd -n Pixel_6_API_34 -k "system-images;android-34;google_apis;x86_64" -d pixel
```
Где:
```
-n Pixel_6_API_34 - имя вашего AVD
-k - идентификатор пакета системы
-d pixel - ID устройства (Pixel)
```
#### Проверьте список AVD
```sh
.\avdmanager.bat list avd
.\emulator -list-avds
```

#### Запустите эмулятор
```sh
cd C:\Users\User\AppData\Local\Android\Sdk\emulator
.\emulator -avd Pixel_6_API_34
```

### Установка APK

```sh
cd C:\Users\User\AppData\Local\Android\Sdk\platform-tools
.\adb install "C:\Users\User\repo\theme_mode_changer\app\build\outputs\apk\release\app-release.apk"
```