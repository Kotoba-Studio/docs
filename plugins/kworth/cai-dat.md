---
description: Yêu cầu, cài đặt JAR và thiết lập KWorth lần đầu.
icon: download
---

# Cài đặt

## Cài đặt

### Yêu cầu

* Java 21 trở lên.
* Minecraft 1.21.1 trở lên.
* Paper, Folia hoặc Canvas.
* Vault nếu dùng economy qua Vault.
* PlaceholderAPI nếu cần placeholder.
* KShards nếu dùng economy `kshards`.

### Cài đặt

{% stepper %}
{% step %}
#### Cài JAR

Đặt `KWorth-R01-v3.jar` vào thư mục `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động máy chủ để tạo các tệp trong `plugins/KWorth/`.
{% endstep %}

{% step %}
#### Cấu hình

Chỉnh các tệp cần thiết. Chạy lệnh sau để nạp lại cấu hình:

```
/kworth reload
```
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Không để nhiều JAR KWorth trong thư mục `plugins/`.
{% endhint %}
