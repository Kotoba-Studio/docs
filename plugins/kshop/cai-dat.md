---
description: Yêu cầu, cài đặt JAR và thiết lập KShop lần đầu.
icon: download
---

# Cài đặt

## Cài đặt KShop

### Yêu cầu

* Java 21.
* Minecraft 1.21.x.
* Paper, Folia hoặc Canvas.
* Ít nhất một economy provider phù hợp.

### Cài đặt

{% stepper %}
{% step %}
#### Cài JAR

Đặt JAR KShop vào thư mục `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động máy chủ để tạo thư mục `plugins/KShop/`.
{% endstep %}

{% step %}
#### Chọn cấu hình

Chọn style và economy trong `config.yml`. Sau đó chạy:

```
/kshop reload
```
{% endstep %}
{% endstepper %}

KShop tự nhận Vault-compatible provider, KEssentials, Essentials, SunLight, CMI, XConomy, PlayerPoints và KShards khi plugin tương ứng đã được cài.
