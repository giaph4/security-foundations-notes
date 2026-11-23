# Giáo trình Giai đoạn 3: Phòng thủ — Blue Team (bản chi tiết)

Nov 23, 2026 · @Huynh Gia Pho

Phát hiện sớm, khoanh vùng nhanh, khôi phục có kiểm soát — đó là năng lực phản ứng linh hoạt. Giáo trình này dẫn bạn qua 5 module trong 18 tuần, mỗi chương gồm lý thuyết, video, tài liệu đọc, lab và tiêu chí đạt.

## Cách dùng giáo trình

Yêu cầu đầu vào: Giai đoạn 0–2 (home lab có AD, đọc được Event Log/Sysmon, biết ATT&CK và risk). Học 12–15 giờ/tuần theo vòng **Xem video → Đọc → Lab → Ghi chú → Tự kiểm tra**; tỷ lệ khuyến nghị 25% lý thuyết, 75% thực hành.

Lộ trình lab xuyên suốt: [TryHackMe — SOC Level 1](https://tryhackme.com/path/outline/soclevel1) (path đã được làm mới, bắt đầu từ Blue Team Introduction và SOC Team Internals). Video xuyên suốt: [SOC Core Skills with John Strand — Antisyphon](https://www.antisyphontraining.com/product/soc-core-skills-with-john-strand/) (16 giờ, lớp live theo hình thức pay-what-you-can, bản ghi có trên YouTube).

### Vai trò trong SOC

| Vai trò | Công việc chính | Kỹ năng then chốt |
| --- | --- | --- |
| SOC Analyst Tier 1 | Triage alert, phân loại true/false positive, escalate | Đọc log nhanh, SIEM query, playbook |
| SOC Tier 2 / Incident Responder | Điều tra sâu, containment, phối hợp khắc phục | Forensics, EDR, ATT&CK, giao tiếp |
| Detection Engineer | Viết, test, tuning rule; đo coverage | Sigma/KQL/SPL, Detection-as-Code, Python |
| Threat Hunter | Chủ động tìm kẻ xâm nhập chưa bị phát hiện | Hypothesis, CTI, thống kê, baseline |
| DFIR Specialist | Phân tích disk/memory, malware, timeline | Volatility, KAPE, reverse cơ bản |

### Mục tiêu đầu ra

1. Hardening Windows/Linux/mạng theo CIS và đo được hiệu quả
2. Triển khai SIEM thu log từ nhiều nguồn, viết query SPL/KQL thành thạo
3. Viết, test, tuning detection rule (Sigma, YARA, Suricata) theo ATT&CK
4. Xử lý trọn vẹn một incident theo NIST SP 800-61, viết playbook và postmortem
5. Thu thập và phân tích bằng chứng disk, memory; phân tích malware đơn giản an toàn
6. Thực hiện threat hunt dựa trên giả thuyết

### Cấu trúc

| Module | Tuần | Nội dung chính | Sản phẩm nộp |
| --- | --- | --- | --- |
| 1. Hardening & Architecture | 1–2 | Endpoint, network, email, backup | Báo cáo hardening trước/sau |
| 2. Logging, SIEM & Detection | 3–8 | Nguồn log, SIEM, SPL/KQL, Sigma, YARA, Detection-as-Code | Home SOC + 20 rule có test |
| 3. Incident Response | 9–11 | Vòng đời IR, triage, playbook, SOAR, postmortem | 4 playbook + 1 postmortem |
| 4. Forensics & Malware | 12–15 | Artifact Windows/Linux, memory, malware static/dynamic | 2 báo cáo forensics + 1 báo cáo malware |
| 5. Threat Hunting & NSM | 16–17 | Hypothesis hunting, Zeek, RITA, CTI | 3 hunt report |
| Capstone | 18 | Purple team mini | Báo cáo capstone |

### Quy ước & an toàn

- Repo `security-foundations-notes/phase-3/` + repo riêng `detections` cho rule
- Máy lab cần thêm 8–16 GB RAM cho SIEM
- Malware chỉ phân tích trong VM cách ly: host-only network, tắt shared folder/clipboard, snapshot trước mỗi lần chạy
- Mỗi module kết thúc bằng "Góc nhìn bảo mật": kẻ tấn công né tránh ra sao và cách bịt lỗ hổng phát hiện

## Module 1 — Hardening & Security Architecture (Tuần 1–2)

Phòng ngừa rẻ hơn phát hiện; mỗi lớp hardening giảm số alert SOC phải xử lý. Video chính: Professor Messer SY0-701 mục 2.5 (Hardening Techniques, Mitigation Techniques) và 3.1–3.2.

### Chương 1.1 — Endpoint hardening (Tuần 1)

**Lý thuyết cần nắm**

- **Windows**: CIS Benchmark / Microsoft Security Baseline; tắt SMBv1, LLMNR, NBT-NS, WPAD; bật Credential Guard, LSA Protection (RunAsPPL), ASR rules của Defender, AppLocker/WDAC; LAPS; BitLocker
- **Linux**: CIS Benchmark, SSH key-only, `sysctl` hardening, AppArmor/SELinux, auditd, tắt service thừa
- **EDR/XDR**: telemetry, behavioral detection, isolate host; mã nguồn mở: Wazuh agent, Velociraptor
- Patch management: WSUS/Intune, unattended-upgrades; đo thời gian vá trung bình

**Video**: [Professor Messer SY0-701](https://www.professormesser.com/security-plus/sy0-701/sy0-701-video/sy0-701-comptia-security-plus-course/) mục 2.5 Hardening Techniques, 4.1 Hardening Targets, 4.5 Operating System Security

**Đọc**: [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks), [Microsoft Security Compliance Toolkit](https://learn.microsoft.com/windows/security/operating-system-security/device-management/windows-security-configuration-framework/security-compliance-toolkit-10), [Microsoft — Attack surface reduction rules](https://learn.microsoft.com/defender-endpoint/attack-surface-reduction-rules-reference)

**Lab**:

1. Chạy [PingCastle](https://www.pingcastle.com/) trên AD lab và [HardeningKitty](https://github.com/scipag/HardeningKitty) trên workstation → ghi điểm trước
2. Áp GPO baseline: tắt LLMNR/NBT-NS, SMB signing, LAPS, ASR rules, audit policy
3. Linux: áp CIS Level 1 bằng Ansible (role [ansible-lockdown](https://github.com/ansible-lockdown)), so sánh điểm Lynis trước/sau

### Chương 1.2 — Network security architecture (Tuần 2)

**Lý thuyết cần nắm**

- Segmentation theo vùng tin cậy (user, server, DMZ, management), micro-segmentation
- Firewall rule review: deny-by-default, xóa rule `any-any`, ghi owner + lý do + ngày hết hạn
- Egress filtering: DNS chỉ qua resolver nội bộ, HTTP/HTTPS qua proxy — chặn C2 và exfiltration
- IDS/IPS (Suricata), NSM (Zeek), WAF (ModSecurity + OWASP CRS), DNS filtering, NAC/802.1X
- Remote access: VPN + MFA hoặc ZTNA; bastion host cho quản trị

**Video**: Messer SY0-701 3.2 (Network Infrastructure Concepts, Firewall Types, Secure Communication), 4.5 (Firewalls, Web Filtering)

**Đọc**: [Suricata documentation](https://docs.suricata.io/), [OWASP CRS](https://coreruleset.org/)

**Lab**:

1. pfSense: chuyển sang egress deny-by-default, chỉ mở DNS/HTTP(S) qua proxy
2. Cài Suricata với ruleset ET Open trên pfSense hoặc [Security Onion](https://securityonionsolutions.com/)
3. Từ Kali kiểm tra Responder (LLMNR poisoning) thất bại sau hardening

### Chương 1.3 — Email security & backup (Tuần 2)

**Lý thuyết cần nắm**

- SPF, DKIM, **DMARC** (p=none → quarantine → reject), MTA-STS; sandbox attachment
- Backup **3-2-1-1-0**: 3 bản, 2 phương tiện, 1 offsite, 1 immutable/offline, 0 lỗi khi test restore; tách credential backup khỏi domain

**Video**: Messer SY0-701 4.5 (Email Security)

**Đọc**: [Cloudflare — What is DMARC?](https://www.cloudflare.com/learning/dns/dns-records/dns-dmarc-record/), [CISA — Ransomware Guide (phần backup)](https://www.cisa.gov/stopransomware/ransomware-guide)

**Lab**: kiểm tra SPF/DKIM/DMARC của 3 domain bằng `dig TXT`; dựng backup bất biến cho Ubuntu lab (ví dụ restic tới storage riêng) và test restore.

### Góc nhìn bảo mật — Module 1

- Kẻ tấn công tận dụng cấu hình mặc định: LLMNR, SMB không ký, admin dùng chung mật khẩu, egress mở toàn bộ
- Người phòng thủ: baseline + đo điểm định kỳ, ghi tài liệu mọi ngoại lệ

### Tiêu chí đạt Module 1

- [ ] Báo cáo hardening có điểm PingCastle / Lynis / HardeningKitty trước–sau
- [ ] Chứng minh ≥ 2 kỹ thuật (Responder, SMB relay) bị chặn sau hardening
- [ ] Tài liệu firewall rule có owner và lý do cho từng rule

## Module 2 — Logging, SIEM & Detection Engineering (Tuần 3–8)

Không có log đúng thì không có phát hiện, không có điều tra. Video chính: [SOC Core Skills — John Strand](https://www.antisyphontraining.com/product/soc-core-skills-with-john-strand/); lab chính: [TryHackMe SOC Level 1](https://tryhackme.com/path/outline/soclevel1) phần Core SOC Solutions và SIEM.

### Chương 2.1 — Nguồn log & pipeline (Tuần 3)

**Lý thuyết cần nắm**

| Nguồn | Dữ liệu quan trọng | Phát hiện được |
| --- | --- | --- |
| Windows Security + Sysmon | 4624/4625/4688/4769; Sysmon 1/3/10/11/13/22 | Brute force, process độc, credential dumping, persistence |
| PowerShell | 4104 Script Block | Script bị làm rối, download cradle |
| Linux auditd/journald | execve, sudo, SSH | Privilege escalation, reverse shell |
| Firewall / proxy | Allow/deny, URL, user-agent | C2 beacon, exfiltration |
| DNS resolver | Query, response, client | DGA, DNS tunneling |
| EDR | Process tree, network, file | Hành vi tấn công end-to-end |
| Cloud / SaaS | CloudTrail, Entra ID sign-in, M365 audit | Chiếm tài khoản cloud, inbox rule độc |
| Web / WAF | Access log, rule match | SQLi, web shell, scanning |

- Pipeline: agent → parse/normalize (ECS, OCSF) → lưu trữ hot/warm/cold → query/alert
- Đồng bộ NTP cho mọi nguồn — sai giờ làm hỏng timeline

**Video**: Messer SY0-701 4.4 (Security Monitoring, Security Tools), 4.9 (Log Data)

**Đọc**: [Sysmon — Microsoft Sysinternals](https://learn.microsoft.com/sysinternals/downloads/sysmon), [Elastic Common Schema](https://www.elastic.co/guide/en/ecs/current/index.html), [MITRE ATT&CK Data Sources](https://attack.mitre.org/datasources/)

**Lab**: vẽ sơ đồ log pipeline cho home lab; cài agent thu log từ DC, workstation (Sysmon + PowerShell logging), Ubuntu (auditd), pfSense (syslog).

### Chương 2.2 — SIEM & ngôn ngữ truy vấn (Tuần 4–5)

**Lý thuyết cần nắm**

| SIEM | Ngôn ngữ | Ưu điểm | Nhược điểm |
| --- | --- | --- | --- |
| Splunk | SPL | Mạnh, phổ biến, có BOTS dataset để học | Chi phí cao; bản Free giới hạn |
| Elastic Security | KQL, EQL, ES\|QL | Mã nguồn mở lõi, rule có sẵn, EQL cho sequence | Vận hành cụm tốn công |
| Microsoft Sentinel | KQL | Tích hợp M365/Entra/Defender | Phụ thuộc Azure, tính phí theo GB |
| Wazuh | Rule XML | Miễn phí, có FIM, SCA, vuln detection | Detection logic đơn giản hơn |
| Security Onion | Elastic + Zeek + Suricata | All-in-one NSM + SIEM cho lab | Cần tài nguyên lớn |

**Ví dụ — "IP nào đăng nhập thất bại > 20 lần trong 10 phút?"**

```
# Splunk SPL
index=wineventlog EventCode=4625
| bin _time span=10m
| stats count by _time, src_ip
| where count > 20

# Microsoft Sentinel KQL
SecurityEvent
| where EventID == 4625
| summarize Failures = count() by IpAddress, bin(TimeGenerated, 10m)
| where Failures > 20
```

**Video**: [Splunk Education — khóa miễn phí](https://www.splunk.com/en_us/training/free-courses/overview.html) (Intro to Splunk, Using Fields); [Microsoft Learn — KQL](https://learn.microsoft.com/kusto/query/)

**Đọc**: [Splunk Search Reference](https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/WhatsInThisManual), [Wazuh documentation](https://documentation.wazuh.com/current/)

**Lab**:

1. Triển khai [Wazuh](https://wazuh.com/) hoặc Elastic Stack (docker compose), thu ≥ 5 nguồn log, dựng dashboard tổng quan
2. Splunk **Boss of the SOC** ([BOTS v3 dataset](https://github.com/splunk/botsv3)) trên Splunk Free; viết write-up
3. [Microsoft Learn — KQL tutorial](https://learn.microsoft.com/kusto/query/tutorials/learn-common-operators) trên dữ liệu mẫu

### Chương 2.3 — Detection Engineering (Tuần 6–8)

**Lý thuyết cần nắm**

- Vòng đời rule: Requirement (technique + data source) → Develop → Test (Atomic Red Team) → Deploy → Tune → Review
- Pyramid of Pain: hash < IP < domain < artifact < tool < **TTP**
- **Sigma** (rule chung, chuyển sang SPL/KQL bằng `sigma-cli`), **YARA** (file/malware), **Suricata** (network)
- Detection-as-Code: rule trong Git, CI kiểm cú pháp, test tự động, review qua pull request
- Đo lường: ATT&CK coverage, precision, MTTD; mỗi rule có mô tả, mức độ, false positive đã biết, hướng dẫn triage

**Ví dụ Sigma — Office sinh PowerShell (T1059.001, T1566.001):**

```yaml
title: Office Application Spawning PowerShell
id: 00000000-0000-0000-0000-000000000000  # thay bằng UUID mới
status: experimental
description: Word/Excel/Outlook khởi chạy PowerShell, dấu hiệu phổ biến của macro độc
tags:
  - attack.execution
  - attack.t1059.001
  - attack.t1566.001
logsource:
  category: process_creation
  product: windows
detection:
  selection_parent:
    ParentImage|endswith:
      - '\WINWORD.EXE'
      - '\EXCEL.EXE'
      - '\OUTLOOK.EXE'
  selection_child:
    Image|endswith:
      - '\powershell.exe'
      - '\pwsh.exe'
  condition: selection_parent and selection_child
falsepositives:
  - Add-in nội bộ hợp lệ (allowlist theo hash/đường dẫn)
level: high
```

**Video**: kênh [Antisyphon Training (YouTube)](https://www.youtube.com/@AntisyphonTraining) — các buổi Anti-Cast về detection; [SigmaHQ — Getting started](https://sigmahq.io/docs/basics/rules.html)

**Đọc**: [SigmaHQ rules](https://github.com/SigmaHQ/sigma), [YARA documentation](https://yara.readthedocs.io/), [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team), [Palantir — Alerting and Detection Strategy Framework](https://github.com/palantir/alerting-detection-strategy-framework)

**Lab**:

1. Cài Atomic Red Team trên workstation lab, chạy 20 test thuộc 6 tactic
2. Viết 20 Sigma rule, chuyển đổi bằng [sigma-cli](https://github.com/SigmaHQ/sigma-cli), triển khai lên SIEM; ghi detect/miss và lý do
3. Viết 3 YARA rule cho mẫu từ [MalwareBazaar](https://bazaar.abuse.ch/) (trong VM cách ly)
4. Repo `detections` trên GitHub + GitHub Actions kiểm cú pháp
5. Tô coverage hiện tại bằng [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)

### Góc nhìn bảo mật — Module 2

- Kẻ tấn công: xóa log, tắt agent, dùng LOLBin để né rule dựa trên tên file, đổi IOC liên tục
- Người phòng thủ: alert khi agent im lặng hoặc log bị xóa (1102), rule theo hành vi, test rule định kỳ bằng Atomic

### Tiêu chí đạt Module 2

- [ ] Home SOC thu ≥ 5 nguồn log, có dashboard
- [ ] 20 rule có metadata, test bằng Atomic, tỷ lệ phát hiện ≥ 80%
- [ ] Write-up 1 bộ BOTS
- [ ] Viết cùng một truy vấn bằng SPL và KQL không tra cứu

## Module 3 — Incident Response (Tuần 9–11)

IR là nơi "chịu trách nhiệm" thể hiện rõ nhất: quyết định nhanh dưới áp lực, ghi lại mọi hành động, giao tiếp minh bạch. Video chính: Messer SY0-701 mục 4.8 (Incident Response, Incident Planning, Digital Forensics).

### Chương 3.1 — Vòng đời IR & triage (Tuần 9)

**Lý thuyết cần nắm**

| Pha | Mục tiêu | Hành động chính |
| --- | --- | --- |
| Preparation | Sẵn sàng trước sự cố | IR plan, playbook, danh bạ, kênh liên lạc out-of-band, tabletop |
| Detection & Analysis | Xác nhận và hiểu phạm vi | Triage, severity, thu bằng chứng, timeline, IOC/TTP |
| Containment | Ngăn lan rộng | Isolate host qua EDR, disable account, block IP/domain |
| Eradication | Loại bỏ kẻ tấn công | Xóa persistence, vá, reset credential (kể cả krbtgt 2 lần nếu AD bị chiếm) |
| Recovery | Hoạt động lại an toàn | Restore từ backup sạch, giám sát tăng cường |
| Lessons Learned | Cải tiến | Blameless postmortem, action item có owner |

| Severity | Ví dụ | Phản hồi mẫu |
| --- | --- | --- |
| SEV-1 | Ransomware đang mã hóa, Domain Admin bị chiếm | Ngay lập tức, 24/7 |
| SEV-2 | Server bị xâm nhập, tài khoản đặc quyền đăng nhập bất thường | ≤ 1 giờ |
| SEV-3 | 1 workstation nhiễm malware đã bị EDR chặn | ≤ 4 giờ |
| SEV-4 | Phishing được báo cáo, chưa ai click | ≤ 1 ngày làm việc |

**Video**: Messer SY0-701 4.8; [SOC Core Skills](https://www.antisyphontraining.com/product/soc-core-skills-with-john-strand/) phần The Incident Response Process

**Đọc**: [NIST SP 800-61 Rev. 3](https://csrc.nist.gov/pubs/sp/800/61/r3/final), [SANS Incident Handler's Handbook](https://www.sans.org/white-papers/33901/)

**Lab**: 5 case trên [LetsDefend](https://letsdefend.io/) hoặc [Blue Team Labs Online](https://blueteamlabs.online/), viết báo cáo case theo mẫu: alert → xác minh → phạm vi → hành động → kết luận.

### Chương 3.2 — Playbook & SOAR (Tuần 10)

**Lý thuyết cần nắm** — playbook mẫu "Tài khoản M365/Entra bị chiếm":

1. **Xác nhận**: sign-in log (vị trí, IP, thiết bị lạ, impossible travel), MFA prompt bất thường, inbox rule mới
2. **Ngăn chặn**: revoke session/refresh token, reset mật khẩu, đăng ký lại MFA, block IP
3. **Phạm vi**: mail đã gửi/chuyển tiếp, file truy cập, OAuth app được cấp quyền, người nhận phishing nội bộ
4. **Loại bỏ**: xóa inbox rule, OAuth app độc, thiết bị MFA lạ
5. **Khôi phục & thông báo**: báo user/đối tác; đánh giá nghĩa vụ thông báo vi phạm dữ liệu cá nhân
6. **Cải tiến**: Conditional Access, phishing-resistant MFA, rule phát hiện inbox rule đáng ngờ

- SOAR: tự động enrichment, tạo ticket, isolate host — [TheHive](https://strangebee.com/thehive/) + Cortex, [Shuffle](https://shuffler.io/)
- Metrics: MTTD, MTTA, MTTC, MTTR, tỷ lệ true positive

**Đọc**: [Microsoft — Incident response playbooks](https://learn.microsoft.com/security/operations/incident-response-playbooks), [CISA — Incident & Vulnerability Response Playbooks](https://www.cisa.gov/resources-tools/resources/federal-government-cybersecurity-incident-and-vulnerability-response-playbooks)

**Lab**:

1. Viết 4 playbook (Phishing, Ransomware, Account Compromise, Web shell) kèm sơ đồ quyết định và query mẫu
2. TheHive + Cortex bằng Docker, nhận alert từ Wazuh/Elastic
3. Workflow Shuffle: alert → enrichment VirusTotal/AbuseIPDB → tạo case

### Chương 3.3 — Giao tiếp, tabletop & postmortem (Tuần 11)

**Lý thuyết cần nắm**

- Vai trò: Incident Commander, Technical Lead, Scribe, Communications Lead
- Ghi timestamp mọi hành động; không tắt máy khi chưa thu memory; kênh liên lạc riêng nếu email/chat có thể bị theo dõi
- Postmortem: Tóm tắt → Tác động → Timeline (UTC) → Root cause (5 Whys) → Điều hiệu quả / chưa hiệu quả → Action items → IOC; nguyên tắc blameless

**Đọc**: [CISA Tabletop Exercise Packages](https://www.cisa.gov/resources-tools/services/cisa-tabletop-exercise-packages), [Google SRE Book — Postmortem Culture](https://sre.google/sre-book/postmortem-culture/)

**Lab**: tổ chức tabletop ransomware với bạn cùng lớp bằng kịch bản CISA; mô phỏng 1 sự cố trong lab (bạn đóng cả hai vai), xử lý theo playbook và viết postmortem.

### Góc nhìn bảo mật — Module 3

- Kẻ tấn công tận dụng sự hỗn loạn: xóa dấu vết khi thấy bị phát hiện, quay lại qua persistence chưa bị gỡ
- Người phòng thủ: xác định đủ phạm vi trước khi eradicate, thay đồng loạt credential, giám sát tăng cường sau recovery

### Tiêu chí đạt Module 3

- [ ] 4 playbook có bước cụ thể, query mẫu, điều kiện escalate
- [ ] Pipeline SOAR tự động enrichment hoạt động
- [ ] 1 postmortem với timeline UTC và action item
- [ ] Giải thích vì sao không reboot máy nhiễm trước khi thu memory

## Module 4 — Digital Forensics & Malware Analysis (Tuần 12–15)

Forensics trả lời "chuyện gì đã xảy ra, khi nào, bằng cách nào" với bằng chứng bảo vệ được. Video chính: kênh 13Cubed (video "Introduction to Windows Forensics" và loạt Investigating Windows) và [SANS DFIR posters](https://www.sans.org/posters/).

### Chương 4.1 — Nguyên tắc & Windows artifacts (Tuần 12)

**Lý thuyết cần nắm**

- **Order of volatility** (RFC 3227): CPU/cache → RAM → network state → process → disk → log từ xa → backup
- Chain of custody: ai thu, khi nào, ở đâu, SHA-256 trước/sau, nơi lưu; làm việc trên bản sao

| Artifact | Chứng minh | Công cụ |
| --- | --- | --- |
| Prefetch | Chương trình đã chạy, số lần, thời điểm | PECmd |
| Amcache, Shimcache | Dấu vết thực thi/có mặt của file | AmcacheParser, AppCompatCacheParser |
| UserAssist, ShellBags, RecentDocs | Hành vi người dùng | Registry Explorer, RECmd |
| LNK, Jump Lists | File đã mở, ổ USB | LECmd, JLECmd |
| $MFT, $UsnJrnl | Tạo/sửa/xóa file | MFTECmd |
| SRUM | Sử dụng mạng theo ứng dụng | SrumECmd |
| Event Logs | Đăng nhập, service, task, PowerShell | EvtxECmd, Hayabusa, Chainsaw |

**Video**: 13Cubed — Introduction to Windows Forensics (YouTube); Messer SY0-701 4.8 (Digital Forensics)

**Đọc**: [SANS Windows Forensic Analysis poster](https://www.sans.org/posters/windows-forensic-analysis/), [Eric Zimmerman's tools](https://ericzimmerman.github.io/), [RFC 3227](https://datatracker.ietf.org/doc/html/rfc3227)

**Lab**: TryHackMe phòng [Windows Forensics 1](https://tryhackme.com/room/windowsforensics1) và [Windows Forensics 2](https://tryhackme.com/room/windowsforensics2); thu triage bằng [KAPE](https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape) trên workstation lab sau khi chạy chuỗi Atomic Red Team.

### Chương 4.2 — Timeline & Linux forensics (Tuần 13)

**Lý thuyết cần nắm**

- Timeline: [Plaso/log2timeline](https://github.com/log2timeline/plaso) → Timeline Explorer; super-timeline
- Thu từ xa hàng loạt máy: [Velociraptor](https://docs.velociraptor.app/)
- Linux: `/var/log`, `.bash_history`, cron, systemd unit, `/tmp`, `authorized_keys`, `wtmp/btmp`; công cụ [UAC](https://github.com/tclahr/uac)
- EVTX nhanh: [Hayabusa](https://github.com/Yamato-Security/hayabusa), [Chainsaw](https://github.com/WithSecureLabs/chainsaw) (áp rule Sigma lên log)

**Lab**: chạy Hayabusa trên bộ [EVTX-ATTACK-SAMPLES](https://github.com/sbousseaden/EVTX-ATTACK-SAMPLES), giải thích 10 phát hiện; dựng timeline từ KAPE triage ở Chương 4.1.

### Chương 4.3 — Memory forensics (Tuần 13)

**Lý thuyết cần nắm**

- Thu memory: WinPmem, DumpIt; Linux: AVML, LiME
- [Volatility 3](https://github.com/volatilityfoundation/volatility3): `windows.pslist`, `pstree`, `psscan`, `cmdline`, `netscan`, `malfind`, `dlllist`, `svcscan`
- Dấu hiệu: process không có parent hợp lệ, `svchost.exe` ngoài `System32`, vùng nhớ RWX chứa header MZ, kết nối ra IP lạ

```bash
vol -f mem.raw windows.info
vol -f mem.raw windows.pstree
vol -f mem.raw windows.netscan
vol -f mem.raw windows.malfind --dump
vol -f mem.raw windows.cmdline --pid 4242
```

**Đọc**: [SANS Memory Forensics Cheat Sheet](https://www.sans.org/posters/memory-forensics-cheat-sheet/), [Volatility 3 documentation](https://volatility3.readthedocs.io/)

**Lab**: [MemLabs](https://github.com/stuxnet999/MemLabs) lab 1–3; TryHackMe phòng [Volatility](https://tryhackme.com/room/volatility); thu memory workstation lab và tìm process injection sau khi chạy Atomic T1055.

### Chương 4.4 — Malware analysis cơ bản (Tuần 14–15)

**Lý thuyết cần nắm**

- Môi trường: [FLARE VM](https://github.com/mandiant/flare-vm) (Windows), [REMnux](https://remnux.org/) (Linux), mạng host-only + INetSim/FakeNet-NG, snapshot
- Static: hash, strings/FLOSS, PE header (PEStudio, Detect It Easy), import table, entropy, YARA, [CAPA](https://github.com/mandiant/capa)
- Dynamic: Procmon, System Informer, Regshot, Wireshark/FakeNet, Sysmon; sandbox online cho mẫu không nhạy cảm (Any.Run, Hybrid Analysis)
- Document & script: [oletools](https://github.com/decalage2/oletools) (`olevba`), [CyberChef](https://gchq.github.io/CyberChef/)
- Đầu ra: IOC, TTP theo ATT&CK, YARA/Sigma để phát hiện

**Đọc**: sách *Practical Malware Analysis* (Michael Sikorski, Andrew Honig) chương 1–3; [SANS — Cheat Sheet for Analyzing Malicious Documents](https://www.sans.org/posters/cheat-sheet-for-analyzing-malicious-documents/)

**Lab**:

1. Dựng FLARE VM + REMnux cách ly
2. Phân tích tĩnh/động 2 mẫu từ [MalwareBazaar](https://bazaar.abuse.ch/) thuộc họ phổ biến có báo cáo công khai để đối chiếu
3. Phân tích 1 file Office có macro bằng `olevba`
4. [CyberDefenders](https://cyberdefenders.org/) / BTLO: 5 challenge Endpoint Forensics và Malware Analysis

### Góc nhìn bảo mật — Module 4

- Kẻ tấn công: timestomping, xóa log, fileless malware chỉ nằm trong RAM, packing/obfuscation
- Người phòng thủ: đối chiếu nhiều nguồn artifact ($MFT vs $UsnJrnl vs Prefetch), thu memory sớm, log tập trung ngoài máy

### Tiêu chí đạt Module 4

- [ ] 2 báo cáo forensics (1 disk/triage, 1 memory) có timeline và chain of custody
- [ ] 1 báo cáo malware: IOC, TTP, YARA rule, khuyến nghị phát hiện
- [ ] Kể được 8 artifact Windows và ý nghĩa chứng minh

## Module 5 — Threat Hunting & Network Security Monitoring (Tuần 16–17)

Hunting là giả định rule đã bỏ sót và chủ động đi tìm — kỹ năng giúp phản ứng trước mối đe dọa chưa có signature. Video chính: các buổi threat hunting miễn phí trên kênh [Antisyphon Training](https://www.youtube.com/@AntisyphonTraining); khóa [MITRE ATT&CK CTI Training](https://attack.mitre.org/resources/learn-more-about-attack/training/cti/).

### Chương 5.1 — Phương pháp hunting (Tuần 16)

**Lý thuyết cần nắm**

- **Hypothesis-driven**: "Nếu kẻ tấn công dùng WMI để lateral movement, ta sẽ thấy `WmiPrvSE.exe` sinh process lạ trên nhiều máy"
- **Intel-driven**: từ báo cáo CTI mới → tìm TTP/IOC tương ứng
- **Data-driven**: stack counting, baseline, long-tail analysis
- Khung [PEAK](https://www.splunk.com/en_us/blog/security/peak-threat-hunting-framework.html) (Prepare, Execute, Act with Knowledge); kết quả hunt luôn để lại rule mới, khoảng trống log, hoặc incident

| Giả thuyết | ATT&CK | Dữ liệu | Cách tìm |
| --- | --- | --- | --- |
| C2 beaconing đều đặn | T1071 | Zeek conn log, proxy | Khoảng cách kết nối đều, độ lệch chuẩn thấp (RITA) |
| Persistence qua task / Run key | T1053, T1547 | Sysmon 1, 13; 4698 | Stack count, đường dẫn trong `AppData`/`Temp` |
| Credential dumping LSASS | T1003.001 | Sysmon 10 | GrantedAccess bất thường tới `lsass.exe` |
| Living-off-the-land | T1218 | Sysmon 1 | `rundll32`, `regsvr32`, `mshta`, `certutil` kèm URL |
| DNS tunneling | T1071.004 | DNS log | Subdomain dài, entropy cao, nhiều TXT query |
| Kerberoasting | T1558.003 | 4769 | Nhiều ticket RC4 từ 1 user trong thời gian ngắn |

**Đọc**: [The ThreatHunting Project](https://www.threathunting.net/), [The DFIR Report](https://thedfirreport.com/) (chọn 1 báo cáo gần đây làm nguồn giả thuyết)

**Lab**: 3 hunt trong home SOC theo bảng trên (sau khi mô phỏng bằng Atomic Red Team); chuyển 1 báo cáo The DFIR Report thành 3 giả thuyết + query.

### Chương 5.2 — Network Security Monitoring (Tuần 17)

**Lý thuyết cần nắm**

- [Zeek](https://zeek.org/): log `conn`, `dns`, `http`, `ssl`, `files`, `x509` — metadata giàu ngữ cảnh, nhẹ hơn full PCAP
- [Suricata](https://suricata.io/): alert signature + EVE JSON; fingerprint TLS (JA3/JA4)
- [RITA](https://github.com/activecm/rita): phát hiện beacon, DNS tunneling, long connection từ Zeek log

**Video**: TryHackMe phòng [Zeek](https://tryhackme.com/room/zeekbro) và [Snort](https://tryhackme.com/room/snort) (có hướng dẫn từng bước)

**Đọc**: [Zeek documentation](https://docs.zeek.org/), sách *The Practice of Network Security Monitoring* (Richard Bejtlich)

**Lab**: chạy Zeek trên PCAP từ [Malware-Traffic-Analysis.net](https://www.malware-traffic-analysis.net/), phân tích bằng `zeek-cut` và RITA; mô phỏng beacon C2 trong mạng cách ly của lab và phát hiện bằng RITA.

### Chương 5.3 — Threat Intelligence cho SOC (Tuần 17)

**Lý thuyết cần nắm**

- Cấp độ: strategic, operational, tactical (TTP), technical (IOC)
- Nguồn mở: CISA advisories, The DFIR Report, abuse.ch (URLhaus, ThreatFox), AlienVault OTX
- Nền tảng: [MISP](https://www.misp-project.org/), [OpenCTI](https://filigran.io/solutions/open-cti/); STIX 2.1 / TAXII

**Video**: [MITRE ATT&CK CTI Training](https://attack.mitre.org/resources/learn-more-about-attack/training/cti/) module 1–3

**Lab**: MISP (Docker), import feed abuse.ch, tích hợp với SIEM để match IOC; TryHackMe phòng [MISP](https://tryhackme.com/room/misp).

### Góc nhìn bảo mật — Module 5

- Kẻ tấn công: beacon có jitter, domain fronting, dùng dịch vụ cloud hợp lệ làm C2
- Người phòng thủ: hunt theo hành vi thay vì IOC, baseline traffic bình thường, kết hợp network + endpoint

### Tiêu chí đạt Module 5

- [ ] 3 hunt report: giả thuyết, dữ liệu, query, kết quả, rule/khoảng trống phát sinh
- [ ] Phát hiện beacon C2 lab bằng RITA/Zeek
- [ ] MISP có ít nhất 1 match IOC được xác minh

## Lịch học 18 tuần

Mỗi tuần khoảng 12–15 giờ: 3–4 giờ video/đọc, 8–9 giờ lab, 1–2 giờ viết báo cáo/write-up.

| Tuần | Chủ đề | Video / đọc | Lab | Sản phẩm |
| --- | --- | --- | --- | --- |
| 1 | Endpoint hardening Windows/AD | Messer 2.5, 4.1; CIS Benchmarks | PingCastle, GPO baseline, LAPS | Điểm trước–sau |
| 2 | Network, email, backup | Messer 3.2, 4.5; Suricata docs | Egress deny, Suricata, Responder thất bại | **Báo cáo hardening** |
| 3 | Nguồn log, pipeline | Messer 4.4, 4.9; Sysmon docs | Thu log 5 nguồn, NTP | Sơ đồ log pipeline |
| 4 | SIEM & SPL | [Splunk free courses](https://www.splunk.com/en_us/training/free-courses/overview.html) | Splunk Free + BOTS v3 | Write-up BOTS (nửa đầu) |
| 5 | KQL, dashboard, Wazuh/Elastic | Microsoft Learn KQL | Dashboard home SOC | Write-up BOTS hoàn chỉnh |
| 6 | Detection engineering, Sigma | SigmaHQ docs; [SOC Core Skills](https://www.antisyphontraining.com/product/soc-core-skills-with-john-strand/) | Atomic 10 test, 10 Sigma rule | Repo `detections` |
| 7 | YARA, Suricata rule, tuning FP | YARA docs | 10 Sigma rule tiếp, 3 YARA | Coverage ATT&CK lần 1 |
| 8 | Detection-as-Code, metrics | Palantir ADS Framework | GitHub Actions kiểm rule | **Home SOC + 20 rule** |
| 9 | IR lifecycle, triage | Messer 4.8; NIST SP 800-61r3 | LetsDefend/BTLO 3 case | Báo cáo case |
| 10 | Playbook, SOAR | Microsoft IR playbooks | TheHive + Cortex + Shuffle | 4 playbook |
| 11 | Tabletop, postmortem | CISA Tabletop; Google SRE postmortem | Mô phỏng sự cố trong lab | **Postmortem** |
| 12 | Nguyên tắc forensics, Windows artifacts | 13Cubed; SANS poster | THM Windows Forensics 1–2, KAPE | Ghi chú artifact |
| 13 | Timeline, memory forensics | Volatility docs | Hayabusa, MemLabs, Volatility | **Báo cáo memory** |
| 14 | Malware static | Practical Malware Analysis ch.1–3 | FLARE VM, PEStudio, CAPA, FLOSS | Ghi chú phân tích |
| 15 | Malware dynamic, document malware | SANS malicious documents cheat sheet | Procmon, FakeNet, olevba | **Báo cáo malware + YARA** |
| 16 | Threat hunting | ThreatHunting Project; The DFIR Report | 2 hunt | Hunt report 1–2 |
| 17 | NSM, CTI | Zeek docs; ATT&CK CTI Training | Zeek, RITA, MISP | Hunt report 3 |
| 18 | Ôn tập & capstone | Ôn ghi chú | Capstone | **Báo cáo capstone** |

## Kiểm tra cuối giai đoạn (Tuần 18)

Đạt khi trả lời trơn tru ≥ 80% câu hỏi và hoàn thành capstone có báo cáo.

### Câu hỏi tự đánh giá

**Hardening & Logging**

1. Chỉ được thu 5 loại log cho doanh nghiệp 200 người, bạn chọn loại nào và vì sao?
2. Vì sao tắt LLMNR/NBT-NS và bật SMB signing là ưu tiên cao trong AD?
3. Egress filtering chặn được những giai đoạn nào của Kill Chain?

**Detection**

4. Vì sao rule dựa trên TTP bền hơn rule dựa trên hash/IP?
5. Rule tạo 300 alert/ngày, 95% false positive — bạn tuning theo các bước nào?
6. Viết truy vấn SPL và KQL tìm process con của `winword.exe`.

**Incident Response**

7. Phân biệt containment ngắn hạn và dài hạn với ví dụ ransomware.
8. Khi AD bị chiếm Domain Admin, những bước eradication nào bắt buộc?
9. MTTD và MTTR tính thế nào, dùng để cải tiến điều gì?
10. Vì sao postmortem cần blameless?

**Forensics & Malware**

11. Order of volatility là gì? Thu gì trước trên server đang chạy?
12. Prefetch và Amcache chứng minh điều gì? Giới hạn của chúng?
13. Plugin Volatility nào phát hiện process injection và dấu hiệu là gì?
14. Môi trường phân tích malware an toàn cần những điều kiện nào?

**Hunting**

15. Viết giả thuyết hunt cho T1003.001 kèm truy vấn.
16. RITA phát hiện beacon dựa trên đặc điểm nào của kết nối?

### Capstone: "Purple team mini" trong home lab

Kịch bản bạn tự mô phỏng trên hệ thống của mình: phishing macro → PowerShell tải payload → persistence bằng scheduled task → dump LSASS → lateral movement sang server → exfiltration qua HTTPS/DNS. Dùng [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team) hoặc [MITRE Caldera](https://caldera.mitre.org/).

- [ ] Kế hoạch mô phỏng map ATT&CK
- [ ] Ghi nhận bước nào bị phát hiện, bước nào bị bỏ sót
- [ ] Xử lý như incident thật theo playbook (case trong TheHive)
- [ ] Thu memory + triage, dựng timeline đầy đủ
- [ ] Viết rule mới cho mọi bước bị bỏ sót, chạy lại để xác minh
- [ ] Báo cáo 10–15 trang: tóm tắt lãnh đạo, timeline, phân tích, coverage trước/sau, khuyến nghị

Chứng chỉ gợi ý sau giai đoạn: [TryHackMe SAL1](https://tryhackme.com/resources/blog/complete-soc-analyst-learning-path-from-beginner-to-job-ready-in-2026), BTL1, CompTIA CySA+; xa hơn GCIH, GCFA — kiểm tra phiên bản và giá trên trang chính thức.

## Nguồn tham khảo

Các link đánh dấu (✓) đã được kiểm tra qua tìm kiếm ngày 23/11/2026; các link còn lại là trang chính thức của dự án/nhà cung cấp, nên mở lại để xác nhận trước khi dùng.

### Video, khóa học & lab

| Nguồn | Loại | Chi phí | Dùng cho |
| --- | --- | --- | --- |
| [TryHackMe — SOC Level 1](https://tryhackme.com/path/outline/soclevel1) ✓ | Lab path | Trả phí (có phần miễn phí) | Toàn giai đoạn |
| [SOC Core Skills with John Strand](https://www.antisyphontraining.com/product/soc-core-skills-with-john-strand/) ✓ | Khóa 16 giờ | Pay-what-you-can, bản ghi trên YouTube | Module 2, 3 |
| [Professor Messer SY0-701](https://www.professormesser.com/security-plus/sy0-701/sy0-701-video/sy0-701-comptia-security-plus-course/) ✓ | Video | Miễn phí | Module 1–3 |
| [MITRE ATT&CK CTI Training](https://attack.mitre.org/resources/learn-more-about-attack/training/cti/) ✓ | Khóa tự học | Miễn phí | Module 5 |
| [TryHackMe SAL1 — lộ trình SOC Analyst](https://tryhackme.com/resources/blog/complete-soc-analyst-learning-path-from-beginner-to-job-ready-in-2026) ✓ | Bài hướng dẫn | Miễn phí | Định hướng chứng chỉ |
| [Antisyphon Training (YouTube)](https://www.youtube.com/@AntisyphonTraining) | Video | Miễn phí | Module 2, 5 |
| 13Cubed (YouTube) — Introduction to Windows Forensics | Video | Miễn phí | Module 4 |
| [Splunk free courses](https://www.splunk.com/en_us/training/free-courses/overview.html) | Khóa học | Miễn phí | Module 2 |
| [Microsoft Learn — KQL](https://learn.microsoft.com/kusto/query/) | Tài liệu + tutorial | Miễn phí | Module 2 |
| [Blue Team Labs Online](https://blueteamlabs.online/), [CyberDefenders](https://cyberdefenders.org/), [LetsDefend](https://letsdefend.io/) | Lab | Freemium | Module 3, 4 |
| [Splunk BOTS v3](https://github.com/splunk/botsv3), [MemLabs](https://github.com/stuxnet999/MemLabs), [EVTX-ATTACK-SAMPLES](https://github.com/sbousseaden/EVTX-ATTACK-SAMPLES), [Malware-Traffic-Analysis.net](https://www.malware-traffic-analysis.net/), [MalwareBazaar](https://bazaar.abuse.ch/) | Dữ liệu luyện tập | Miễn phí | Module 2, 4, 5 |

### Công cụ

| Công cụ | Dùng cho |
| --- | --- |
| [Wazuh](https://wazuh.com/), [Security Onion](https://securityonionsolutions.com/), [Sysmon](https://learn.microsoft.com/sysinternals/downloads/sysmon) | SIEM / log |
| [Sigma](https://github.com/SigmaHQ/sigma), [sigma-cli](https://github.com/SigmaHQ/sigma-cli), [YARA](https://yara.readthedocs.io/), [Suricata](https://suricata.io/), [Zeek](https://zeek.org/), [RITA](https://github.com/activecm/rita) | Detection & NSM |
| [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team), [MITRE Caldera](https://caldera.mitre.org/) | Mô phỏng để test |
| [TheHive](https://strangebee.com/thehive/), [Shuffle](https://shuffler.io/), [MISP](https://www.misp-project.org/), [OpenCTI](https://filigran.io/solutions/open-cti/) | IR, SOAR, CTI |
| [KAPE](https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape), [Eric Zimmerman's tools](https://ericzimmerman.github.io/), [Velociraptor](https://docs.velociraptor.app/), [Plaso](https://github.com/log2timeline/plaso), [Hayabusa](https://github.com/Yamato-Security/hayabusa), [Chainsaw](https://github.com/WithSecureLabs/chainsaw) | Forensics |
| [Volatility 3](https://github.com/volatilityfoundation/volatility3), [FLARE VM](https://github.com/mandiant/flare-vm), [REMnux](https://remnux.org/), [CAPA](https://github.com/mandiant/capa), [oletools](https://github.com/decalage2/oletools), [CyberChef](https://gchq.github.io/CyberChef/) | Memory & malware |
| [PingCastle](https://www.pingcastle.com/), [HardeningKitty](https://github.com/scipag/HardeningKitty) | Hardening |

### Chuẩn & tài liệu

| Tài liệu | Dùng cho |
| --- | --- |
| [NIST SP 800-61 Rev. 3](https://csrc.nist.gov/pubs/sp/800/61/r3/final) | Module 3 |
| [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks) | Module 1 |
| [CISA Tabletop Exercise Packages](https://www.cisa.gov/resources-tools/services/cisa-tabletop-exercise-packages) | Module 3 |
| [Microsoft — Incident response playbooks](https://learn.microsoft.com/security/operations/incident-response-playbooks) | Module 3 |
| [SANS DFIR posters](https://www.sans.org/posters/) | Module 4 |
| [MITRE ATT&CK](https://attack.mitre.org/), [D3FEND](https://d3fend.mitre.org/) | Toàn giai đoạn |
| [The DFIR Report](https://thedfirreport.com/), [The ThreatHunting Project](https://www.threathunting.net/) | Module 5 |

### Sách

| Sách | Tác giả |
| --- | --- |
| *Blue Team Handbook: SOC, SIEM, and Threat Hunting* | Don Murdoch |
| *Incident Response & Computer Forensics* (3rd ed.) | Jason Luttgens, Matthew Pepe, Kevin Mandia |
| *The Art of Memory Forensics* | Michael Hale Ligh và cộng sự |
| *Practical Malware Analysis* | Michael Sikorski, Andrew Honig |
| *The Practice of Network Security Monitoring* | Richard Bejtlich |
