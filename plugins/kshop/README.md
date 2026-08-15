---
description: Shop GUI R04 HotFix với giao dịch an toàn, nhiều economy và Price Guard.
icon: shop
---

# KShop

## KShop R04 – HotFix

<a href="https://github.com/Kotoba-Studio/KShop/releases/" class="button primary" data-icon="download">Tải bản phát hành</a>

KShop là shop GUI đa currency cho Paper và Folia tương thích API 1.21.x.

### Điểm nổi bật

* Chọn economy theo từng product: Vault, KShards, PlayerPoints hoặc miễn phí.
* Có mười style shop và bốn style Rank Shop.
* Hỗ trợ Rank Shop, tax và Market Economy tùy chọn.
* Hỗ trợ chọn số lượng, command product và product permission.
* Queue, journal và idempotency bảo vệ giao dịch mỗi người chơi.
* Price Guard kiểm tra giá KWorth và công thức craft.

### Cài đặt nhanh

{% stepper %}
{% step %}
#### Cài plugin

Tắt máy chủ. Sao lưu `plugins/KShop/`, rồi đặt `KShop-R04.jar` vào `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động máy chủ một lần. Chỉ dùng một JAR KShop.
{% endstep %}

{% step %}
#### Chọn cấu hình

Chọn style và ngôn ngữ trong `config.yml`. Chọn economy trên từng item.

Chạy `/kshop status` để xác nhận provider. Restart khi đổi JAR hoặc dependency.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Giữ `price.guard.enabled` và `price.guard.fail-closed` bật trên production.
{% endhint %}

### Tài liệu

* [Cài đặt](cai-dat.md) — cài đặt và nâng cấp an toàn.
* [Cấu hình](cau-hinh.md) — config, product, Rank Shop, style, language, sound và mẫu.
* [Lệnh và quyền hạn](lenh-va-quyen-han.md) — command người chơi và quản trị.
* [Nâng cấp lên R03](nang-cap-kshop-r04.md) — migration và rollback.
* [Java API](java-api.md) — tích hợp KShop vào plugin khác.
* [Vận hành](van-hanh.md) — transaction, Market Economy và khắc phục sự cố.

### Khả năng tương thích

* Paper hoặc Folia tương thích API 1.21.x.
* Economy provider chỉ cần cho product không dùng `eco: free`.
* KShards, Vault, PlayerPoints và LuckPerms là các tích hợp phổ biến.
