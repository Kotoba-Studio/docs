---
description: Phạm vi tích hợp Java được công bố cho KShop R03.
icon: brackets-curly
---

# Java API

## Tích hợp Java

KShop R03 documentation package không công bố Java API ổn định.

Không dùng package, class hoặc dependency từ tài liệu R02 như một API contract cho R03.

### Tích hợp an toàn

Khai báo KShop là dependency khi plugin của bạn cần plugin này hoạt động trước.

Tích hợp qua command hoặc cấu hình khi phù hợp. Kiểm tra release notes trước khi gọi API nội bộ.

{% hint style="warning" %}
Không bind vào config, transaction, market hoặc economy nội bộ. Các thành phần này không phải stable API.
{% endhint %}
