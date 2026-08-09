---
description: Hệ thống tiền tệ Shards bất đồng bộ cho máy chủ Minecraft.
icon: gem
---

# KShards

## KShards

<a href="https://github.com/Kotoba-Studio/KShards/releases/" class="button primary" data-icon="download">Tải bản phát hành</a>

KShards là hệ thống tiền tệ Shards bất đồng bộ cho Paper, Folia và Canvas.

### Điểm nổi bật

* SQLite, MySQL và MariaDB.
* Chuyển Shards, lịch sử, bảng xếp hạng và khóa tài khoản.
* Hỗ trợ PlaceholderAPI và API cho plugin khác.
* Tích hợp trực tiếp với KShop.
* Thưởng Shards theo WorldGuard region do quản trị viên khai báo.

{% hint style="info" %}
KShards không tự tìm hoặc tạo WorldGuard region.
{% endhint %}

### Cài đặt nhanh

{% stepper %}
{% step %}
#### Cài plugin

Đặt JAR KShards vào thư mục `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động máy chủ để tạo thư mục `plugins/KShards/`.
{% endstep %}

{% step %}
#### Chọn database

Chọn loại database trong `config.yml`. Chạy `/shards reload` sau khi thay đổi.
{% endstep %}
{% endstepper %}

### Khả năng tương thích

* Java 21.
* Minecraft 1.21.x.
* Paper, Folia hoặc Canvas.
* WorldGuard chỉ cần thiết cho thưởng theo region.
