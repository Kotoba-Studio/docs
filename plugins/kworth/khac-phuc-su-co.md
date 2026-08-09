---
description: Chẩn đoán lỗi khởi động, reload và item stack.
icon: wrench
---

# Khắc phục sự cố

## Khắc phục sự cố

### Plugin không hoạt động

Kiểm tra console khi máy chủ khởi động. Đảm bảo `plugins/` chỉ có một JAR KWorth.

### `/sell` báo plugin disabled

Tìm lỗi xuất hiện khi dòng sau được ghi vào console:

```
[KWorth] Enabling KWorth ...
```

Nếu `plugins/KWorth/startup-error.txt` tồn tại, hãy gửi tệp này để kiểm tra.

### Reload

```
/kworth reload
```

Nếu vừa thay JAR hoặc cập nhật phiên bản, hãy tắt hẳn máy chủ. Sau đó khởi động lại thay vì reload nóng.

### Item không gộp stack

KWorth chỉ thêm lore giá vào bản hiển thị trong GUI. Item trả về inventory phải giữ metadata và lore gốc.

Nếu item không gộp được, hãy cung cấp item type, cách tạo item và log máy chủ.
