---
description: Hệ thống tiền Shards R03 với SQL, audit và giao dịch idempotent.
icon: gem
---

# KShards

## KShards R03

<a href="https://github.com/Kotoba-Studio/KShards/releases/" class="button primary" data-icon="download">Tải bản phát hành</a>

KShards là hệ thống tiền Shards độc lập cho Paper và Folia tương thích 1.21.x.

### Điểm nổi bật

* SQLite, MySQL và MariaDB.
* Balance, pay, history, top, freeze và audit.
* Giao dịch idempotent cùng bảo vệ thao tác admin lặp.
* Event multiplier lưu epoch chính xác qua restart.
* Thưởng AFK theo vùng CUBOID hoặc WorldGuard.
* Tích hợp KShop và PlaceholderAPI.

{% hint style="info" %}
WorldGuard chỉ cần khi vùng thưởng dùng mode `WORLDGUARD`.
{% endhint %}

### Cài đặt nhanh

{% stepper %}
{% step %}
#### Cài plugin

Đặt `KShards-R03.jar` vào thư mục `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động một lần để tạo `plugins/KShards/`.
{% endstep %}

{% step %}
#### Chọn database

Chọn storage trong `config.yml`. Chạy `/shards status` để xác nhận kết nối.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Không đổi `storage.type` bằng reload. Backup rồi restart đầy đủ khi đổi storage.
{% endhint %}

### Khả năng tương thích

* Java phù hợp phiên bản server Minecraft 1.21.x.
* Paper hoặc Folia tương thích.
* PlaceholderAPI dùng cho placeholder.
* WorldEdit và WorldGuard dùng cho vùng `WORLDGUARD`.

### Placeholder và bảo mật

Placeholder chung: `%kshards_symbol%`, `%kshards_name%`, `%kshards_prefix%` và `%kshards_service_status%`.

Placeholder player: `%kshards_balance%`, `%kshards_balance_raw%`, `%kshards_balance_formatted%`, `%kshards_balance_compact%`, `%kshards_lifetime_earned%`, `%kshards_lifetime_spent%`, `%kshards_frozen%` và `%kshards_rank%`.

Top động dùng `%kshards_top_<n>_name%`, `_uuid%`, `_balance%`, `_balance_raw%`, `_balance_formatted%` hoặc `_balance_compact%`.

Giữ `command-cooldown-millis`, `duplicate-window-millis`, giới hạn high-value và audit bật. KShards dùng transaction idempotent; lỗi ghi event sẽ rollback state RAM.
