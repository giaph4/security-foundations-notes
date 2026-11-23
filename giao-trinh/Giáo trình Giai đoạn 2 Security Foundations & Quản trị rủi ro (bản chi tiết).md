# Giáo trình Giai đoạn 2: Security Foundations & Quản trị rủi ro (bản chi tiết)

Nov 23, 2026 · @Huynh Gia Pho

Bảo mật không phải là chặn mọi thứ, mà là biết bảo vệ cái gì trước và vì sao. Giáo trình này dẫn bạn qua 5 module trong 10 tuần, mỗi chương gồm lý thuyết, video, tài liệu đọc, lab và tiêu chí đạt.

## Cách dùng giáo trình

Học 12–15 giờ/tuần trong 10 tuần; mỗi chương theo vòng **Xem video → Đọc tài liệu → Làm lab → Ghi chú → Tự kiểm tra**. Giai đoạn này có nhiều sản phẩm dạng tài liệu (risk register, threat model, policy) — kỹ năng mà người chịu trách nhiệm bảo vệ hệ thống dùng hằng ngày.

Video xuyên suốt giai đoạn: [Professor Messer — CompTIA SY0-701 Security+ Training Course](https://www.professormesser.com/security-plus/sy0-701/sy0-701-video/sy0-701-comptia-security-plus-course/) (121 video, khoảng 15 giờ, miễn phí; [playlist YouTube](https://www.youtube.com/playlist?list=PLG49S3nxzAnl4QDVqK-hOnoqcSKEIDDuv)). Các mục Messer trong giáo trình ghi theo số objective của đề SY0-701 (ví dụ 1.4 = Cryptographic Solutions).

### Mục tiêu đầu ra

Kết thúc giai đoạn, bạn phải làm được:

1. Chọn đúng thuật toán mã hóa / băm / ký cho từng tình huống và chỉ ra lỗi crypto phổ biến trong code
2. Thiết kế xác thực + phân quyền cho một ứng dụng web (MFA, OAuth 2.0/OIDC, RBAC)
3. Đánh giá một CVE mới bằng CVSS, EPSS, CISA KEV và quyết định mức ưu tiên vá
4. Lập risk register theo NIST SP 800-30 / ISO 27005 và trình bày cho người không chuyên
5. Map control theo NIST CSF 2.0 và CIS Controls v8
6. Threat model một hệ thống bằng STRIDE + DFD

### Cấu trúc

| Module | Tuần | Nội dung chính | Sản phẩm nộp |
| --- | --- | --- | --- |
| 1. Cryptography & PKI | 1–2 | Symmetric, asymmetric, hash, password hashing, signature, PKI, TLS | Lab OpenSSL + báo cáo crypto review 1 repo |
| 2. IAM | 3–4 | Authentication, MFA, session, OAuth/OIDC/SAML, RBAC/ABAC, Zero Trust | Tài liệu thiết kế IAM + lab Keycloak |
| 3. Threat & Vulnerability | 5–6 | Tác nhân đe dọa, malware, ATT&CK, control, CVE/CVSS/EPSS/KEV | Vulnerability report có ưu tiên |
| 4. Risk & Framework | 7–8 | Quy trình rủi ro, ALE, FAIR, NIST CSF, ISO 27001, CIS, pháp lý VN, policy | Risk register 20 dòng + báo cáo lãnh đạo |
| 5. Threat Modeling | 9 | DFD, STRIDE, attack tree, PASTA | Threat model |
| Kiểm tra | 10 | Capstone | Báo cáo đánh giá an toàn 1 hệ thống |

### Quy ước ghi chú

- Tiếp tục repo `security-foundations-notes`, thêm thư mục `phase-2/` với mỗi chương một file Markdown
- Anki: thuật toán nên/không nên dùng, thuật ngữ rủi ro, 6 function NIST CSF, STRIDE
- Mỗi lab ghi theo mẫu: Mục tiêu → Môi trường → Các bước → Kết quả → Ý nghĩa bảo mật

### Cột "Góc nhìn bảo mật"

Mỗi module kết thúc bằng phần này: kẻ tấn công lạm dụng kiến thức đó ra sao và người phòng thủ kiểm soát ở đâu — cầu nối sang Giai đoạn 3 (Blue Team) và 4 (Red Team).

## Module 1 — Cryptography & PKI (Tuần 1–2)

Mục tiêu không phải chứng minh toán học mà là **dùng đúng** và **nhận ra dùng sai**. Video chính: Professor Messer SY0-701 mục 1.4; nâng cao: [Coursera — Cryptography I (Dan Boneh)](https://www.coursera.org/learn/crypto) (audit miễn phí).

### Chương 1.1 — Các khối cơ bản (Tuần 1)

**Lý thuyết cần nắm**

| Khối | Nên dùng | Không nên dùng | Dùng cho |
| --- | --- | --- | --- |
| Symmetric | AES-256-GCM, ChaCha20-Poly1305 | DES, 3DES, RC4, AES-ECB | Mã hóa dữ liệu, disk, TLS |
| Asymmetric | RSA ≥ 3072, ECDH/ECDSA P-256, X25519/Ed25519 | RSA 1024, PKCS#1 v1.5 cho mã hóa | Trao đổi khóa, chữ ký |
| Hash | SHA-256, SHA-3, BLAKE2 | MD5, SHA-1 | Integrity, fingerprint |
| Password hashing | Argon2id, scrypt, bcrypt | SHA-256 không salt, MD5 | Lưu mật khẩu |
| MAC | HMAC-SHA256 | Tự ghép `hash(key + msg)` | Xác thực thông điệp, webhook |
| Random | CSPRNG (`secrets`, `SecureRandom`) | `random`, `Math.random()` | Token, IV, khóa |

- Key, IV/nonce (không lặp với GCM), salt, pepper, AEAD, forward secrecy
- Encoding ≠ encryption: Base64, hex không bảo vệ gì
- Post-Quantum Cryptography: ML-KEM (FIPS 203), ML-DSA (FIPS 204); "harvest now, decrypt later", crypto agility

**Video**: Messer SY0-701 1.4 (Encrypting Data, Key Exchange, Encryption Technologies, Hashing and Digital Signatures); [Computerphile — Public Key Cryptography](https://www.youtube.com/watch?v=GSIDS_lvRv4)

**Đọc**: [OWASP Cryptographic Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html), [OWASP Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html); sách *Serious Cryptography* (2nd ed., Jean-Philippe Aumasson) chương 1–4

**Lab**:

1. `openssl enc -aes-256-ecb` và `-aes-256-cbc` mã hóa một ảnh BMP, so sánh để thấy ECB lộ mẫu
2. [Hashcat](https://hashcat.net/hashcat/) trên lab: crack 10 hash MD5 vs 10 hash bcrypt từ wordlist, ghi thời gian
3. [CryptoHack](https://cryptohack.org/): hoàn thành mục Introduction + General

### Chương 1.2 — Chữ ký số, PKI & TLS (Tuần 1–2)

**Lý thuyết cần nắm**

- Chữ ký số: ký bằng private key, kiểm bằng public key → integrity + authenticity + non-repudiation
- X.509: subject, issuer, SAN, validity, key usage; chain Root CA → Intermediate → Leaf
- Thu hồi: CRL, OCSP, OCSP stapling; Certificate Transparency ([crt.sh](https://crt.sh/))
- TLS 1.3 handshake: ClientHello (key share) → ServerHello → Certificate → Finished
- Lỗi thực tế: tắt verify certificate trong code, cert hết hạn, private key trong repo, self-signed trên production

**Video**: Messer SY0-701 1.4 (Certificates, Public Key Infrastructure); [Cloudflare — What happens in a TLS handshake?](https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/) (bài đọc có hình minh họa)

**Đọc**: [The Illustrated TLS 1.3 Connection](https://tls13.xargs.org/) (giải thích từng byte)

**Lab**:

1. OpenSSL: tạo CA riêng, ký certificate cho web server trong DMZ lab, cấu hình Nginx HTTPS, kiểm tra bằng `openssl s_client -connect host:443 -showcerts`
2. Quét TLS domain của bạn bằng [testssl.sh](https://testssl.sh/) hoặc [SSL Labs](https://www.ssllabs.com/ssltest/), giải thích từng cảnh báo
3. Tra crt.sh một domain lớn, quan sát các subdomain lộ qua Certificate Transparency

### Chương 1.3 — Crypto trong ứng dụng (Tuần 2)

**Lý thuyết cần nắm**

- Quản lý khóa: KMS, HSM, Vault; envelope encryption; key rotation
- JWT: `alg: none`, nhầm HS256/RS256, không kiểm `exp`, payload chỉ là base64
- Java: `javax.crypto`, `KeyStore`; tránh `Cipher.getInstance("AES")` (nhiều provider mặc định ECB)

**Ví dụ Python — AEAD và băm mật khẩu đúng cách:**

```python
import os
from cryptography.hazmat.primitives.ciphers.aead import AESGCM
from cryptography.exceptions import InvalidTag
from argon2 import PasswordHasher
from argon2.exceptions import VerifyMismatchError

# AES-256-GCM: mỗi lần mã hóa dùng nonce mới 12 byte
key = AESGCM.generate_key(bit_length=256)
aesgcm = AESGCM(key)
nonce = os.urandom(12)
ct = aesgcm.encrypt(nonce, b"secret data", b"user-id:42")  # AAD gắn ngữ cảnh
try:
    pt = aesgcm.decrypt(nonce, ct, b"user-id:42")
except InvalidTag:
    # Sai key/AAD hoặc dữ liệu bị sửa -> từ chối, không cố "sửa" dữ liệu
    raise

# Argon2id cho mật khẩu
ph = PasswordHasher()
stored = ph.hash("P@ssw0rd-example")
try:
    ph.verify(stored, "wrong-password")
except VerifyMismatchError:
    print("Sai mật khẩu")  # Không tiết lộ chi tiết cho người dùng
```

**Đọc**: [OWASP Key Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Key_Management_Cheat_Sheet.html), [OWASP JSON Web Token Cheat Sheet for Java](https://cheatsheetseries.owasp.org/cheatsheets/JSON_Web_Token_for_Java_Cheat_Sheet.html), [NIST Post-Quantum Cryptography](https://csrc.nist.gov/projects/post-quantum-cryptography)

**Lab**: Crypto review một đồ án Java của bạn — liệt kê mọi chỗ lưu mật khẩu, token, khóa, kết nối TLS và đánh giá đúng/sai theo bảng ở Chương 1.1.

### Góc nhìn bảo mật — Module 1

- Kẻ tấn công hiếm khi phá thuật toán; họ khai thác cách dùng sai: khóa lộ, nonce lặp, hash yếu, verify bị tắt, downgrade
- Người phòng thủ: dùng thư viện cấp cao, không tự viết crypto, secret scanning, inventory certificate + cảnh báo hết hạn

### Tiêu chí đạt Module 1

- [ ] Giải thích encoding / hashing / encryption / signing bằng ví dụ
- [ ] Web server lab chạy HTTPS bằng CA tự tạo, client tin cậy đúng chain
- [ ] Báo cáo crypto review 1 repo với ≥ 5 phát hiện + cách sửa
- [ ] Hoàn thành 2 mục đầu CryptoHack

## Module 2 — Identity & Access Management (Tuần 3–4)

Danh tính là "chu vi mới": phần lớn vụ xâm nhập bắt đầu từ credential bị lộ hoặc quyền quá rộng. Video chính: Messer SY0-701 mục 4.6 (Identity and Access Management, Access Controls, Multifactor Authentication, Password Security).

### Chương 2.1 — Authentication & session (Tuần 3)

**Lý thuyết cần nắm**

- Yếu tố: know / have / are; độ mạnh MFA: SMS < TOTP < push có number matching < **FIDO2/WebAuthn (passkey)** — chống phishing
- Chính sách mật khẩu theo NIST SP 800-63B: độ dài tối thiểu, chặn mật khẩu đã lộ, không ép đổi định kỳ vô cớ
- Tấn công: credential stuffing, password spraying, MFA fatigue, adversary-in-the-middle phishing, SIM swap, session token theft
- Session: cookie `HttpOnly`, `Secure`, `SameSite`; timeout; đổi session ID sau login

**Video**: Messer SY0-701 4.6 (Multifactor Authentication, Password Security)

**Đọc**: [NIST SP 800-63B](https://pages.nist.gov/800-63-4/sp800-63b.html), [OWASP Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html), [OWASP Session Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html), [passkeys.dev](https://passkeys.dev/)

**Lab**: [PortSwigger Web Security Academy — Authentication](https://portswigger.net/web-security/authentication) (lab mức Apprentice); dùng DevTools kiểm tra cookie attribute của 3 website bạn dùng.

### Chương 2.2 — Authorization (Tuần 3)

**Lý thuyết cần nắm**

- Mô hình: DAC, MAC, **RBAC**, **ABAC**, ReBAC ([OpenFGA](https://openfga.dev/))
- Least privilege, separation of duties, need-to-know, just-in-time access
- Lỗi kinh điển: IDOR/BOLA, kiểm tra quyền chỉ ở frontend, leo thang quyền ngang/dọc

**Đọc**: [OWASP Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html)

**Lab**: [PortSwigger — Access control vulnerabilities](https://portswigger.net/web-security/access-control) (lab Apprentice); vẽ ma trận quyền (role × chức năng) cho 1 đồ án của bạn.

### Chương 2.3 — Federation: OAuth 2.0, OIDC, SAML (Tuần 4)

**Lý thuyết cần nắm**

| Chuẩn | Mục đích | Token | Dùng khi |
| --- | --- | --- | --- |
| OAuth 2.0 | **Ủy quyền** truy cập API | Access token, refresh token | App gọi API thay mặt user |
| OpenID Connect | **Xác thực** trên nền OAuth | ID token (JWT) | "Đăng nhập bằng Google", SSO hiện đại |
| SAML 2.0 | SSO doanh nghiệp | Assertion XML có chữ ký | Ứng dụng enterprise, Entra ID/Okta |
| Kerberos | SSO nội bộ AD | TGT, service ticket | Windows domain |

- Luồng nên dùng: **Authorization Code + PKCE** (web, mobile, SPA); Client Credentials (service-to-service). Tránh Implicit và Resource Owner Password
- Lỗi hay gặp: `redirect_uri` không kiểm chặt, thiếu `state`, token trong localStorage, scope quá rộng, không kiểm `aud`/`iss`

**Video**: [OAuth 2.0 and OpenID Connect (in plain English) — Nate Barbettini, Okta](https://classcentral.com/classroom/youtube-oauth-2-0-and-openid-connect-in-plain-english-211239) (slide: [Speaker Deck](https://speakerdeck.com/nbarbettini/oauth-and-openid-connect-in-plain-english))

**Đọc**: [RFC 9700 — OAuth 2.0 Security Best Current Practice](https://datatracker.ietf.org/doc/rfc9700/), [oauth.net/2](https://oauth.net/2/), [OWASP OAuth 2.0 Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/OAuth2_Cheat_Sheet.html)

**Lab**:

1. Chạy [Keycloak](https://www.keycloak.org/getting-started/getting-started-docker) bằng Docker, tạo realm, 2 role (user, admin), bật TOTP
2. Tích hợp 1 app Spring Boot với Keycloak qua OIDC ([Spring Security OAuth2 Login](https://docs.spring.io/spring-security/reference/servlet/oauth2/login/index.html)), bảo vệ endpoint theo role
3. Quan sát toàn bộ luồng redirect bằng DevTools/Burp, decode ID token trên [jwt.io](https://jwt.io/), kiểm `iss`, `aud`, `exp`
4. [PortSwigger — OAuth authentication](https://portswigger.net/web-security/oauth) (lab Apprentice)

### Chương 2.4 — IAM doanh nghiệp & Zero Trust (Tuần 4)

**Lý thuyết cần nắm**

- Identity lifecycle: joiner – mover – leaver; access review định kỳ
- Directory: Active Directory, Microsoft Entra ID; SCIM provisioning
- PAM: vault mật khẩu admin, session recording, break-glass account; secret cho app: [HashiCorp Vault](https://developer.hashicorp.com/vault/tutorials)
- Zero Trust: xác minh mọi request theo danh tính + thiết bị + ngữ cảnh

**Video**: Messer SY0-701 1.2 (Zero Trust)

**Đọc**: [NIST SP 800-207 — Zero Trust Architecture](https://csrc.nist.gov/pubs/sp/800/207/final)

**Lab**: AD lab — cấu hình Fine-Grained Password Policy cho nhóm admin và [Windows LAPS](https://learn.microsoft.com/windows-server/identity/laps/laps-overview) cho máy trạm; viết quy trình offboarding nhân viên 10 bước.

### Góc nhìn bảo mật — Module 2

- Kẻ tấn công: phishing lấy session, password spraying, lạm dụng OAuth consent (app độc xin quyền), tài khoản nghỉ việc chưa khóa
- Người phòng thủ: phishing-resistant MFA cho nhóm rủi ro cao, Conditional Access, giám sát sign-in log, access review, least privilege

### Tiêu chí đạt Module 2

- [ ] Vẽ luồng Authorization Code + PKCE và giải thích `state`, `code_verifier`
- [ ] App mẫu đăng nhập qua Keycloak có MFA và RBAC
- [ ] Tài liệu thiết kế IAM (2–3 trang) cho 1 đồ án: loại tài khoản, role, ma trận quyền, chính sách mật khẩu/MFA, vòng đời tài khoản

## Module 3 — Threat Landscape & Vulnerability Management (Tuần 5–6)

Biết kẻ địch là ai, họ dùng gì, và lỗ hổng nào cần vá trước — nền tảng cho khả năng phản ứng linh hoạt trước mối đe dọa mới. Video chính: Messer SY0-701 mục 2.1–2.5 và 4.3.

### Chương 3.1 — Tác nhân đe dọa & kỹ thuật tấn công (Tuần 5)

**Lý thuyết cần nắm**

| Tác nhân | Động cơ | Năng lực | Ví dụ hành vi |
| --- | --- | --- | --- |
| Ransomware gang | Tiền | Trung bình–cao, mô hình RaaS | Double extortion, mua quyền truy cập từ initial access broker |
| APT | Gián điệp, phá hoại | Rất cao | Zero-day, supply chain, tiềm ẩn lâu |
| Hacktivist | Chính trị | Thấp–trung bình | DDoS, deface, leak |
| Insider | Tiền, bất mãn, sơ suất | Có sẵn quyền | Tuồn dữ liệu |
| Opportunistic | Tò mò, danh tiếng | Thấp | Quét hàng loạt lỗ hổng công khai |

- Malware: ransomware, infostealer, RAT, loader, botnet, rootkit, wiper
- Social engineering: phishing, BEC, vishing, deepfake, QR phishing
- Supply chain: typosquatting npm/PyPI, CI/CD bị chiếm, nhà cung cấp bị xâm nhập
- **Cyber Kill Chain** (7 bước) và **MITRE ATT&CK** (14 tactic Enterprise)

**Video**: Messer SY0-701 2.1 (Threat Actors), 2.2 (Phishing, Impersonation), 2.4 (An Overview of Malware, Other Malware Types)

**Đọc**: [MITRE ATT&CK — Getting Started](https://attack.mitre.org/resources/), [Lockheed Martin — Cyber Kill Chain](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html), [CISA #StopRansomware Guide](https://www.cisa.gov/stopransomware/ransomware-guide)

**Lab**: [MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/) — tô các technique của 1 nhóm ransomware từ một [CISA advisory](https://www.cisa.gov/news-events/cybersecurity-advisories); tham khảo hướng dẫn trong [ATT&CK CTI Training](https://attack.mitre.org/resources/learn-more-about-attack/training/cti/).

### Chương 3.2 — Security controls (Tuần 5)

**Lý thuyết cần nắm**

| Theo chức năng | Ví dụ |
| --- | --- |
| Preventive | Firewall, MFA, patch, hardening |
| Detective | SIEM, IDS, audit log, EDR alert |
| Corrective | Restore backup, cách ly máy, reset credential |
| Deterrent | Banner cảnh báo, chính sách kỷ luật |
| Compensating | WAF virtual patch khi chưa vá được |

Theo loại: administrative (policy, đào tạo), technical (cấu hình, phần mềm), physical (khóa, camera).

**Video**: Messer SY0-701 1.1 (Security Controls)

**Đọc**: [MITRE D3FEND](https://d3fend.mitre.org/) — bản đồ kỹ thuật phòng thủ tương ứng với ATT&CK

**Lab**: Với mỗi technique trong ATT&CK layer ở Chương 3.1, gán 1 control preventive + 1 detective.

### Chương 3.3 — Vulnerability Management (Tuần 6)

**Lý thuyết cần nắm**

- Vòng đời: Discover asset → Scan → Prioritize → Remediate → Verify → Report
- **CVE** (định danh), **CWE** (loại lỗi), **CVSS v3.1/v4.0** (mức độ kỹ thuật), **EPSS** (xác suất bị khai thác 30 ngày tới), **CISA KEV** (đã bị khai thác thực tế)
- Ưu tiên thực tế = CVSS × mức độ lộ diện × giá trị tài sản × có trong KEV / EPSS cao
- SLA mẫu: KEV hoặc Critical Internet-facing ≤ 72 giờ; High ≤ 14 ngày; Medium ≤ 30 ngày
- Ngoại lệ: compensating control + risk acceptance có người ký + ngày xem xét lại

**So sánh cách ưu tiên**: chỉ theo CVSS dễ làm nhưng tạo hàng nghìn việc "Critical"; kết hợp EPSS + KEV + ngữ cảnh tài sản giảm khối lượng mạnh nhưng cần asset inventory tốt.

**Video**: Messer SY0-701 4.3 (Identifying Vulnerabilities, Analyzing Vulnerabilities, Vulnerability Remediation)

**Đọc**: [FIRST CVSS v4.0](https://www.first.org/cvss/), [FIRST EPSS](https://www.first.org/epss/), [CISA KEV Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog), [NVD](https://nvd.nist.gov/), [CWE Top 25](https://cwe.mitre.org/top25/)

**Lab**:

1. Cài [Greenbone Community Edition](https://greenbone.github.io/docs/latest/) (Docker), quét toàn bộ home lab
2. Với 10 phát hiện cao nhất: tra NVD, EPSS, KEV; lập bảng ưu tiên
3. Vá 3 lỗi, quét lại xác minh
4. [Trivy](https://trivy.dev/) quét image Docker của DVWA/Juice Shop và một đồ án của bạn
5. TryHackMe: phòng [Vulnerabilities 101](https://tryhackme.com/room/vulnerabilities101)

### Góc nhìn bảo mật — Module 3

- Kẻ tấn công: khai thác lỗ hổng công khai trong vài giờ sau khi có PoC, nhắm thiết bị biên (VPN, firewall, file transfer)
- Người phòng thủ: asset inventory đầy đủ, ưu tiên theo KEV/EPSS, vá thiết bị biên trước, giám sát dấu hiệu khai thác

### Tiêu chí đạt Module 3

- [ ] Vulnerability report: 10 lỗi với CVSS, EPSS, KEV, độ lộ diện, ưu tiên, SLA, trạng thái
- [ ] ATT&CK layer cho 1 nhóm ransomware kèm 5 control phòng/phát hiện
- [ ] Giải thích vì sao 1 lỗi CVSS 9.8 nội bộ có thể xếp sau 1 lỗi CVSS 7.5 trên Internet có trong KEV

## Module 4 — Quản trị rủi ro & Framework (Tuần 7–8)

Module cốt lõi của vai trò "chịu trách nhiệm bảo vệ hệ thống": biến lỗ hổng kỹ thuật thành quyết định kinh doanh có người chịu trách nhiệm. Video chính: Messer SY0-701 mục 5.1–5.5; video bổ trợ: kênh [Simply Cyber — Gerald Auger](https://www.youtube.com/c/GeraldAuger) (nhiều video miễn phí về GRC).

### Chương 4.1 — Thuật ngữ & quy trình rủi ro (Tuần 7)

**Lý thuyết cần nắm**

- **Asset** → **Threat** khai thác **Vulnerability** → gây **Impact**; **Risk** = Likelihood × Impact
- Inherent risk → Residual risk; risk appetite / tolerance; risk owner
- Quy trình (NIST SP 800-30, ISO/IEC 27005):
  1. Thiết lập bối cảnh: phạm vi, tiêu chí, khẩu vị rủi ro
  2. Nhận diện: asset inventory, threat, vulnerability, control hiện có
  3. Phân tích: ước lượng likelihood và impact
  4. Đánh giá: xếp hạng so với tiêu chí
  5. Xử lý: Mitigate / Transfer / Avoid / Accept
  6. Giám sát & rà soát: KRI, review hàng quý

**Video**: Messer SY0-701 5.2 (Risk Management, Risk Analysis, Risk Management Strategies, Business Impact Analysis)

**Đọc**: [NIST SP 800-30 Rev. 1 — Guide for Conducting Risk Assessments](https://csrc.nist.gov/pubs/sp/800/30/r1/final)

**Lab**: Chọn 1 hệ thống bạn hiểu rõ (đồ án hoặc tổ chức giả định), lập asset inventory 15–20 tài sản với owner và mức độ quan trọng.

### Chương 4.2 — Định tính vs định lượng (Tuần 7)

**Lý thuyết cần nắm**

| Phương pháp | Cách làm | Ưu điểm | Nhược điểm |
| --- | --- | --- | --- |
| Định tính (ma trận 5×5) | Chấm 1–5 likelihood và impact | Nhanh, dễ truyền đạt | Chủ quan, khó so với chi phí |
| Định lượng cổ điển | SLE = AV × EF; ALE = SLE × ARO | Ra số tiền | Cần dữ liệu, dễ tạo ảo giác chính xác |
| FAIR | Loss Event Frequency × Loss Magnitude, mô phỏng Monte Carlo | Khoảng giá trị có căn cứ | Tốn công, cần đào tạo |

**Ví dụ ALE**: server dữ liệu khách hàng trị giá 2 tỷ đồng (AV), ransomware làm mất 40% (EF) → SLE = 800 triệu; tần suất 0,25 lần/năm (ARO) → ALE = 200 triệu/năm. Backup bất biến + EDR giá 60 triệu/năm giảm ARO còn 0,05 → ALE mới 40 triệu → lợi ích ròng 100 triệu/năm.

**Đọc**: [The FAIR Institute — What is FAIR?](https://www.fairinstitute.org/what-is-fair); sách *How to Measure Anything in Cybersecurity Risk* (Douglas Hubbard, Richard Seiersen)

**Lab**: Lập risk register 20 dòng theo mẫu bên dưới; tính ALE cho 3 rủi ro lớn nhất.

### Chương 4.3 — Framework & chuẩn (Tuần 8)

**Lý thuyết cần nắm**

| Framework | Nội dung chính | Link |
| --- | --- | --- |
| NIST CSF 2.0 | 6 function: Govern, Identify, Protect, Detect, Respond, Recover; Profile hiện tại vs mục tiêu | [nist.gov/cyberframework](https://www.nist.gov/cyberframework) |
| ISO/IEC 27001:2022 | ISMS (điều khoản 4–10) + Annex A 93 control, 4 nhóm | [iso.org/standard/27001](https://www.iso.org/standard/27001) |
| ISO/IEC 27005 | Hướng dẫn quản trị rủi ro ATTT | [iso.org](https://www.iso.org/standard/80585.html) |
| NIST SP 800-53 | Thư viện control chi tiết | [csrc.nist.gov](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) |
| CIS Controls v8 | 18 control, Implementation Group IG1–IG3 | [cisecurity.org/controls](https://www.cisecurity.org/controls) |

**Video**: Messer SY0-701 5.1 (Security Policies, Security Standards, Security Procedures, Security Considerations)

**Lab**: Tự đánh giá theo CIS Controls IG1 bằng bảng tính, xác định 10 khoảng trống; map 10 rủi ro vào function NIST CSF 2.0.

### Chương 4.4 — Pháp lý & tuân thủ tại Việt Nam (Tuần 8)

**Lý thuyết cần nắm**

- Luật An toàn thông tin mạng 2015, Luật An ninh mạng 2018 và văn bản hướng dẫn
- Nghị định 85/2016/NĐ-CP và Thông tư 12/2022/TT-BTTTT về bảo đảm an toàn hệ thống thông tin theo cấp độ
- Bảo vệ dữ liệu cá nhân: Nghị định 13/2023/NĐ-CP và Luật Bảo vệ dữ liệu cá nhân
- Quốc tế: GDPR, PCI DSS v4.0, SOC 2

**Đọc**: tra cứu văn bản gốc và tình trạng hiệu lực trên [Cơ sở dữ liệu quốc gia về văn bản pháp luật](https://vbpl.vn/) hoặc [Thư viện Pháp luật](https://thuvienphapluat.vn/) — văn bản thay đổi thường xuyên, luôn kiểm tra trước khi trích dẫn

### Chương 4.5 — Policy & giao tiếp rủi ro (Tuần 8)

**Lý thuyết cần nắm**

- Cấp tài liệu: Policy → Standard → Procedure → Guideline
- Policy cơ bản: Acceptable Use, Access Control, Password/MFA, Backup, Incident Response, Data Classification
- Báo cáo lãnh đạo: 1 trang, top 5 rủi ro, xu hướng, tiền/thời gian, quyết định cần họ đưa ra

**Đọc**: [SANS Security Policy Templates](https://www.sans.org/information-security-policy/) (mẫu miễn phí)

**Lab**: Viết 2 policy — Access Control và Backup (mỗi bản 1–2 trang) — dựa trên mẫu SANS, điều chỉnh cho tổ chức giả định.

### Mẫu risk register

| ID | Tài sản | Mối đe dọa / điểm yếu | L (1–5) | I (1–5) | Điểm | Control hiện có | Xử lý | Owner | Hạn |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| R-01 | DB khách hàng | SQL injection qua API tìm kiếm | 4 | 5 | 20 | Không | Mitigate: parameterized query + WAF | Trưởng nhóm backend | 2 tuần |
| R-02 | Tài khoản admin | Phishing chiếm mật khẩu | 3 | 5 | 15 | Mật khẩu mạnh | Mitigate: FIDO2 MFA | IT | 1 tháng |
| R-03 | Server file | Ransomware | 3 | 4 | 12 | Backup hàng tuần | Mitigate: backup bất biến hàng ngày + EDR | IT | 1 tháng |
| R-04 | Website marketing | Deface | 2 | 2 | 4 | CMS cập nhật | Accept, review sau 6 tháng | Marketing | — |

### Góc nhìn bảo mật — Module 4

- Kẻ tấn công tận dụng rủi ro bị "chấp nhận ngầm" — thứ không ai sở hữu, không ai review
- Người phòng thủ: mọi rủi ro có owner, quyết định xử lý được ghi lại, review định kỳ và sau mỗi sự cố

### Tiêu chí đạt Module 4

- [ ] Risk register 20 dòng có owner, xử lý, hạn
- [ ] Báo cáo 1 trang top 5 rủi ro cho lãnh đạo, không dùng thuật ngữ thừa
- [ ] Map ≥ 10 rủi ro vào NIST CSF function và CIS safeguard
- [ ] Giải thích được khi nào chấp nhận rủi ro là quyết định đúng

## Module 5 — Threat Modeling (Tuần 9)

Threat modeling trả lời 4 câu hỏi: **Ta đang xây gì? Điều gì có thể sai? Ta sẽ làm gì? Ta làm đủ tốt chưa?** Đây là cách rẻ nhất để tìm lỗi thiết kế trước khi viết code. Tài liệu nền: [Threat Modeling Manifesto](https://www.threatmodelingmanifesto.org/).

### Chương 5.1 — Data Flow Diagram

**Lý thuyết cần nắm**

- Thành phần: External entity, Process, Data store, Data flow, **Trust boundary**
- Mọi luồng qua trust boundary là nơi cần xác thực, phân quyền, validate input, mã hóa
- Vẽ vừa đủ: Level 0 → Level 1

**Đọc**: [OWASP Threat Modeling Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Threat_Modeling_Cheat_Sheet.html), [OWASP Threat Modeling Process](https://owasp.org/www-community/Threat_Modeling_Process)

### Chương 5.2 — STRIDE

**Lý thuyết cần nắm**

| Mối đe dọa | Vi phạm | Ví dụ (hệ thống bán vé flash-sale) | Control điển hình |
| --- | --- | --- | --- |
| **S**poofing | Authentication | Bot giả user mua vé hàng loạt | MFA, rate limit, bot detection |
| **T**ampering | Integrity | Sửa giá vé trong request | Tính giá phía server, ký dữ liệu |
| **R**epudiation | Non-repudiation | User chối đã thanh toán | Audit log bất biến |
| **I**nformation disclosure | Confidentiality | API trả thông tin user khác (IDOR) | Kiểm tra quyền theo đối tượng |
| **D**enial of service | Availability | Flood endpoint đặt vé lúc mở bán | Queue, rate limit, autoscale, CDN/WAF |
| **E**levation of privilege | Authorization | User thường gọi API admin | RBAC phía server |

**Đọc**: [Microsoft — Threat Modeling Tool & STRIDE](https://learn.microsoft.com/azure/security/develop/threat-modeling-tool-threats); sách *Threat Modeling: Designing for Security* (Adam Shostack) chương 1–3

### Chương 5.3 — Phương pháp khác & quy trình buổi họp

| Phương pháp | Đặc điểm | Khi nên dùng |
| --- | --- | --- |
| STRIDE | Theo từng thành phần DFD, dễ học | Mặc định cho team phát triển |
| Attack tree | Mục tiêu ở gốc, nhánh AND/OR | Phân tích sâu 1 mối đe dọa |
| PASTA | 7 bước, gắn mục tiêu kinh doanh | Dự án lớn |
| [LINDDUN](https://linddun.org/) | Quyền riêng tư | Hệ thống xử lý dữ liệu cá nhân |

Quy trình 60–90 phút: chốt phạm vi + vẽ DFD → áp STRIDE qua từng luồng qua trust boundary → ghi mỗi mối đe dọa thành 1 dòng (mô tả, thành phần, likelihood, impact, control) → đưa vào backlog có owner → review khi kiến trúc thay đổi.

**Lab**:

1. Cài [OWASP Threat Dragon](https://owasp.org/www-project-threat-dragon/) (hoặc [Microsoft Threat Modeling Tool](https://learn.microsoft.com/azure/security/develop/threat-modeling-tool))
2. Vẽ DFD Level 1 cho 1 đồ án (ví dụ hệ thống bán vé): client, API gateway, service, DB, cache, payment gateway, admin portal
3. Áp STRIDE, tìm ≥ 20 mối đe dọa
4. Vẽ attack tree cho mục tiêu "mua được vé vượt giới hạn"
5. Chuyển top 10 mối đe dọa thành security requirement theo [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/)
6. Chơi [Elevation of Privilege card game](https://www.microsoft.com/en-us/download/details.aspx?id=20303) cùng bạn trong nhóm đồ án

### Góc nhìn bảo mật — Module 5

- Kẻ tấn công tìm chỗ hệ thống "tin" dữ liệu từ phía không tin cậy — đúng chỗ trust boundary bị bỏ qua
- Người phòng thủ: threat model ngay từ thiết kế, cập nhật khi thêm tính năng, dùng kết quả để ưu tiên test bảo mật

### Tiêu chí đạt Module 5

- [ ] DFD có trust boundary rõ ràng
- [ ] Bảng 20 mối đe dọa STRIDE có control và ưu tiên
- [ ] 1 attack tree ≥ 3 tầng
- [ ] 10 security requirement tham chiếu mã ASVS

## Lịch học 10 tuần

Mỗi tuần khoảng 12–15 giờ: 4 giờ video/đọc, 6–7 giờ lab, 2–3 giờ viết sản phẩm tài liệu, 1 giờ Anki + ghi chú.

| Tuần | Chủ đề | Video / đọc | Lab | Sản phẩm |
| --- | --- | --- | --- | --- |
| 1 | Symmetric, asymmetric, hash, password hashing | Messer 1.4; [Computerphile PKC](https://www.youtube.com/watch?v=GSIDS_lvRv4); OWASP Password Storage | OpenSSL ECB vs CBC; Hashcat MD5 vs bcrypt; CryptoHack | Ghi chú bảng thuật toán |
| 2 | PKI, TLS, crypto trong app | Messer 1.4 (Certificates, PKI); [Illustrated TLS 1.3](https://tls13.xargs.org/) | CA riêng + Nginx HTTPS; testssl.sh | **Crypto review 1 repo** |
| 3 | Authentication, MFA, session, authorization | Messer 4.6; NIST SP 800-63B; OWASP Authentication | PortSwigger Authentication + Access control | Ma trận quyền |
| 4 | OAuth/OIDC/SAML, Zero Trust, IAM doanh nghiệp | [OAuth in plain English](https://classcentral.com/classroom/youtube-oauth-2-0-and-openid-connect-in-plain-english-211239); RFC 9700; NIST SP 800-207 | Keycloak + Spring Boot OIDC; PortSwigger OAuth | **Tài liệu thiết kế IAM** |
| 5 | Tác nhân đe dọa, malware, ATT&CK, control | Messer 2.1–2.4, 1.1; [ATT&CK CTI Training](https://attack.mitre.org/resources/learn-more-about-attack/training/cti/) | ATT&CK Navigator cho 1 nhóm ransomware | ATT&CK layer + control |
| 6 | Vulnerability management | Messer 4.3; FIRST EPSS, CISA KEV | Greenbone quét lab, Trivy | **Vulnerability report** |
| 7 | Quy trình rủi ro, ALE, FAIR | Messer 5.2; NIST SP 800-30 | Asset inventory + 10 rủi ro đầu | Bản nháp risk register |
| 8 | NIST CSF 2.0, ISO 27001, CIS, pháp lý VN, policy | Messer 5.1; NIST CSF 2.0; CIS Controls | CIS IG1 self-assessment; 2 policy | **Risk register 20 dòng + báo cáo lãnh đạo** |
| 9 | Threat modeling | OWASP Threat Modeling Cheat Sheet; Shostack | Threat Dragon DFD + STRIDE + attack tree | **Threat model** |
| 10 | Ôn tập & capstone | Ôn Anki, ghi chú | Capstone | **Báo cáo đánh giá an toàn** |

Tuỳ chọn: sau tuần 10 ôn thêm 2–3 tuần với toàn bộ playlist Messer SY0-701 và thi CompTIA Security+ (kiểm tra phiên bản đề và giá trên trang CompTIA trước khi đăng ký).

## Kiểm tra cuối giai đoạn (Tuần 10)

Đạt khi trả lời trơn tru ≥ 80% câu hỏi (không tra cứu) và hoàn thành capstone có báo cáo.

### Câu hỏi tự đánh giá

**Cryptography**

1. Vì sao không dùng SHA-256 để lưu mật khẩu? Chọn gì thay thế và vì sao?
2. AES-GCM tốt hơn AES-CBC ở điểm nào? Điều gì xảy ra nếu lặp nonce?
3. Trình duyệt xác minh certificate của một website qua những bước nào?
4. Chữ ký số cung cấp những thuộc tính bảo mật nào mà mã hóa thông thường không có?

**IAM**

5. OAuth 2.0 và OpenID Connect khác nhau thế nào? PKCE chống lại tấn công gì?
6. Vì sao FIDO2 chống phishing còn TOTP thì không?
7. RBAC và ABAC khác nhau ra sao? Cho ví dụ cần ABAC.

**Threat & Vulnerability**

8. Phân biệt CVSS, EPSS, KEV. Nếu chỉ được vá 3 lỗi tuần này, bạn chọn theo tiêu chí nào?
9. Pyramid of Pain và Kill Chain giúp người phòng thủ ưu tiên thế nào?

**Risk & Framework**

10. Tính ALE khi AV = 500 triệu, EF = 30%, ARO = 0,5. Control giá 50 triệu/năm giảm ARO còn 0,1 có đáng không?
11. 4 cách xử lý rủi ro là gì? Ai có quyền ký chấp nhận rủi ro?
12. 6 function của NIST CSF 2.0 là gì? Function nào mới so với bản 1.1?
13. ISO 27001 và CIS Controls bổ sung cho nhau thế nào?

**Threat Modeling**

14. Với mỗi chữ của STRIDE, cho 1 ví dụ trên ứng dụng mobile banking.
15. Vì sao trust boundary là nơi ưu tiên kiểm tra trong DFD?

### Capstone: "Báo cáo đánh giá an toàn một hệ thống"

Chọn 1 đồ án của bạn (hoặc tổ chức giả định 50 nhân viên) và nộp báo cáo 10–15 trang:

- [ ] Tóm tắt cho lãnh đạo (1 trang): top 5 rủi ro, chi phí đề xuất, quyết định cần phê duyệt
- [ ] Phạm vi & asset inventory
- [ ] Threat model (DFD + STRIDE)
- [ ] Kết quả quét lỗ hổng và ưu tiên
- [ ] Risk register + ALE cho top 3
- [ ] Đánh giá IAM và crypto
- [ ] Roadmap khắc phục 90 ngày map vào NIST CSF 2.0

Hoàn thành capstone = sẵn sàng vào Giai đoạn 3 (Blue Team).

## Nguồn tham khảo

Các link đánh dấu (✓) đã được kiểm tra qua tìm kiếm ngày 23/11/2026; các link còn lại là trang chính thức của tổ chức/dự án, nên mở lại để xác nhận trước khi dùng.

### Video & khóa học

| Nguồn | Loại | Chi phí | Dùng cho |
| --- | --- | --- | --- |
| [Professor Messer — SY0-701 Security+ Training Course](https://www.professormesser.com/security-plus/sy0-701/sy0-701-video/sy0-701-comptia-security-plus-course/) ✓ | Video, 121 bài | Miễn phí | Toàn giai đoạn |
| [Playlist YouTube Messer SY0-701](https://www.youtube.com/playlist?list=PLG49S3nxzAnl4QDVqK-hOnoqcSKEIDDuv) ✓ | Video | Miễn phí | Toàn giai đoạn |
| [Computerphile — Public Key Cryptography](https://www.youtube.com/watch?v=GSIDS_lvRv4) ✓ | Video ngắn | Miễn phí | Module 1 |
| [OAuth 2.0 and OpenID Connect (in plain English) — Okta](https://classcentral.com/classroom/youtube-oauth-2-0-and-openid-connect-in-plain-english-211239) ✓ và [slide](https://speakerdeck.com/nbarbettini/oauth-and-openid-connect-in-plain-english) ✓ | Video talk | Miễn phí | Module 2 |
| [MITRE ATT&CK — CTI Training](https://attack.mitre.org/resources/learn-more-about-attack/training/cti/) ✓ | Khóa tự học + slide | Miễn phí | Module 3 |
| [Simply Cyber — Gerald Auger (YouTube)](https://www.youtube.com/c/GeraldAuger) ✓ | Video GRC, nghề nghiệp | Miễn phí | Module 4 |
| [Coursera — Cryptography I (Dan Boneh)](https://www.coursera.org/learn/crypto) | Khóa học | Audit miễn phí | Module 1 nâng cao |
| [PortSwigger Web Security Academy](https://portswigger.net/web-security) | Lab | Miễn phí | Module 2 |
| [CryptoHack](https://cryptohack.org/) | Lab crypto | Miễn phí | Module 1 |
| [TryHackMe](https://tryhackme.com/) | Lab | Freemium | Module 3 |

### Chuẩn & tài liệu gốc

| Tài liệu | Tổ chức | Dùng cho |
| --- | --- | --- |
| [NIST CSF 2.0](https://www.nist.gov/cyberframework) | NIST | Module 4 |
| [NIST SP 800-30 Rev. 1](https://csrc.nist.gov/pubs/sp/800/30/r1/final) | NIST | Module 4 |
| [NIST SP 800-63B](https://pages.nist.gov/800-63-4/sp800-63b.html) | NIST | Module 2 |
| [NIST SP 800-207 — Zero Trust](https://csrc.nist.gov/pubs/sp/800/207/final) | NIST | Module 2 |
| [NIST Post-Quantum Cryptography](https://csrc.nist.gov/projects/post-quantum-cryptography) | NIST | Module 1 |
| [CIS Controls v8](https://www.cisecurity.org/controls) | CIS | Module 4 |
| [ISO/IEC 27001](https://www.iso.org/standard/27001) | ISO | Module 4 |
| [MITRE ATT&CK](https://attack.mitre.org/), [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/), [D3FEND](https://d3fend.mitre.org/) | MITRE | Module 3 |
| [CISA KEV](https://www.cisa.gov/known-exploited-vulnerabilities-catalog), [CISA Advisories](https://www.cisa.gov/news-events/cybersecurity-advisories) | CISA | Module 3 |
| [FIRST EPSS](https://www.first.org/epss/), [CVSS](https://www.first.org/cvss/) | FIRST | Module 3 |
| [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/) | OWASP | Module 1, 2, 5 |
| [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/), [Threat Dragon](https://owasp.org/www-project-threat-dragon/) | OWASP | Module 5 |
| [RFC 9700 — OAuth 2.0 Security BCP](https://datatracker.ietf.org/doc/rfc9700/) | IETF | Module 2 |
| [Threat Modeling Manifesto](https://www.threatmodelingmanifesto.org/) | Cộng đồng | Module 5 |
| [The FAIR Institute](https://www.fairinstitute.org/) | FAIR Institute | Module 4 |

### Công cụ

| Công cụ | Dùng cho |
| --- | --- |
| OpenSSL, [testssl.sh](https://testssl.sh/), [SSL Labs](https://www.ssllabs.com/ssltest/), [Hashcat](https://hashcat.net/hashcat/), [crt.sh](https://crt.sh/) | Module 1 |
| [Keycloak](https://www.keycloak.org/), [jwt.io](https://jwt.io/) | Module 2 |
| [Greenbone Community Edition](https://greenbone.github.io/docs/latest/), [Trivy](https://trivy.dev/) | Module 3 |

### Sách

| Sách | Tác giả | Dùng cho |
| --- | --- | --- |
| *Serious Cryptography* (2nd ed.) | Jean-Philippe Aumasson | Module 1 |
| *Threat Modeling: Designing for Security* | Adam Shostack | Module 5 |
| *How to Measure Anything in Cybersecurity Risk* | Douglas Hubbard, Richard Seiersen | Module 4 |
| *CompTIA Security+ Study Guide* | Mike Chapple, David Seidl | Tổng hợp |
