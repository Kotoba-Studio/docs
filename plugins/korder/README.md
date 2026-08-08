---
description: Buy Order Marketplace cho máy chủ Minecraft Paper-family.
icon: envelope
---

# KOrder

## KOrder

<a href="./" class="button primary">Tiếng Việt</a> <a href="english/overview.md" class="button secondary">English</a>

KOrder là plugin **Buy Order Marketplace** cho máy chủ Minecraft Paper-family.

Người chơi tạo đơn mua với tiền được giữ trong escrow. Người khác giao đúng vật phẩm để nhận tiền. Người mua nhận hàng qua Stash.

**Phiên bản:** R01\
**Tác giả:** V3rhs\
**Studio:** Kotoba Studio / K-Studio\
**Hỗ trợ:** [Discord](https://discord.gg/x9ScDT7fCV)

{% hint style="info" %}
Tiếng Việt là ngôn ngữ mặc định của tài liệu này. Chọn **English** trong thanh điều hướng để xem bản tiếng Anh.
{% endhint %}

### Điểm nổi bật

* Giao diện Modern mặc định, cùng các style King và Custom.
* Escrow, audit log và transaction SQLite giúp giảm rủi ro nhân bản vật phẩm.
* Hỗ trợ PlaceholderAPI, Discord Webhook và Java API tùy chọn.

### Cài đặt nhanh

{% stepper %}
{% step %}
#### Tắt máy chủ

Không thay nóng JAR khi giao dịch đang hoạt động.
{% endstep %}

{% step %}
#### Cài plugin

Đặt `KOrder-R01.jar` vào thư mục `plugins/`.

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

Phiên bản Java runtime phụ thuộc vào máy chủ đang chạy.
