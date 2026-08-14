---
description: Lệnh quản trị KShield, permission nodes và alias.
icon: terminal
---

# Lệnh và quyền hạn

## Lệnh và quyền hạn

| Lệnh                                   | Quyền hạn                |
| -------------------------------------- | ------------------------ |
| `/kshield`                             | `KShield.Gui.Info`       |
| `/kshield reload`                      | `KShield.reload`         |
| `/kshield inspect <player>`            | `KShield.inspect`        |
| `/kshield rules`                       | `KShield.rules`          |
| `/kshield testmod <mod>`               | `KShield.testmod`        |
| `/kshield alerts [local]`              | `KShield.alerts`         |
| `/kshield profile <player>`            | `KShield.Gui.Profile`    |
| `/kshield monitor <player>`            | `KShield.Gui.Monitor`    |
| `/kshield history <player\|uuid>`      | `KShield.Gui.History`    |
| `/kshield clearhistory <player\|uuid>` | `KShield.ClearHistory`   |
| `/kshield focus [player]`              | `KShield.focus`          |
| `/kshield unfocus`                     | `KShield.focus`          |
| `/kshield follow [player]`             | `KShield.follow`         |
| `/kshield unfollow`                    | `KShield.follow`         |
| `/kshield check <player> [50-5000]`    | `KShield.check`          |
| `/kshield teleport <player>`           | `KShield.teleport`       |
| `/kshield top`                         | `KShield.Gui.Top`        |
| `/kshield stats`                       | `KShield.Gui.Statistics` |
| `/kshield shutdown [confirm]`          | `KShield.shutdown`       |

### Alias

* `/ks`
* `/tg`

### Bypass

`KShield.Bypass` loại người chơi khỏi tracking và check. Không cấp quyền này cho nhóm mặc định.

### Lưu ý

`/kshield reload` validate cấu hình trước khi thay thế snapshot đang chạy.

`/kshield testmod` chỉ kiểm tra registry. Lệnh không scan hoặc punish người chơi.
