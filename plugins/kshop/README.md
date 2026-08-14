---
description: Shop GUI R03 cho Paper, Folia và Canvas.
icon: shop
---

# KShop

## KShop R03

<a href="https://github.com/Kotoba-Studio/KShop/releases/" class="button primary" data-icon="download">Tải bản phát hành</a>

KShop là shop GUI cho máy chủ Paper, Folia và Canvas trên API 1.21.

### Điểm nổi bật

* Chọn currency theo từng sản phẩm: Vault, KShards, PlayerPoints hoặc miễn phí.
* Có mười style shop và bốn style Rank Shop.
* Hỗ trợ Rank Shop, tax và Market Economy tùy chọn.
* Hỗ trợ chọn số lượng, command product và product permission.
* Dùng queue theo người chơi để hạn chế click spam và giao dịch trùng.

### Cài đặt nhanh

{% stepper %}
{% step %}
#### Cài plugin

Tắt máy chủ. Sao lưu `plugins/KShop/`, rồi đặt JAR KShop R03 vào `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động máy chủ. Chỉ dùng một JAR KShop.
{% endstep %}

{% step %}
#### Chọn cấu hình

Chọn style và language trong `config.yml`. Chọn economy trên từng item.

Chạy `/kshop reload` sau khi thay đổi.
{% endstep %}
{% endstepper %}

### Tài liệu

* [Cài đặt](cai-dat.md) — cài R03 và nâng cấp an toàn.
* [Cấu hình](cau-hinh.md) — config, product, Rank Shop, style, language, sound và mẫu.
* [Lệnh và quyền hạn](lenh-va-quyen-han.md) — command người chơi và quản trị.
* [Nâng cấp lên R03](nang-cap-len-r03.md) — migration và rollback.
* [Java API](java-api.md) — tích hợp KShop vào plugin khác.
* [Vận hành](van-hanh.md) — transaction, Market Economy và khắc phục sự cố.

### Khả năng tương thích

* API Bukkit 1.21.
* Paper, Folia hoặc Canvas tương thích.
* Economy provider chỉ cần thiết cho sản phẩm không dùng `eco: free`.
