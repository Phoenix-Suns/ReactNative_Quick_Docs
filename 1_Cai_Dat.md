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

tren may tinh: 
cmd/ipconfig
xem IPv4 Address

tren thiet bi:
Menu/ Dev Settings/ Debug server host & port for device/ 
Nhap IPv4:8081

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