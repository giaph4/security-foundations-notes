# Giáo trình Giai đoạn 5: Chuyên sâu — AppSec, Cloud, CTI, GRC, AI Security (bản chi tiết)

Nov 23, 2026 · @Huynh Gia Pho

Sau nền tảng chung, bạn chọn 1 track chính học sâu 13 tuần và 1 track phụ 6 tuần, tổng 20 tuần. Mỗi chương gồm lý thuyết, video, tài liệu đọc, lab; mỗi track kết thúc bằng dự án portfolio.

## Cách dùng giáo trình

Yêu cầu đầu vào: Giai đoạn 0–4. Học 12–15 giờ/tuần theo vòng **Xem video → Đọc → Lab → Dự án → Viết bài**; giai đoạn này nghiêng về dự án thực tế hơn bài lab riêng lẻ.

### Chọn track

| Track | Phù hợp nếu bạn | Nền tảng tận dụng | Vai trò đích |
| --- | --- | --- | --- |
| A. AppSec & DevSecOps | Thích code, review, CI/CD | Java, Spring, Android, Giai đoạn 4 web | Application Security Engineer, DevSecOps Engineer |
| B. Cloud & Container | Thích hạ tầng, tự động hóa | Linux, network, Docker, IaC | Cloud Security Engineer |
| C. Threat Intelligence | Thích nghiên cứu, viết, phân tích | Giai đoạn 3 hunting, ATT&CK | CTI Analyst, Threat Hunter |
| D. GRC | Thích quy trình, kinh doanh, giao tiếp | Giai đoạn 2 risk, ISO, pháp lý | Risk/Compliance Analyst, ISO 27001 Auditor |
| E. AI Security | Thích điều mới, có nền data science | Python, data science, AppSec | AI/ML Security Engineer, AI Red Teamer |

Gợi ý cho nền tảng kỹ sư phần mềm: **Track A chính + Track B hoặc E phụ**. Ưu điểm: tận dụng tối đa kỹ năng hiện có. Nhược điểm: ít vị trí entry-level hơn SOC, thường cần 1–2 năm kinh nghiệm dev hoặc security trước. Nếu cần việc sớm, chọn C hoặc tiếp tục hướng SOC từ Giai đoạn 3.

### Cấu trúc mỗi track

Mỗi track có 3–4 chương theo đúng khuôn Giai đoạn 0–1: **Lý thuyết cần nắm → Video → Đọc → Lab**, sau đó là **Dự án portfolio**, **Chứng chỉ** và **Tiêu chí đạt**.

### Quy ước

- Repo riêng cho mỗi dự án portfolio, README gồm: bài toán, kiến trúc, cách chạy, kết quả trước/sau, bài học
- Blog (GitHub Pages/Hashnode): 1 bài/2 tuần về điều vừa học
- Cloud lab: tài khoản riêng, bật MFA, đặt budget alert, dọn tài nguyên sau mỗi buổi

## Track A — Application Security & DevSecOps

