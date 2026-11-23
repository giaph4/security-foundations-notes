# Giai đoạn 4: Tấn công — Red Team & Pentest

> **Thời lượng:** 4–5 tháng · **Trọng tâm:** Pentest web/network/AD
> **Trạng thái giai đoạn:** ⬜ Chưa bắt đầu · 🟨 Đang học · ✅ Đạt gate

📖 Giáo trình chi tiết: [Giáo trình Giai đoạn 4 Tấn công — Red Team & Pentest (bản chi tiết)](../giao-trinh/Gi%C3%A1o%20tr%C3%ACnh%20Giai%20%C4%91o%E1%BA%A1n%204%20T%E1%BA%A5n%20c%C3%B4ng%20%E2%80%94%20Red%20Team%20%26%20Pentest%20%28b%E1%BA%A3n%20chi%20ti%E1%BA%BFt%29.md)
🗺 Roadmap tổng: [Roadmap An ninh mạng & An toàn thông tin](../roadmap/Roadmap%20An%20ninh%20m%E1%BA%A1ng%20%26%20An%20to%C3%A0n%20th%C3%B4ng%20tin.md)

> Mục đích không phải "hack" mà là **chứng minh rủi ro thật bằng bằng chứng, rồi đề xuất khắc phục**.


> ⚠️ **CHỈ thực hành trên lab của bản thân hoặc nền tảng được phép.** Tấn công hệ thống không được ủy quyền là vi phạm pháp luật. Đọc [đạo đức & pháp lý](../00-bat-dau/dao-duc-phap-ly.md) trước mỗi buổi lab.

## Bản đồ module & chương

| Module | Chương | Thời gian | Trạng thái |
| --- | --- | --- | --- |
| **[1. Quy trình pentest, Recon & Enumeration](m1-quy-trinh-pentest-recon-enumeration/README.md)** | 3 chương | Tuần 1–2 | ⬜ |
| | [1.1 Phương pháp luận](m1-quy-trinh-pentest-recon-enumeration/1.1-phuong-phap-luan.md) | Tuần 1 | ⬜ |
| | [1.2 Passive recon / OSINT](m1-quy-trinh-pentest-recon-enumeration/1.2-passive-recon-osint.md) | Tuần 1 | ⬜ |
| | [1.3 Active recon & enumeration](m1-quy-trinh-pentest-recon-enumeration/1.3-active-recon-enumeration.md) | Tuần 2 | ⬜ |
| **[2. Web Application & API Security](m2-web-application-api-security/README.md)** | 4 chương | Tuần 3–8 | ⬜ |
| | [2.1 Nền tảng HTTP & Burp Suite](m2-web-application-api-security/2.1-nen-tang-http-burp-suite.md) | Tuần 3 | ⬜ |
| | [2.2 Injection & XSS](m2-web-application-api-security/2.2-injection-xss.md) | Tuần 4–5 | ⬜ |
| | [2.3 Access control, SSRF, file & logic](m2-web-application-api-security/2.3-access-control-ssrf-file-logic.md) | Tuần 6–7 | ⬜ |
| | [2.4 API Security](m2-web-application-api-security/2.4-api-security.md) | Tuần 8 | ⬜ |
| **[3. Network, Privilege Escalation & Active Directory](m3-network-privilege-escalation-active-directory/README.md)** | 4 chương | Tuần 9–14 | ⬜ |
| | [3.1 Foothold & shell](m3-network-privilege-escalation-active-directory/3.1-foothold-shell.md) | Tuần 9 | ⬜ |
| | [3.2 Linux Privilege Escalation](m3-network-privilege-escalation-active-directory/3.2-linux-privilege-escalation.md) | Tuần 10 | ⬜ |
| | [3.3 Windows Privilege Escalation](m3-network-privilege-escalation-active-directory/3.3-windows-privilege-escalation.md) | Tuần 11 | ⬜ |
| | [3.4 Pivoting & Active Directory attacks](m3-network-privilege-escalation-active-directory/3.4-pivoting-active-directory-attacks.md) | Tuần 12–14 | ⬜ |
| **[4. Mở rộng: chọn 1 nhánh](m4-mo-rong-chon-1-nhanh/README.md)** | 1 chương | Tuần 15–16 | ⬜ |
| | [4.0 Chọn nhánh mở rộng (Mobile / Wireless & Social / Exploit dev & RE)](m4-mo-rong-chon-1-nhanh/4.0-chon-nhanh-mo-rong-mobile-wireless-social-exploi.md) | Tuần 15–16 | ⬜ |
| **[5. Reporting & giao tiếp](m5-reporting-giao-tiep/README.md)** | 3 chương | Tuần 17 | ⬜ |
| | [5.1 Cấu trúc báo cáo](m5-reporting-giao-tiep/5.1-cau-truc-bao-cao.md) | Tuần 17 | ⬜ |
| | [5.2 Viết finding tốt](m5-reporting-giao-tiep/5.2-viet-finding-tot.md) | Tuần 17 | ⬜ |
| | [5.3 Giao tiếp trong engagement](m5-reporting-giao-tiep/5.3-giao-tiep-trong-engagement.md) | Tuần 17 | ⬜ |

## Gate — tiêu chí để đi tiếp

> Chỉ chuyển giai đoạn khi **tất cả** ô được tick **và** có bằng chứng (link tới file/commit/ảnh).

- [ ] Hoàn thành toàn bộ lab Apprentice + Practitioner của PortSwigger cho 8 nhóm lỗ hổng chính
- [ ] Root 30+ máy HTB/THM (ít nhất 10 Windows/AD)
- [ ] Pentest trọn vẹn 1 đồ án của bản thân và viết báo cáo 15–25 trang
- [ ] (Tuỳ chọn) eJPT → PNPT/CPTS → OSCP

## Sản phẩm của giai đoạn (deliverables)

- [PortSwigger — 8 nhóm lỗ hổng chính](san-pham/portswigger-tracker.md)
- [Root 30+ máy (≥ 10 Windows/AD)](san-pham/theo-doi-may-htb-thm.md)
- [Báo cáo pentest 15–25 trang cho đồ án của bản thân](san-pham/bao-cao-pentest-do-an.md)
- [(Tuỳ chọn) eJPT → PNPT/CPTS → OSCP](san-pham/chung-chi-pentest.md)

## Nguồn học gợi ý

- **PortSwigger Web Security Academy** (miễn phí)
- Hack The Box (Academy + Labs), TryHackMe Jr Penetration Tester, VulnHub, GOAD
- OWASP Juice Shop, DVWA; *The Web Application Hacker's Handbook*, HackTricks
- Bug bounty: HackerOne, Bugcrowd, Intigriti — đọc policy trước khi test

## Nhật ký giai đoạn

| Tuần | Làm được gì | Vướng ở đâu | Việc tuần sau |
| --- | --- | --- | --- |
|  |  |  |  |

## Tổng kết cuối giai đoạn (viết khi đạt gate)

- Điều mình hiểu sâu nhất: …
- Điều còn yếu cần quay lại: …
- Ngày đạt gate: ____/____/____
