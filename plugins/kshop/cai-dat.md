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

Tắt hoàn toàn máy chủ. Đặt `KShop-R02-v6.jar` vào `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động máy chủ để tạo thư mục `plugins/KShop/`.
{% endstep %}

{% step %}
#### Kiểm tra

Chạy lệnh sau, rồi mở `/shop` để kiểm tra GUI:

```
/kshop status
```
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Không xóa `plugins/KShop/` khi nâng cấp. Hãy backup thư mục này trước khi thay JAR.
{% endhint %}

KShop tự nhận Vault-compatible provider, KEssentials, Essentials, SunLight, CMI, XConomy, TheNewEconomy, CoinsEngine, PlayerPoints và KShards.