Đưa bảo mật vào mọi bước của vòng đời phần mềm sao cho lỗi bị bắt sớm, rẻ và tự động. Video chính: [Web App Vulnerabilities — DevSecOps Course for Beginners (freeCodeCamp, \~1,5 giờ)](https://www.youtube.com/watch?v=F5KJVuii0Yw) và [Learn DevSecOps and API Security (freeCodeCamp, 2 giờ)](https://www.freecodecamp.org/news/learn-devsecops-and-api-security/).

### Chương A.1 — Secure SDLC

**Lý thuyết cần nắm**

| Pha | Hoạt động bảo mật | Công cụ / tài liệu |
| --- | --- | --- |
| Requirements | Security requirement từ ASVS, abuse case | OWASP ASVS |
| Design | Threat modeling | Threat Dragon, STRIDE |
| Implementation | Secure coding, code review, pre-commit | Cheat Sheets, Semgrep, Gitleaks |
| Build | SAST, SCA, secret scanning, SBOM | CodeQL, SonarQube, Dependency-Check, Trivy, Syft |
| Test | DAST, API testing, fuzzing | OWASP ZAP, Nuclei |
| Release | Ký artifact, provenance | Sigstore/cosign, SLSA |
| Deploy | IaC scan, container scan, admission policy | Checkov, Trivy, Kyverno |
| Operate | WAF, monitoring, VDP | ModSecurity, SIEM |

Khung trưởng thành: [OWASP SAMM](https://owaspsamm.org/), BSIMM, [NIST SSDF SP 800-218](https://csrc.nist.gov/pubs/sp/800/218/final).

**Video**: [freeCodeCamp DevSecOps (Snyk)](https://www.youtube.com/watch?v=F5KJVuii0Yw) phần What is DevSecOps, DevOps vs DevSecOps

**Đọc**: [OWASP SAMM — Model](https://owaspsamm.org/model/), [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/)

**Lab**: tự đánh giá mức SAMM cho nhóm làm đồ án của bạn, chọn 3 practice cần nâng.

### Chương A.2 — Secure coding Java/Spring & Android

**Lý thuyết cần nắm**

- Spring Security: `SecurityFilterChain`, method security (`@PreAuthorize`), CSRF, CORS, password encoder, session fixation
- Input/output: Bean Validation, output encoding, dùng DTO chống mass assignment/lộ field
- JPA với tham số, tránh JPQL nối chuỗi; tránh Java native serialization với dữ liệu không tin cậy
- Logging: không log mật khẩu/token, chống log injection
- Android: Network Security Config, Keystore, không export component thừa, kiểm tra deep link

**Đọc**: [Spring Security Reference](https://docs.spring.io/spring-security/reference/), [OWASP Java Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Java_Security_Cheat_Sheet.html), [OWASP Mass Assignment Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html)

**Lab**: secure code review [OWASP WebGoat](https://owasp.org/www-project-webgoat/) hoặc [Snyk Java Goof](https://github.com/snyk/java-goof); [Snyk Learn](https://learn.snyk.io/) bài Java.

### Chương A.3 — Pipeline DevSecOps

**Lý thuyết cần nắm** — pipeline mẫu GitHub Actions:

```yaml
name: devsecops
on: [pull_request]
jobs:
  security:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      security-events: write   # upload kết quả SARIF
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0       # Gitleaks cần lịch sử commit
      - name: Secret scanning
        uses: gitleaks/gitleaks-action@v2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      - name: SAST (Semgrep)
        run: |
          pip install semgrep
          semgrep scan --config p/java --config p/owasp-top-ten --error
      - name: SCA + IaC (Trivy)
        uses: aquasecurity/trivy-action@master  # pin theo commit SHA trong dự án thật
        with:
          scan-type: fs
          severity: CRITICAL,HIGH
          exit-code: '1'       # chặn merge nếu có lỗi nghiêm trọng
```

- Vận hành: bắt đầu chế độ cảnh báo, tuning false positive, sau đó mới chặn build; pin action theo SHA; token CI least privilege
- So sánh: SAST bắt sớm nhưng nhiều false positive; DAST chính xác hơn nhưng cần app chạy; SCA rẻ và hiệu quả cao — nên kết hợp SCA + SAST + DAST

**Video**: [TechWorld with Nana — DevSecOps Tutorial with GitHub Actions](https://classcentral.com/classroom/youtube-devsecops-tutorial-for-beginners-with-github-actions-and-docker-scout-273517)

**Đọc**: [Semgrep docs](https://semgrep.dev/docs/), [GitHub CodeQL](https://codeql.github.com/docs/), [Trivy docs](https://trivy.dev/), [OWASP ZAP — Getting Started](https://www.zaproxy.org/getting-started/)

**Lab**: áp pipeline trên cho 1 đồ án Spring Boot; viết 5 Semgrep rule tùy biến; chạy ZAP baseline scan trên môi trường staging.

### Chương A.4 — Software supply chain

**Lý thuyết cần nắm**

- SBOM (CycloneDX, SPDX), VEX; lockfile, private registry
- Typosquatting, dependency confusion, CI bị chiếm, maintainer bị chiếm tài khoản
- [SLSA](https://slsa.dev/), [Sigstore/cosign](https://www.sigstore.dev/), [OpenSSF Scorecard](https://securityscorecards.dev/)

**Lab**: tạo SBOM bằng [Syft](https://github.com/anchore/syft), ký image bằng cosign, verify trong bước deploy.

### Dự án portfolio, chứng chỉ & tiêu chí đạt

- **Dự án A1**: pipeline DevSecOps cho 1 đồ án Java, số finding trước/sau tuning, sửa mọi Critical/High
- **Dự án A2**: báo cáo secure code review theo ASVS (≥ 10 phát hiện)
- Chứng chỉ tham khảo: Burp Suite Certified Practitioner, OSWE (nâng cao), Certified DevSecOps Professional

* [ ] Pipeline chạy thật, có security gate và tài liệu tuning
* [ ] Báo cáo code review theo ASVS
* [ ] Giải thích vì sao SBOM giúp phản ứng nhanh khi có CVE thư viện mới như Log4Shell

## Track B — Cloud & Container Security

Phần lớn sự cố cloud đến từ cấu hình sai và danh tính quá quyền, không phải lỗ hổng của nhà cung cấp. Chọn 1 cloud chính (khuyến nghị AWS vì tài liệu và lab nhiều nhất). Video chính: [freeCodeCamp — AWS Certified Cloud Practitioner course](https://www.freecodecamp.org/news/aws-certified-cloud-practitioner-certification-study-course-pass-the-exam/) (nền tảng) và [freeCodeCamp — Google Cloud Cybersecurity course](https://www.freecodecamp.org/news/beginners-guide-to-cloud-cybersecurity/).

### Chương B.1 — Nền tảng cloud security & IAM

**Lý thuyết cần nắm**

- **Shared Responsibility Model**: IaaS → PaaS → SaaS; danh tính và dữ liệu luôn là trách nhiệm của bạn
- **IAM**: user vs role, policy JSON (Effect/Action/Resource/Condition), least privilege, permission boundary, SCP; tránh access key dài hạn — dùng IAM Identity Center, role assumption, OIDC federation cho CI/CD
- Network: VPC, subnet public/private, security group vs NACL, VPC endpoint
- Data: KMS, S3 Block Public Access, bucket policy, Secrets Manager
- Logging: CloudTrail, GuardDuty, Security Hub, AWS Config, VPC Flow Logs
- Compute: IMDSv2 bắt buộc, SSM Session Manager thay SSH

**Đọc**: [freeCodeCamp — Learn Cloud Security Fundamentals in AWS](https://www.freecodecamp.org/news/learn-cloud-security-fundamentals-in-aws-a-guide-for-beginners/), [AWS Security documentation](https://docs.aws.amazon.com/security/), [AWS IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)

**Lab**: tạo AWS account lab riêng, MFA cho root, budget alert 5 USD, CloudTrail mọi region; viết 3 IAM policy least privilege cho 3 vai trò.

### Chương B.2 — Tấn công cloud & phòng chống

**Lý thuyết cần nắm**

| Tấn công | Ví dụ | Phát hiện / phòng chống |
| --- | --- | --- |
| Lộ access key | Key trong GitHub, image Docker | Secret scanning, không dùng key dài hạn, GuardDuty |
| Storage public | S3/Blob mở công khai | Block Public Access cấp account, Config rule |
| IAM privilege escalation | `iam:PassRole`, `iam:CreatePolicyVersion` | Least privilege, IAM Access Analyzer |
| SSRF → metadata | Lấy credential role của EC2 | IMDSv2, hop limit |
| Crypto-mining | Khởi tạo hàng loạt instance GPU | Budget alert, SCP giới hạn region/instance |

**Đọc**: [Hacking the Cloud](https://hackingthe.cloud/) (bách khoa kỹ thuật tấn công/phòng thủ cloud)

**Lab**: [flAWS](http://flaws.cloud/) và [flAWS2](http://flaws2.cloud/) (cả Attacker và Defender path); [CloudGoat](https://github.com/RhinoSecurityLabs/cloudgoat) 5 scenario, mỗi scenario ghi CloudTrail event tương ứng.

### Chương B.3 — IaC & CSPM

**Lý thuyết cần nắm**

- Terraform an toàn: remote state mã hóa + lock, không commit `.tfstate`
- Scan IaC: [Checkov](https://www.checkov.io/), Trivy config; policy-as-code bằng OPA/Conftest
- CSPM mã nguồn mở: [Prowler](https://github.com/prowler-cloud/prowler), ScoutSuite; CIS AWS Foundations Benchmark

**Đọc**: [Terraform — Sensitive data in state](https://developer.hashicorp.com/terraform/language/state/sensitive-data), [Prowler docs](https://docs.prowler.com/)

**Lab**: chạy Prowler trên account lab, sửa 10 phát hiện bằng Terraform, chạy lại so sánh.

### Chương B.4 — Container & Kubernetes security

**Lý thuyết cần nắm**

- Image: distroless/Alpine, non-root, multi-stage build, scan Trivy, ký cosign
- Kubernetes: RBAC, ServiceAccount token, NetworkPolicy, Pod Security Standards (restricted), Secrets, admission control ([Kyverno](https://kyverno.io/)), audit log
- Runtime: [Falco](https://falco.org/); đánh giá: [kube-bench](https://github.com/aquasecurity/kube-bench), kubescape

**Đọc**: [Kubernetes — Security Checklist](https://kubernetes.io/docs/concepts/security/security-checklist/), [OWASP Kubernetes Top 10](https://owasp.org/www-project-kubernetes-top-ten/)

**Lab**: [Kubernetes Goat](https://madhuakula.com/kubernetes-goat/) trên kind/minikube; áp Kyverno policy + Falco + NetworkPolicy, mô phỏng container escape và ghi lại phát hiện.

### Dự án portfolio, chứng chỉ & tiêu chí đạt

- **Dự án B1**: triển khai đồ án lên AWS bằng Terraform theo kiến trúc an toàn (private subnet, ALB + WAF, RDS mã hóa, Secrets Manager, IAM role tối thiểu); báo cáo Prowler + Checkov trước/sau
- **Dự án B2**: cụm K8s có Kyverno + Falco + NetworkPolicy, báo cáo mô phỏng tấn công
- Chứng chỉ tham khảo: AWS Certified Security – Specialty, AZ-500, CCSK, CKS, CCSP

* [ ] flAWS 1–2 + 5 scenario CloudGoat có write-up attacker + defender
* [ ] Dự án B1 có điểm Prowler cải thiện rõ, code Terraform trên GitHub
* [ ] Giải thích 3 con đường IAM privilege escalation và cách chặn

## Track C — Cyber Threat Intelligence

CTI biến thông tin về kẻ tấn công thành quyết định — track trực tiếp nhất cho yêu cầu "phản ứng linh hoạt trước mối đe dọa mới". Video chính: [MITRE ATT&CK — CTI Training](https://attack.mitre.org/resources/learn-more-about-attack/training/cti/) (miễn phí, có bài tập map báo cáo vào ATT&CK).

### Chương C.1 — Vòng đời & phương pháp phân tích

**Lý thuyết cần nắm**

1. **Direction**: Priority Intelligence Requirements — ví dụ "Nhóm ransomware nào đang nhắm ngành bán lẻ Đông Nam Á?"
2. **Collection**: nguồn mở, feed, telemetry nội bộ, chia sẻ ngành
3. **Processing**: chuẩn hóa (STIX 2.1), loại trùng, gắn nhãn TLP
4. **Analysis**: Diamond Model, ATT&CK mapping, Analysis of Competing Hypotheses, đánh giá độ tin cậy
5. **Dissemination**: flash alert cho SOC, báo cáo chiến dịch cho IR, brief cho lãnh đạo
6. **Feedback**: đo mức độ hữu ích, cập nhật PIR

**Video**: [ATT&CK CTI Training](https://attack.mitre.org/resources/learn-more-about-attack/training/cti/) module 0–2

**Đọc**: [FIRST — Traffic Light Protocol](https://www.first.org/tlp/), [STIX 2.1 introduction](https://oasis-open.github.io/cti-documentation/stix/intro)

**Lab**: TryHackMe phòng [Cyber Threat Intelligence](https://tryhackme.com/room/cyberthreatintel) và [Diamond Model](https://tryhackme.com/room/diamondmodelrmuwwg42) (hoặc tương đương); bài tập map báo cáo trong ATT&CK CTI Training.

### Chương C.2 — Nguồn & công cụ

**Lý thuyết cần nắm**

- Nguồn mở: [CISA Advisories](https://www.cisa.gov/news-events/cybersecurity-advisories), [The DFIR Report](https://thedfirreport.com/), [Google Threat Intelligence blog](https://cloud.google.com/blog/topics/threat-intelligence), [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/), [Unit 42](https://unit42.paloaltonetworks.com/), [Cisco Talos](https://blog.talosintelligence.com/), [abuse.ch](https://abuse.ch/), [AlienVault OTX](https://otx.alienvault.com/)
- Pivoting hạ tầng thụ động: passive DNS, WHOIS lịch sử, certificate, [URLScan](https://urlscan.io/), VirusTotal relations
- Nền tảng: [OpenCTI](https://filigran.io/solutions/open-cti/), [MISP](https://www.misp-project.org/); [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)

**Lab**: triển khai OpenCTI (Docker), kết nối connector ATT&CK, CISA KEV, OTX; TryHackMe phòng [OpenCTI](https://tryhackme.com/room/opencti).

### Chương C.3 — Viết báo cáo CTI

**Lý thuyết cần nắm**

- BLUF: kết luận + mức độ tin cậy → bằng chứng → tác động → khuyến nghị hành động
- Ngôn ngữ ước lượng: "gần như chắc chắn", "có khả năng", "không chắc" — tách sự thật và đánh giá
- Tránh bias: confirmation bias, mirror imaging; ghi rõ khoảng trống thông tin

**Đọc**: sách *Intelligence-Driven Incident Response* (Rebekah Brown, Scott J. Roberts); [CISA advisory bất kỳ](https://www.cisa.gov/news-events/cybersecurity-advisories) làm mẫu cấu trúc

**Lab**: viết 1 flash alert (1 trang) và 1 brief lãnh đạo (1 trang) từ cùng một báo cáo chiến dịch.

### Dự án portfolio, chứng chỉ & tiêu chí đạt

- **Dự án C1**: hồ sơ 1 nhóm ransomware/APT có nhắm vào Việt Nam/Đông Nam Á từ nguồn công khai — lịch sử, mục tiêu, TTP (ATT&CK layer), IOC còn hiệu lực, detection đề xuất
- **Dự án C2**: bản tin threat hàng tuần trong 6 tuần cho tổ chức giả định, mỗi số có 3 tin + "việc cần làm ngay"
- Chứng chỉ tham khảo: Arcx CTI 101 (miễn phí), CREST CPTIA, GIAC GCTI

* [ ] Hồ sơ tác nhân có ATT&CK layer và đánh giá độ tin cậy
* [ ] 6 số bản tin tuần
* [ ] Chuyển 1 báo cáo chiến dịch thành 5 Sigma rule + 3 giả thuyết hunt

## Track D — GRC (Governance, Risk & Compliance)

GRC là nơi trách nhiệm bảo vệ hệ thống được chính thức hóa: ai chịu trách nhiệm, kiểm soát nào bắt buộc, chứng minh với kiểm toán ra sao. Video chính: kênh [Simply Cyber — Gerald Auger](https://www.youtube.com/c/GeraldAuger) (nhiều playlist miễn phí về GRC, phỏng vấn GRC entry-level) và trang tổng hợp tài nguyên miễn phí [SimplyCyber.io](https://SimplyCyber.io).

### Chương D.1 — Governance

**Lý thuyết cần nắm**

- Cơ cấu: HĐQT/Ban giám đốc → CISO → security team; mô hình Three Lines
- RACI cho quy trình bảo mật; chiến lược 1–3 năm gắn mục tiêu kinh doanh; ngân sách theo rủi ro
- KPI (% patch đúng SLA, % user có MFA chống phishing) và KRI (số rủi ro vượt khẩu vị)

**Video**: Professor Messer SY0-701 mục 5.1 (Security Policies, Standards, Procedures, Governance) — [khóa học](https://www.professormesser.com/security-plus/sy0-701/sy0-701-video/sy0-701-comptia-security-plus-course/)

**Đọc**: [NIST CSF 2.0 — Govern function](https://www.nist.gov/cyberframework)

### Chương D.2 — Xây ISMS theo ISO/IEC 27001:2022

**Lý thuyết cần nắm**

1. Bối cảnh, bên liên quan, phạm vi ISMS (điều khoản 4)
2. Cam kết lãnh đạo, chính sách, vai trò (điều khoản 5)
3. Đánh giá và xử lý rủi ro, **Statement of Applicability** cho 93 control Annex A (điều khoản 6)
4. Nguồn lực, năng lực, nhận thức, tài liệu (điều khoản 7)
5. Vận hành control (điều khoản 8)
6. Giám sát, **internal audit**, management review (điều khoản 9)
7. Khắc phục, cải tiến liên tục (điều khoản 10)

**Đọc**: [ISO/IEC 27001](https://www.iso.org/standard/27001) (bản chuẩn có phí; trang ISO có tóm tắt), [CIS Controls v8](https://www.cisecurity.org/controls) để map control kỹ thuật

**Lab**: dựng [CISO Assistant](https://github.com/intuitem/ciso-assistant-community) (mã nguồn mở) hoặc [Eramba](https://www.eramba.org/), nhập risk register từ Giai đoạn 2 và bộ control ISO 27001.

### Chương D.3 — Compliance thường gặp

| Khung | Áp dụng cho | Trọng tâm |
| --- | --- | --- |
| ISO/IEC 27001 | Mọi tổ chức | ISMS có chứng nhận |
| Cấp độ ATTT hệ thống thông tin (NĐ 85/2016, TT 12/2022) | Cơ quan, doanh nghiệp tại VN | Phân loại cấp độ 1–5, yêu cầu tối thiểu |
| Bảo vệ dữ liệu cá nhân (NĐ 13/2023, Luật BVDLCN) | Tổ chức xử lý dữ liệu cá nhân tại VN | Đánh giá tác động, đồng ý, thông báo vi phạm |
| [PCI DSS v4.0](https://www.pcisecuritystandards.org/) | Xử lý thẻ thanh toán | 12 yêu cầu |
| SOC 2 | SaaS phục vụ khách hàng Mỹ | Trust Services Criteria |
| GDPR | Dữ liệu cư dân EU | Quyền chủ thể, DPO, 72 giờ thông báo |

**Đọc**: văn bản gốc trên [vbpl.vn](https://vbpl.vn/) hoặc [thuvienphapluat.vn](https://thuvienphapluat.vn/) — luôn kiểm tra hiệu lực trước khi áp dụng

### Chương D.4 — Risk nâng cao & vận hành

**Lý thuyết cần nắm**

- Business Impact Analysis → RTO/RPO → BCP/DRP
- Third-party risk: questionnaire, phân hạng nhà cung cấp, điều khoản hợp đồng
- Định lượng rủi ro bằng FAIR + Monte Carlo

**Đọc**: [The FAIR Institute](https://www.fairinstitute.org/), [NIST SP 800-30](https://csrc.nist.gov/pubs/sp/800/30/r1/final)

**Lab**: mô phỏng Monte Carlo 10.000 lần bằng Python cho kịch bản ransomware, trình bày phân phối tổn thất; vendor assessment cho 1 SaaS giả định.

### Dự án portfolio, chứng chỉ & tiêu chí đạt

- **Dự án D1**: bộ tài liệu ISMS cho công ty giả định 50 người: phạm vi, chính sách, risk assessment, SoA, 5 procedure, kế hoạch audit
- **Dự án D2**: gap assessment theo NIST CSF 2.0 + roadmap 12 tháng có ngân sách
- Chứng chỉ tham khảo: ISO/IEC 27001 Lead Implementer / Lead Auditor, CISA, CRISC, CISM, CISSP (cần kinh nghiệm — kiểm tra điều kiện)

* [ ] Bộ tài liệu ISMS có SoA
* [ ] Gap assessment + roadmap ưu tiên theo rủi ro
* [ ] Trình bày 10 phút cho "ban giám đốc" về top rủi ro và quyết định cần phê duyệt

## Track E — AI Security

Mảng mới và thay đổi nhanh, phù hợp nếu bạn có nền data science. Hai hướng: bảo mật **cho** hệ thống AI và dùng AI **để** bảo mật. Nguồn chính: [OWASP GenAI Security Project](https://genai.owasp.org/) và [MITRE ATLAS](https://atlas.mitre.org/).

### Chương E.1 — Mối đe dọa với ứng dụng LLM

**Lý thuyết cần nắm** (theo OWASP Top 10 for LLM Applications)

| Rủi ro | Mô tả | Phòng chống |
| --- | --- | --- |
| Prompt injection (trực tiếp & gián tiếp) | Chỉ dẫn độc trong input hoặc trong tài liệu/web model đọc | Tách dữ liệu khỏi chỉ dẫn, hạn chế quyền tool, xác nhận người dùng cho hành động nhạy cảm |
| Sensitive information disclosure | Lộ system prompt, dữ liệu người khác | Phân quyền RAG theo user, lọc dữ liệu |
| Supply chain | Model/dataset/thư viện bị nhiễm | Nguồn tin cậy, tránh file pickle không tin cậy |
| Data & model poisoning | Dữ liệu fine-tune bị chèn | Kiểm soát pipeline dữ liệu, đánh giá trước triển khai |
| Improper output handling | Output được thực thi/hiển thị không kiểm tra | Coi output như input không tin cậy |
| Excessive agency | Agent có quá nhiều quyền/tool | Least privilege cho tool, human-in-the-loop |
| Unbounded consumption | DoS/chi phí tăng vọt | Rate limit, quota |

**Đọc**: [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/) (bản mới nhất), [PortSwigger — Web LLM attacks](https://portswigger.net/web-security/llm-attacks)

**Lab**: [Lakera Gandalf](https://gandalf.lakera.ai/); PortSwigger mục Web LLM attacks.

### Chương E.2 — Framework & quản trị AI

**Lý thuyết cần nắm**

- [MITRE ATLAS](https://atlas.mitre.org/): tactic/technique tấn công hệ thống ML
- [NIST AI RMF 1.0](https://www.nist.gov/itl/ai-risk-management-framework) (Govern, Map, Measure, Manage) và hồ sơ Generative AI
- ISO/IEC 42001: hệ thống quản lý AI
- Adversarial ML cổ điển: evasion, model extraction, membership inference

**Lab**: map 5 kỹ thuật ATLAS vào một ứng dụng chatbot giả định; thử adversarial example trên model phân loại ảnh nhỏ bằng [IBM Adversarial Robustness Toolbox](https://github.com/Trusted-AI/adversarial-robustness-toolbox).

### Chương E.3 — Test bảo mật ứng dụng LLM & AI cho bảo mật

**Lý thuyết cần nắm**

- Công cụ quét/red team LLM: [garak](https://github.com/NVIDIA/garak), [PyRIT](https://github.com/Azure/PyRIT)
- AI cho bảo mật: hỗ trợ triage alert, tóm tắt incident, giải thích script bị làm rối, viết query/rule nháp — luôn cần người xác minh, không đưa dữ liệu nhạy cảm vào dịch vụ chưa phê duyệt
- Kẻ tấn công dùng AI: phishing cá nhân hóa, deepfake giọng nói/video trong BEC — cần quy trình xác minh ngoài kênh

**Lab**: dùng garak quét một model chạy local (ví dụ qua Ollama), ghi lại nhóm lỗi phát hiện.

### Dự án portfolio & tiêu chí đạt

- **Dự án E1**: ứng dụng RAG nhỏ (tài liệu nội bộ giả định) — threat model theo OWASP LLM Top 10 + ATLAS, triển khai phòng chống (phân quyền theo user, lọc output, giới hạn tool), test bằng garak/PyRIT, báo cáo kết quả
- **Dự án E2**: hướng dẫn nội bộ "Sử dụng AI an toàn" cho tổ chức giả định

* [ ] Threat model + báo cáo test cho ứng dụng RAG
* [ ] Giải thích indirect prompt injection và vì sao không thể chỉ dựa vào lọc prompt
* [ ] Map 5 kỹ thuật ATLAS vào hệ thống của mình

## Lịch học 20 tuần, kiểm tra & portfolio

Ví dụ lịch cho tổ hợp khuyến nghị **Track A (chính) + Track B (phụ)**; nếu chọn track khác, giữ nguyên nhịp: 4 tuần nền tảng → 5 tuần lab nâng cao + dự án 1 → 4 tuần dự án 2 + chứng chỉ → 6 tuần track phụ → 1 tuần tổng kết.

| Tuần | Track | Chủ đề | Video / đọc | Lab / sản phẩm |
| --- | --- | --- | --- | --- |
| 1 | A | Secure SDLC, SAMM | [freeCodeCamp DevSecOps](https://www.youtube.com/watch?v=F5KJVuii0Yw); OWASP SAMM | Tự đánh giá SAMM |
| 2 | A | Secure coding Spring | Spring Security Reference; OWASP Java Cheat Sheet | Review WebGoat/Java Goof |
| 3 | A | Secure coding Android, Snyk Learn | Android security tips | Ghi chú lỗi hay gặp |
| 4 | A | SAST/SCA/secret scanning | Semgrep, Trivy docs | Pipeline bản nháp |
| 5–6 | A | Pipeline đầy đủ, tuning | TechWorld with Nana DevSecOps | Pipeline chạy trên đồ án |
| 7 | A | DAST, ZAP | ZAP Getting Started | ZAP baseline trên staging |
| 8–9 | A | Semgrep rule tùy biến, CodeQL | CodeQL docs | **Dự án A1** |
| 10–11 | A | Supply chain, SBOM, ký artifact | SLSA, Sigstore | SBOM + cosign |
| 12–13 | A | Secure code review theo ASVS | OWASP ASVS | **Dự án A2** + ôn chứng chỉ |
| 14 | B | Cloud fundamentals, IAM | [freeCodeCamp AWS CCP](https://www.freecodecamp.org/news/aws-certified-cloud-practitioner-certification-study-course-pass-the-exam/) | Account lab, 3 IAM policy |
| 15 | B | Tấn công cloud | Hacking the Cloud | flAWS 1–2 |
| 16 | B | CloudGoat | Hacking the Cloud | 5 scenario |
| 17 | B | IaC, CSPM | Prowler, Checkov docs | Prowler trước/sau |
| 18–19 | B | Container & K8s | K8s Security Checklist | **Dự án B1** (hoặc B2) |
| 20 | — | Tổng kết | — | Portfolio, blog, CV |

### Portfolio cuối giai đoạn

- [ ] 2 dự án track chính + 1 dự án track phụ, mỗi dự án có README đầy đủ
- [ ] Blog: ≥ 10 bài (write-up, nghiên cứu, hướng dẫn)
- [ ] 1 chứng chỉ thuộc track chính (hoặc đã có lịch thi)
- [ ] CV 1 trang mô tả dự án bằng kết quả đo được

### Câu hỏi phỏng vấn tự luyện

1. (AppSec) SCA báo 400 lỗ hổng thư viện trong một repo cũ — bạn xử lý thế nào?
2. (AppSec) Review đoạn code đăng nhập Spring Boot và chỉ ra 5 vấn đề.
3. (Cloud) Access key AWS bị đẩy lên GitHub công khai 2 giờ trước — làm gì theo thứ tự?
4. (Cloud) Thiết kế IAM cho CI/CD deploy lên AWS không dùng key dài hạn.
5. (CTI) Lãnh đạo hỏi "Chúng ta có bị ảnh hưởng bởi chiến dịch X không?" — trả lời trong 24 giờ thế nào?
6. (GRC) Ban giám đốc muốn đạt ISO 27001 trong 9 tháng — kế hoạch và rủi ro của kế hoạch?
7. (AI) Chatbot nội bộ có quyền đọc email và gửi tin nhắn — liệt kê rủi ro và control.

## Nguồn tham khảo

Các link đánh dấu (✓) đã được kiểm tra qua tìm kiếm ngày 23/11/2026; các link còn lại là trang chính thức của tổ chức/dự án, nên mở lại để xác nhận trước khi dùng.

### Video & khóa học

| Nguồn | Track | Chi phí |
| --- | --- | --- |
| [freeCodeCamp — Web App Vulnerabilities, DevSecOps Course for Beginners](https://www.youtube.com/watch?v=F5KJVuii0Yw) ✓ | A | Miễn phí |
| [freeCodeCamp — Learn DevSecOps and API Security](https://www.freecodecamp.org/news/learn-devsecops-and-api-security/) ✓ | A | Miễn phí |
| [TechWorld with Nana — DevSecOps Tutorial (GitHub Actions)](https://classcentral.com/classroom/youtube-devsecops-tutorial-for-beginners-with-github-actions-and-docker-scout-273517) ✓ | A | Miễn phí |
| [freeCodeCamp — AWS Certified Cloud Practitioner course](https://www.freecodecamp.org/news/aws-certified-cloud-practitioner-certification-study-course-pass-the-exam/) ✓ | B | Miễn phí |
| [freeCodeCamp — Google Cloud Cybersecurity course](https://www.freecodecamp.org/news/beginners-guide-to-cloud-cybersecurity/) ✓ | B | Miễn phí |
| [freeCodeCamp — Learn Cloud Security Fundamentals in AWS](https://www.freecodecamp.org/news/learn-cloud-security-fundamentals-in-aws-a-guide-for-beginners/) ✓ | B | Miễn phí |
| [MITRE ATT&CK — CTI Training](https://attack.mitre.org/resources/learn-more-about-attack/training/cti/) ✓ | C | Miễn phí |
| [Simply Cyber — Gerald Auger (YouTube)](https://www.youtube.com/c/GeraldAuger) ✓ và [SimplyCyber.io](https://SimplyCyber.io) ✓ | D | Miễn phí |
| [Professor Messer SY0-701](https://www.professormesser.com/security-plus/sy0-701/sy0-701-video/sy0-701-comptia-security-plus-course/) ✓ | D | Miễn phí |
| [Snyk Learn](https://learn.snyk.io/) | A | Miễn phí |
| [PortSwigger — Web LLM attacks](https://portswigger.net/web-security/llm-attacks), [Lakera Gandalf](https://gandalf.lakera.ai/) | E | Miễn phí |

### Chuẩn, framework & tài liệu

| Track | Nguồn |
| --- | --- |
| A | [OWASP SAMM](https://owaspsamm.org/), [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/), [NIST SSDF SP 800-218](https://csrc.nist.gov/pubs/sp/800/218/final), [SLSA](https://slsa.dev/), [Sigstore](https://www.sigstore.dev/), [OpenSSF Scorecard](https://securityscorecards.dev/), [Spring Security Reference](https://docs.spring.io/spring-security/reference/), [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/) |
| B | [AWS Security documentation](https://docs.aws.amazon.com/security/), [AWS IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html), [Hacking the Cloud](https://hackingthe.cloud/), [Kubernetes Security Checklist](https://kubernetes.io/docs/concepts/security/security-checklist/), [OWASP Kubernetes Top 10](https://owasp.org/www-project-kubernetes-top-ten/) |
| C | [MITRE ATT&CK](https://attack.mitre.org/), [FIRST TLP](https://www.first.org/tlp/), [STIX 2.1](https://oasis-open.github.io/cti-documentation/stix/intro), [CISA Advisories](https://www.cisa.gov/news-events/cybersecurity-advisories), [The DFIR Report](https://thedfirreport.com/) |
| D | [ISO/IEC 27001](https://www.iso.org/standard/27001), [NIST CSF 2.0](https://www.nist.gov/cyberframework), [NIST SP 800-30](https://csrc.nist.gov/pubs/sp/800/30/r1/final), [CIS Controls](https://www.cisecurity.org/controls), [PCI SSC](https://www.pcisecuritystandards.org/), [FAIR Institute](https://www.fairinstitute.org/), [vbpl.vn](https://vbpl.vn/) |
| E | [OWASP GenAI Security Project](https://genai.owasp.org/), [MITRE ATLAS](https://atlas.mitre.org/), [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) |

### Lab & công cụ

| Track | Nguồn |
| --- | --- |
| A | [OWASP WebGoat](https://owasp.org/www-project-webgoat/), [Snyk Java Goof](https://github.com/snyk/java-goof), [Semgrep](https://semgrep.dev/docs/), [CodeQL](https://codeql.github.com/docs/), [Trivy](https://trivy.dev/), [OWASP ZAP](https://www.zaproxy.org/), [Syft](https://github.com/anchore/syft) |
| B | [flAWS](http://flaws.cloud/), [flAWS2](http://flaws2.cloud/), [CloudGoat](https://github.com/RhinoSecurityLabs/cloudgoat), [Prowler](https://github.com/prowler-cloud/prowler), [Checkov](https://www.checkov.io/), [Kubernetes Goat](https://madhuakula.com/kubernetes-goat/), [Falco](https://falco.org/), [Kyverno](https://kyverno.io/), [kube-bench](https://github.com/aquasecurity/kube-bench) |
| C | [OpenCTI](https://filigran.io/solutions/open-cti/), [MISP](https://www.misp-project.org/), [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/), [URLScan](https://urlscan.io/), [AlienVault OTX](https://otx.alienvault.com/) |
| D | [CISO Assistant](https://github.com/intuitem/ciso-assistant-community), [Eramba](https://www.eramba.org/) |
| E | [garak](https://github.com/NVIDIA/garak), [PyRIT](https://github.com/Azure/PyRIT), [IBM Adversarial Robustness Toolbox](https://github.com/Trusted-AI/adversarial-robustness-toolbox) |

### Sách

| Sách | Tác giả | Track |
| --- | --- | --- |
| *Alice and Bob Learn Application Security* | Tanya Janca | A |
| *Agile Application Security* | Laura Bell và cộng sự | A |
| *Hacking Kubernetes* | Andrew Martin, Michael Hausenblas | B |
| *Intelligence-Driven Incident Response* | Rebekah Brown, Scott J. Roberts | C |
| *Measuring and Managing Information Risk: A FAIR Approach* | Jack Freund, Jack Jones | D |
