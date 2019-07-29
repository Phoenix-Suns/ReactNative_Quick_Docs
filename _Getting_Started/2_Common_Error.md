# Common Error - Các lỗi thường gặp

## View config not found for name testScene

**Fix:**
change name to TestScene (Upper first letter), Component phải viết hoa chữ ở đầu.

## Actions must be plain objects. Use custom middleware for async actions

**FIX:**
Kiểm tra Action Return

```js
export const sendTextToDeviceReset = () => ({ type: ACTION_SEND_TEXT_TO_DEVICE_RESET })
```

## Không kết nối với Debugger

**Fix**
Tắt debug, tắt app, reload, Mở Debug lại

## Unable to load script from assets index.android.bundle on windows

**FIX:**
https://stackoverflow.com/questions/44446523/unable-to-load-script-from-assets-index-android-bundle-on-windows

1. (in project directory) mkdir android/app/src/main/assets
2. react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res
3. react-native run-android

## Could not connect to development server on android emulator and on real device

**FIX:**

1. Cách 1:

react-native start

Tìm IP trên máy tính: 
cmd/ipconfig
xem IPv4 Address

Trên Thiết bị (Android, iPhone):
Trong app/ Menu/ Dev Settings/ Debug server host & port for device/ 
Nhập IPv4:8081

2. Cách 2
cd c:/.../Android/sdk/platform-tools
adb reverse tcp:8081 tcp:8081

## bundling failed: Error: Unable to resolve module `AccessibilityInfo`

Hạ phiên bản:

npm uninstall react-native
npm install --save react-native@0.55.4
react-native run-android
npm install --save babel-core@latest babel-loader@latest
npm uninstall --save babel-preset-react-native
npm install --save babel-preset-react-native@4.0.0
react-native run-android

## Unable to resolve "@babel/runtime/helpers/builtin/interopRequireDefault"

npm add @babel/runtime

## Khi chạy lệnh: react-native run-android --variant=release 

**ERROR:** com.android.builder.testing.api.DeviceException: com.android.ddmlib.InstallException: INSTALL_FAILED_UPDATE_INCOMPATIBLE: Package com.pa_app_react_native signatures do not match the previously installed version; ignoring!

**FIX:** Xóa app cũ trong máy android

## Màn hình trắng:

**ERROR:** Màn hình trắng khí debug, build, refresh
**FIX:** Tắt app trong android, mở lại
