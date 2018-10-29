# Cài đặt lần đầu

https://facebook.github.io/react-native/docs/getting-started.html

## 1. Cài Chocolatey

https://chocolatey.org/install

Install with cmd.exe

@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

Install with PowerShell.exe

Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

Upgrading Chocolatey

choco upgrade chocolatey

## 2. Cài đặt Node, Python2, JDK

choco install -y nodejs.install python2 jdk8

## 3. Cài The React Native CLI

npm install -g react-native-cli

## 4. Tạo ứng dụng mới

react-native init AwesomeProject

## 5. Chạy ứng dụng

cd AwesomeProject
react-native run-android

nhấp 2 lần R/ lắc thiet bi để Refresh

### Cach 2

react-native start

Tìm IP trên máy tính: 
cmd/ipconfig
xem IPv4 Address

Trên Thiết bị (Android, iPhone):
Trong app/ Menu/ Dev Settings/ Debug server host & port for device/ 
Nhập IPv4:8081

## 6. Debug:

phải chỉnh URL thành locahost mới chạy
http://localhost:8081/debugger-ui/

## Hạ phiên bản 0.56 xuống 0.55.4

react-native init AwesomeProject
cd AwesomeProject
react-native run-android
npm uninstall react-native
npm install --save react-native@0.55.4
react-native run-android
npm install --save babel-core@latest babel-loader@latest
npm uninstall --save babel-preset-react-native
npm install --save babel-preset-react-native@4.0.0
react-native run-android

## Build Android APK File

### Cách 1: 

#### fix lỗi: Unable to load script from assets index.android.bundle on windows

**FIX:**
https://stackoverflow.com/questions/44446523/unable-to-load-script-from-assets-index-android-bundle-on-windows

1. (in project directory) 
> mkdir android/app/src/main/assets
2. 
> react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res
3. 
> react-native run-android
4.
> Qua android studio build

### Cách 2:

https://stackoverflow.com/questions/35283959/build-and-install-unsigned-apk-on-device-without-the-development-server
https://facebook.github.io/react-native/docs/signed-apk-android

1. run: 
> react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res
2. run:
> cd android
> gradlew assembleRelease
3. run: (in project directory)
> cd..
> react-native run-android --variant=release
4. Thư mục release APK: 
> android\app\build\outputs\apk\release