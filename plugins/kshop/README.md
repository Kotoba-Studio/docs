---
description: Shop GUI R02-v6 cho Paper, Folia và Canvas.
icon: shop
---

# KShop

## KShop R02-v6

<a href="https://github.com/Kotoba-Studio/KShop/releases/" class="button primary" data-icon="download">Tải bản phát hành</a>

KShop là shop GUI cho Paper, Folia và Canvas 1.21.x.

### Điểm nổi bật

* Chọn economy theo từng item, gồm Vault, KShards và PlayerPoints.
* Có mười style shop và bốn style Rank Shop.
* Hỗ trợ Rank Shop, tax và Market Economy tùy chọn.
* Dùng queue và journal để giảm click nhanh, dupe và giao dịch trùng.
* Dùng UI click thống nhất và chỉ phát kết quả cuối của transaction.

### Cài đặt nhanh

{% stepper %}
{% step %}
#### Cài plugin

Đặt JAR KShop vào thư mục `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động máy chủ để tạo thư mục `plugins/KShop/`.
{% endstep %}

{% step %}
#### Chọn cấu hình

Chọn style và language trong `config.yml`. Chọn economy trên từng item.

Chạy `/kshop reload` sau khi thay đổi.
{% endstep %}
{% endstepper %}

### Tài liệu

* [Cài đặt](cai-dat.md) — cài R02-v6 và nâng cấp an toàn.
* [Cấu hình](cau-hinh.md) — config, item, Rank Shop, language và sound.
* [Lệnh và quyền hạn](lenh-va-quyen-han.md) — command người chơi và quản trị.
* [Java API](java-api.md) — tích hợp KShop vào plugin khác.
* [Vận hành](van-hanh.md) — transaction và xử lý lỗi.

### Khả năng tương thích

* Java 21.
* Minecraft 1.21.x.
* Paper, Folia hoặc Canvas.
* Economy provider chỉ cần thiết khi item không dùng `free`.
