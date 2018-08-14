# Common Error - Các lỗi thường gặp

## ERROR: View config not found for name testScene

**Fix:**
change name to TestScene (Upper first letter), Component phải viết hoa chữ ở đầu.

## ERROR: Actions must be plain objects. Use custom middleware for async actions

**FIX:**
Kiểm tra Action Return

```js
export const sendTextToDeviceReset = () => ({ type: ACTION_SEND_TEXT_TO_DEVICE_RESET })
```

## ERROR: Không kết nối với Debugger

**Fix**
Tắt debug, reload, Mở Debug lại