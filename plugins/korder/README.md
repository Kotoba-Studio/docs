---
description: Buy Order Marketplace cho máy chủ Minecraft Paper-family.
icon: envelope
---

# KOrder

## KOrder

<a href="./" class="button primary">Tiếng Việt</a> <a href="english/overview.md" class="button secondary">English</a> <a href="https://github.com/Kotoba-Studio/KOrder/releases/" class="button primary" data-icon="download">Tải bản phát hành</a>

KOrder là plugin **Buy Order Marketplace** cho máy chủ Minecraft Paper-family.

Người chơi tạo đơn mua với tiền được giữ trong escrow. Người khác giao đúng vật phẩm để nhận tiền. Người mua nhận hàng qua Stash.

**Phiên bản:** R02-v2\
**Tác giả:** V3rhs\
**Studio:** Kotoba Studio / K-Studio\
**Hỗ trợ:** [Discord](https://discord.gg/x9ScDT7fCV)

{% hint style="info" %}
Tiếng Việt là ngôn ngữ mặc định của tài liệu này. Chọn **English** trong thanh điều hướng để xem bản tiếng Anh.
{% endhint %}

### Điểm nổi bật

* Giao diện Modern mặc định, cùng các style King và Custom.
* Escrow, audit log và transaction SQLite giúp giảm rủi ro nhân bản vật phẩm.
* Stash bền vững, recovery thận trọng và ledger cho economy không chắc chắn.
* Hỗ trợ PlaceholderAPI, Discord Webhook và Java API tùy chọn.

### Cài đặt nhanh

{% stepper %}
{% step %}
#### Tắt máy chủ

Không thay nóng JAR khi giao dịch đang hoạt động.
{% endstep %}

{% step %}
#### Cài plugin

Đặt `KOrder-R02-v2.jar` vào thư mục `plugins/`.

Cài một economy provider được hỗ trợ.
{% endstep %}

{% step %}
#### Khởi động và cấu hình

Khởi động máy chủ. Chỉnh `plugins/KOrder/config.yml` nếu cần.

Chạy `/korder reload` sau khi thay đổi cấu hình.
{% endstep %}
{% endstepper %}

### Khả năng tương thích

```
Paper / Leaf: 1.21 → 1.21.11
Paper / Leaf: 26.1 → 26.2
Folia / Canvas: scheduler-aware khi API tương thích
Plugin bytecode: Java 21
```

KOrder không hỗ trợ chính thức Spigot/Bukkit thiếu Paper scheduler API.

KOrder tránh NMS và CraftBukkit. Dialog, Anvil và Bedrock form được chọn theo khả năng runtime.

{% hint style="warning" %}
JAR phát hành gọn chỉ có SQLite native cho Linux x86\_64 glibc.

Windows, macOS, Linux ARM64 hoặc Linux musl cần tự build sau khi điều chỉnh native filters.
{% endhint %}
