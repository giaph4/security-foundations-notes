# Detection: <tên rule>

- **ID/Tệp:** `rules/…yml` · **Tác giả:** … · **Ngày:** … · **Mức:** low/medium/high/critical
- **MITRE ATT&CK:** TA____ / T____.___
- **Log source:** (Sysmon EID …, Windows Security …, auditd, …)

## Giả thuyết phát hiện
…

## Rule (Sigma)
```yaml
title:
id:
status: experimental
description:
logsource:
  product:
  category:
detection:
  selection:
    # ...
  condition: selection
falsepositives:
  - …
level: medium
tags:
  - attack.t____
```

## Test (Atomic Red Team / thủ công)
| Test | Lệnh | Kết quả: Detect / Miss | Bằng chứng |
| --- | --- | --- | --- |

## False positive & tuning
…

## Triage khi alert nổ
1. …
