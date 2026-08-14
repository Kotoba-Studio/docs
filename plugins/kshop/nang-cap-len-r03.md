---
icon: arrow-up
---

# Nâng cấp lên R03

## Nâng cấp lên R03

### Trước khi nâng cấp

Sao lưu toàn bộ `plugins/KShop/`. Nếu dùng Git, commit cấu hình trước khi thay JAR.

### Thay JAR

1. Tắt máy chủ.
2. Thay JAR cũ bằng KShop R03.
3. Không chạy hai JAR KShop.
4. Khởi động và đọc console.

KShop có migration nội bộ cho cấu hình cũ. Chờ plugin khởi động xong trước khi sửa file.

### Checklist R02 → R03

* Dùng `name: ''` cho item thường cần tên Minecraft mặc định.
* Kiểm tra lại giao dịch Vault thiếu tiền.
* Giữ `amount` trong phạm vi `1` đến `2304`.
* Giữ `large-buy: true` cho sản phẩm cần chọn số lượng.

Không chép đè toàn bộ file R03 bằng file cũ. So sánh schema rồi chỉ merge phần tùy chỉnh.

Nên giữ category tùy chỉnh, style tùy chỉnh, translations, rank definitions và rank commands.

### Test sau nâng cấp

1. Chạy `/kshop status`.
2. Mở `/shop` và một category.
3. Thử thiếu tiền và đúng bằng giá.
4. Thử large-buy và command product.
5. Thử `/ranks` và market nếu đã bật.

### Rollback

Tắt máy chủ, khôi phục JAR và cấu hình đã sao lưu, rồi khởi động lại. Không xóa backup trước khi bản mới qua kiểm thử production.
