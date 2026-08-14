---
description: Cài PacketEvents và KShield R01-v3, rồi xác minh server.
icon: download
---

# Cài đặt

## Cài đặt

### Yêu cầu

* Paper, Folia, Canvas hoặc fork tương thích.
* Java theo yêu cầu của phiên bản máy chủ.
* PacketEvents bắt buộc.

### Cài lần đầu

{% stepper %}
{% step %}
#### Tắt máy chủ

Không cài plugin khi máy chủ đang chạy.
{% endstep %}

{% step %}
#### Cài PacketEvents

Đặt JAR PacketEvents vào thư mục `plugins/`.
{% endstep %}

{% step %}
#### Cài KShield

Đặt `KShield-R01-v3.jar` vào thư mục `plugins/`.
{% endstep %}

{% step %}
#### Khởi động và kiểm tra

Khởi động hoàn toàn. PacketEvents phải load trước KShield.

```
/kshield rules
/kshield inspect <player>
/kshield testmod Meteor
```
{% endstep %}
{% endstepper %}

### Reload cấu hình

Sau khi sửa cấu hình, chạy:

```
/kshield reload
```

Không dùng lệnh `/reload` của Bukkit hoặc Paper.

### Runtime libraries

R01-v3 dùng `libraries:` của Paper cho một số dependency runtime. Lần chạy đầu cần truy cập repository để tải và cache thư viện.

### Nâng cấp

1. Backup plugin và database.
2. Tắt máy chủ.
3. Xóa JAR KShield cũ.
4. Đặt `KShield-R01-v3.jar`.
5. Khởi động máy chủ.
6. Kiểm tra `mods.yml`.
7. Chạy `/kshield rules`.
