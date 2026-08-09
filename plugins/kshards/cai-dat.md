---
description: Yêu cầu, thiết lập database và cài KShards.
icon: download
---

# Cài đặt

## Cài đặt KShards

### Yêu cầu

* Java 21.
* Minecraft 1.21.x.
* Paper, Folia hoặc Canvas.
* WorldGuard chỉ bắt buộc khi dùng thưởng region.

### Cài đặt

{% stepper %}
{% step %}
#### Cài JAR

Đặt JAR KShards vào thư mục `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động máy chủ để tạo thư mục `plugins/KShards/`.
{% endstep %}

{% step %}
#### Chọn database

Chọn loại database trong `config.yml`. Chạy lệnh sau sau khi chỉnh cấu hình:

```
/shards reload
```
{% endstep %}
{% endstepper %}

SQLite phù hợp máy chủ đơn. MySQL hoặc MariaDB phù hợp mạng nhiều máy chủ.
