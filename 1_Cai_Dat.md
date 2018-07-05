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

nhấp 2 lần R/ lắc để Refresh

## 6. Debug:

phải chỉnh URL thành locahost mới chạy
http://localhost:8081/debugger-ui/