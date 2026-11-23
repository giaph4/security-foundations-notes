# Giai đoạn 3: Phòng thủ — Blue Team

> **Thời lượng:** 4–5 tháng · **Trọng tâm:** SOC, SIEM, detection, IR, forensics
> **Trạng thái giai đoạn:** ⬜ Chưa bắt đầu · 🟨 Đang học · ✅ Đạt gate

📖 Giáo trình chi tiết: [Giáo trình Giai đoạn 3 Phòng thủ — Blue Team (bản chi tiết)](../giao-trinh/Gi%C3%A1o%20tr%C3%ACnh%20Giai%20%C4%91o%E1%BA%A1n%203%20Ph%C3%B2ng%20th%E1%BB%A7%20%E2%80%94%20Blue%20Team%20%28b%E1%BA%A3n%20chi%20ti%E1%BA%BFt%29.md)
🗺 Roadmap tổng: [Roadmap An ninh mạng & An toàn thông tin](../roadmap/Roadmap%20An%20ninh%20m%E1%BA%A1ng%20%26%20An%20to%C3%A0n%20th%C3%B4ng%20tin.md)

> Rèn khả năng **phản ứng linh hoạt**: phát hiện sớm, khoanh vùng nhanh, khôi phục có kiểm soát.


## Bản đồ module & chương

| Module | Chương | Thời gian | Trạng thái |
| --- | --- | --- | --- |
| **[1. Hardening & Security Architecture](m1-hardening-security-architecture/README.md)** | 3 chương | Tuần 1–2 | ⬜ |
| | [1.1 Endpoint hardening](m1-hardening-security-architecture/1.1-endpoint-hardening.md) | Tuần 1 | ⬜ |
| | [1.2 Network security architecture](m1-hardening-security-architecture/1.2-network-security-architecture.md) | Tuần 2 | ⬜ |
| | [1.3 Email security & backup](m1-hardening-security-architecture/1.3-email-security-backup.md) | Tuần 2 | ⬜ |
| **[2. Logging, SIEM & Detection Engineering](m2-logging-siem-detection-engineering/README.md)** | 3 chương | Tuần 3–8 | ⬜ |
| | [2.1 Nguồn log & pipeline](m2-logging-siem-detection-engineering/2.1-nguon-log-pipeline.md) | Tuần 3 | ⬜ |
| | [2.2 SIEM & ngôn ngữ truy vấn](m2-logging-siem-detection-engineering/2.2-siem-ngon-ngu-truy-van.md) | Tuần 4–5 | ⬜ |
| | [2.3 Detection Engineering](m2-logging-siem-detection-engineering/2.3-detection-engineering.md) | Tuần 6–8 | ⬜ |
| **[3. Incident Response](m3-incident-response/README.md)** | 3 chương | Tuần 9–11 | ⬜ |
| | [3.1 Vòng đời IR & triage](m3-incident-response/3.1-vong-doi-ir-triage.md) | Tuần 9 | ⬜ |
| | [3.2 Playbook & SOAR](m3-incident-response/3.2-playbook-soar.md) | Tuần 10 | ⬜ |
| | [3.3 Giao tiếp, tabletop & postmortem](m3-incident-response/3.3-giao-tiep-tabletop-postmortem.md) | Tuần 11 | ⬜ |
| **[4. Digital Forensics & Malware Analysis](m4-digital-forensics-malware-analysis/README.md)** | 4 chương | Tuần 12–15 | ⬜ |
| | [4.1 Nguyên tắc & Windows artifacts](m4-digital-forensics-malware-analysis/4.1-nguyen-tac-windows-artifacts.md) | Tuần 12 | ⬜ |
| | [4.2 Timeline & Linux forensics](m4-digital-forensics-malware-analysis/4.2-timeline-linux-forensics.md) | Tuần 13 | ⬜ |
| | [4.3 Memory forensics](m4-digital-forensics-malware-analysis/4.3-memory-forensics.md) | Tuần 13 | ⬜ |
| | [4.4 Malware analysis cơ bản](m4-digital-forensics-malware-analysis/4.4-malware-analysis-co-ban.md) | Tuần 14–15 | ⬜ |
| **[5. Threat Hunting & Network Security Monitoring](m5-threat-hunting-network-security-monitoring/README.md)** | 3 chương | Tuần 16–17 | ⬜ |
| | [5.1 Phương pháp hunting](m5-threat-hunting-network-security-monitoring/5.1-phuong-phap-hunting.md) | Tuần 16 | ⬜ |
| | [5.2 Network Security Monitoring](m5-threat-hunting-network-security-monitoring/5.2-network-security-monitoring.md) | Tuần 17 | ⬜ |
| | [5.3 Threat Intelligence cho SOC](m5-threat-hunting-network-security-monitoring/5.3-threat-intelligence-cho-soc.md) | Tuần 17 | ⬜ |

## Gate — tiêu chí để đi tiếp

> Chỉ chuyển giai đoạn khi **tất cả** ô được tick **và** có bằng chứng (link tới file/commit/ảnh).

- [ ] Triển khai Wazuh hoặc ELK + Sysmon trong home lab, thu log từ 3 máy
- [ ] Viết 10 Sigma rule, test bằng Atomic Red Team, ghi lại kết quả detect/miss
- [ ] Viết 3 IR playbook và 1 postmortem cho một sự cố giả lập
- [ ] Hoàn thành 10 challenge trên CyberDefenders/BTLO
- [ ] (Tuỳ chọn) Chứng chỉ BTL1, CySA+ hoặc TryHackMe SAL1

## Sản phẩm của giai đoạn (deliverables)

- [Sổ Sigma rules (≥ 10)](san-pham/sigma-rules-log.md)
- [Bộ IR playbook (≥ 3) + postmortem (≥ 1)](san-pham/ir-playbooks.md)
- [Triển khai Wazuh/ELK + Sysmon (3 máy)](san-pham/wazuh-elk-sysmon-lab.md)
- [Theo dõi challenge CyberDefenders/BTLO/LetsDefend (≥ 10)](san-pham/theo-doi-challenge.md)

## Nguồn học gợi ý

- TryHackMe SOC Level 1 / 2, Blue Team Labs Online, CyberDefenders, LetsDefend
- Splunk Boss of the SOC (BOTS), Detection Lab / GOAD
- SANS DFIR posters & cheat sheets, The DFIR Report

## Nhật ký giai đoạn

| Tuần | Làm được gì | Vướng ở đâu | Việc tuần sau |
| --- | --- | --- | --- |
|  |  |  |  |

## Tổng kết cuối giai đoạn (viết khi đạt gate)

- Điều mình hiểu sâu nhất: …
- Điều còn yếu cần quay lại: …
- Ngày đạt gate: ____/____/____
