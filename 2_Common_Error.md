# Common Error - Các lỗi thường gặp

## error: View config not found for name testScene
fix:
change name to TestScene (Upper first letter), Component phải viết hoa chữ ở đầu.

## ERROR: Actions must be plain objects. Use custom middleware for async actions.
FIX:
Kiem tra Action Return
export const sendTextToDeviceReset = () => ({ type: ACTION_SEND_TEXT_TO_DEVICE_RESET })

## ERROR: Khong ket noi voi debug duoc
tat debug, reload, mo debug lai