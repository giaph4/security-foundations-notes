# Giai đoạn 2: Security Foundations & Quản trị rủi ro

> **Thời lượng:** 2–3 tháng · **Trọng tâm:** Crypto, IAM, risk, threat modeling
> **Trạng thái giai đoạn:** ⬜ Chưa bắt đầu · 🟨 Đang học · ✅ Đạt gate

📖 Giáo trình chi tiết: [Giáo trình Giai đoạn 2 Security Foundations & Quản trị rủi ro (bản chi tiết)](../giao-trinh/Gi%C3%A1o%20tr%C3%ACnh%20Giai%20%C4%91o%E1%BA%A1n%202%20Security%20Foundations%20%26%20Qu%E1%BA%A3n%20tr%E1%BB%8B%20r%E1%BB%A7i%20ro%20%28b%E1%BA%A3n%20chi%20ti%E1%BA%BFt%29.md)
🗺 Roadmap tổng: [Roadmap An ninh mạng & An toàn thông tin](../roadmap/Roadmap%20An%20ninh%20m%E1%BA%A1ng%20%26%20An%20to%C3%A0n%20th%C3%B4ng%20tin.md)

> Giai đoạn hình thành năng lực **đánh giá rủi ro** — phân biệt người làm bảo mật có trách nhiệm với người chỉ biết dùng tool.


## Bản đồ module & chương

| Module | Chương | Thời gian | Trạng thái |
| --- | --- | --- | --- |
| **[1. Cryptography & PKI](m1-cryptography-pki/README.md)** | 3 chương | Tuần 1–2 | ⬜ |
| | [1.1 Các khối cơ bản](m1-cryptography-pki/1.1-cac-khoi-co-ban.md) | Tuần 1 | ⬜ |
| | [1.2 Chữ ký số, PKI & TLS](m1-cryptography-pki/1.2-chu-ky-so-pki-tls.md) | Tuần 1–2 | ⬜ |
| | [1.3 Crypto trong ứng dụng](m1-cryptography-pki/1.3-crypto-trong-ung-dung.md) | Tuần 2 | ⬜ |
| **[2. Identity & Access Management](m2-identity-access-management/README.md)** | 4 chương | Tuần 3–4 | ⬜ |
| | [2.1 Authentication & session](m2-identity-access-management/2.1-authentication-session.md) | Tuần 3 | ⬜ |
| | [2.2 Authorization](m2-identity-access-management/2.2-authorization.md) | Tuần 3 | ⬜ |
| | [2.3 Federation: OAuth 2.0, OIDC, SAML](m2-identity-access-management/2.3-federation-oauth-2-0-oidc-saml.md) | Tuần 4 | ⬜ |
| | [2.4 IAM doanh nghiệp & Zero Trust](m2-identity-access-management/2.4-iam-doanh-nghiep-zero-trust.md) | Tuần 4 | ⬜ |
| **[3. Threat Landscape & Vulnerability Management](m3-threat-landscape-vulnerability-management/README.md)** | 3 chương | Tuần 5–6 | ⬜ |
| | [3.1 Tác nhân đe dọa & kỹ thuật tấn công](m3-threat-landscape-vulnerability-management/3.1-tac-nhan-de-doa-ky-thuat-tan-cong.md) | Tuần 5 | ⬜ |
| | [3.2 Security controls](m3-threat-landscape-vulnerability-management/3.2-security-controls.md) | Tuần 5 | ⬜ |
| | [3.3 Vulnerability Management](m3-threat-landscape-vulnerability-management/3.3-vulnerability-management.md) | Tuần 6 | ⬜ |
| **[4. Quản trị rủi ro & Framework](m4-quan-tri-rui-ro-framework/README.md)** | 5 chương | Tuần 7–8 | ⬜ |
| | [4.1 Thuật ngữ & quy trình rủi ro](m4-quan-tri-rui-ro-framework/4.1-thuat-ngu-quy-trinh-rui-ro.md) | Tuần 7 | ⬜ |
| | [4.2 Định tính vs định lượng](m4-quan-tri-rui-ro-framework/4.2-dinh-tinh-vs-dinh-luong.md) | Tuần 7 | ⬜ |
| | [4.3 Framework & chuẩn](m4-quan-tri-rui-ro-framework/4.3-framework-chuan.md) | Tuần 8 | ⬜ |
| | [4.4 Pháp lý & tuân thủ tại Việt Nam](m4-quan-tri-rui-ro-framework/4.4-phap-ly-tuan-thu-tai-viet-nam.md) | Tuần 8 | ⬜ |
| | [4.5 Policy & giao tiếp rủi ro](m4-quan-tri-rui-ro-framework/4.5-policy-giao-tiep-rui-ro.md) | Tuần 8 | ⬜ |
| **[5. Threat Modeling](m5-threat-modeling/README.md)** | 3 chương | Tuần 9 | ⬜ |
| | [5.1 Data Flow Diagram](m5-threat-modeling/5.1-data-flow-diagram.md) | Tuần 9 | ⬜ |
| | [5.2 STRIDE](m5-threat-modeling/5.2-stride.md) | Tuần 9 | ⬜ |
| | [5.3 Phương pháp khác & quy trình buổi họp](m5-threat-modeling/5.3-phuong-phap-khac-quy-trinh-buoi-hop.md) | Tuần 9 | ⬜ |

## Gate — tiêu chí để đi tiếp

> Chỉ chuyển giai đoạn khi **tất cả** ô được tick **và** có bằng chứng (link tới file/commit/ảnh).

- [ ] Viết risk register 15–20 rủi ro cho 1 đồ án của bản thân
- [ ] Threat model STRIDE có DFD cho cùng hệ thống đó
- [ ] Map được 10 control CIS vào các rủi ro đã xác định
- [ ] (Tuỳ chọn) Thi CompTIA Security+

## Sản phẩm của giai đoạn (deliverables)

- [Risk register (15–20 rủi ro)](san-pham/risk-register.md)
- [Threat model STRIDE + DFD](san-pham/threat-model-stride.md)
- [Map 10 CIS Control vào rủi ro](san-pham/map-cis-controls.md)
- [(Tuỳ chọn) Kế hoạch thi Security+](san-pham/on-thi-security-plus.md)

## Nguồn học gợi ý

- Professor Messer Security+ (miễn phí), *Threat Modeling: Designing for Security* (Adam Shostack)
- Tài liệu NIST CSF 2.0 và CIS Controls (miễn phí)

## Nhật ký giai đoạn

| Tuần | Làm được gì | Vướng ở đâu | Việc tuần sau |
| --- | --- | --- | --- |
|  |  |  |  |

## Tổng kết cuối giai đoạn (viết khi đạt gate)

- Điều mình hiểu sâu nhất: …
- Điều còn yếu cần quay lại: …
- Ngày đạt gate: ____/____/____
