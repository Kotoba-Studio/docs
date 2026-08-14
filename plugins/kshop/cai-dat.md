---
description: Yêu cầu, cài đặt JAR và thiết lập KShop lần đầu.
icon: download
---

# Cài đặt

## Cài đặt KShop

### Yêu cầu

* Máy chủ tương thích API Bukkit 1.21.
* Paper, Folia hoặc Canvas.
* Economy provider chỉ cần cho sản phẩm trả phí.

### Cài đặt

{% stepper %}
{% step %}
#### Sao lưu và cài JAR

Tắt hoàn toàn máy chủ. Sao lưu toàn bộ `plugins/KShop/`.

Đặt JAR KShop R03 vào `plugins/`. Xóa hoặc đổi tên JAR KShop cũ.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động máy chủ để tạo thư mục `plugins/KShop/`.
{% endstep %}

{% step %}
#### Kiểm tra

Chạy lệnh sau, rồi mở `/shop` để kiểm tra GUI:

```
/kshop status
```
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Không chạy hai JAR KShop cùng lúc. Không dùng `/reload` thay cho restart khi thay JAR.
{% endhint %}

### Thiết lập economy

Dùng `eco: vault` cho economy tương thích Vault. Dùng `eco: shards` cho KShards.

Dùng `eco: points` cho PlayerPoints. Sản phẩm miễn phí phải dùng `eco: free`.

### Kiểm tra đầu tiên

Chạy `/kshop status`. Kiểm tra style, số sản phẩm, money provider và transaction queue.

Sau đó mở `/shop`. Thử mua với số dư bằng `0`, thiếu tiền và đúng bằng giá.
