---
description: Yêu cầu, thiết lập database và cài KShards.
icon: download
---

# Cài đặt

## Cài đặt KShards

### Yêu cầu

* Java phù hợp server Minecraft 1.21.x.
* Paper hoặc Folia tương thích.
* WorldEdit và WorldGuard chỉ cần cho vùng `WORLDGUARD`.

### Cài đặt

{% stepper %}
{% step %}
#### Cài JAR

Đặt `KShards-R03.jar` vào thư mục `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động máy chủ để tạo thư mục `plugins/KShards/`.
{% endstep %}

{% step %}
#### Chọn storage

Chọn `SQLITE`, `MYSQL` hoặc `MARIADB` trong `config.yml`. Xác nhận kết nối:

```
/shards status
```
{% endstep %}
{% endstepper %}

SQLite phù hợp máy chủ đơn. MySQL hoặc MariaDB phù hợp mạng nhiều máy chủ.

### Cấu hình và an toàn

`config.yml` chứa currency, storage, cache, pay, history, event và security. `events.yml` là state runtime. Không sửa `events.yml` hoặc database khi server đang chạy.

`/shards reload` áp dụng config runtime. Đổi storage, executor hoặc cache phải restart. Không đổi `storage.type` để mong plugin tự chuyển dữ liệu.

Giữ console và file audit bật. Với MySQL, dùng user và database riêng. Không công khai password.
