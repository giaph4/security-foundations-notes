# Roadmap An ninh mạng & An toàn thông tin

Nov 23, 2026 · @Huynh Gia Pho

## Tổng quan

Lộ trình 18–24 tháng, 6 giai đoạn, từ nền tảng IT đến chuyên sâu; mỗi giai đoạn có **gate** (tiêu chí đạt) trước khi đi tiếp. Mục tiêu cuối: tự đánh giá rủi ro, phát hiện – phản ứng sự cố, và chịu trách nhiệm bảo vệ một hệ thống thật.

### Tư duy cốt lõi (áp dụng xuyên suốt)

- **CIA Triad + AAA**: Confidentiality, Integrity, Availability; Authentication, Authorization, Accounting. Mọi quyết định bảo mật đều trả lời: đang bảo vệ thuộc tính nào?
- **Risk-based thinking**: Risk = Likelihood × Impact. Không có hệ thống an toàn tuyệt đối, chỉ có rủi ro được chấp nhận có ý thức.
- **Defense in Depth & Zero Trust**: nhiều lớp kiểm soát; không tin mặc định bất kỳ user, device hay network nào.
- **Assume Breach**: thiết kế như thể kẻ tấn công đã ở bên trong — ưu tiên detection, logging, khả năng khôi phục.
- **Think like attacker, act like defender**: hiểu kỹ thuật tấn công (MITRE ATT&CK) để xây phòng thủ đúng chỗ.
- **Ownership**: chịu trách nhiệm = có tài liệu, có runbook, có số liệu chứng minh, và báo cáo minh bạch khi sự cố xảy ra.

### Lộ trình tổng thể

| Giai đoạn | Thời lượng | Trọng tâm | Gate để đi tiếp |
| --- | --- | --- | --- |
| 0–1. Nền tảng IT | 3–4 tháng | Networking, Linux/Windows, Python/Bash | Tự dựng lab, đọc được PCAP, viết script tự động hóa |
| 2. Security Foundations | 2–3 tháng | Crypto, IAM, risk, threat modeling | Viết được risk register + threat model cho 1 app |
| 3. Blue Team | 4–5 tháng | SOC, SIEM, detection, IR, forensics | Viết detection rule, xử lý trọn 1 incident giả lập |
| 4. Red Team | 4–5 tháng | Pentest web/network/AD | Hoàn thành pentest lab + viết báo cáo chuyên nghiệp |
| 5. Chuyên sâu | 4–6 tháng | Cloud, AppSec/DevSecOps, CTI, GRC | Portfolio 3–5 dự án thực tế trong 1 chuyên ngành |
| 6. Liên tục | Suốt sự nghiệp | Threat watch, cộng đồng, chứng chỉ | Quy trình cập nhật hàng tuần |

### Các hướng nghề chính

| Hướng | Vai trò điển hình | Phù hợp nếu bạn thích |
| --- | --- | --- |
| Blue Team | SOC Analyst, Detection Engineer, Incident Responder, DFIR | Phân tích log, điều tra, phản ứng nhanh |
| Red Team | Penetration Tester, Red Teamer, Bug Bounty Hunter | Tìm lỗ hổng, sáng tạo đường tấn công |
| AppSec / DevSecOps | Application Security Engineer, Security Champion | Code, CI/CD, review bảo mật — tận dụng nền Java/Android |
| Cloud Security | Cloud Security Engineer/Architect | AWS/Azure/GCP, IaC, Kubernetes |
| GRC | Risk Analyst, Compliance, ISO 27001 Auditor | Chính sách, quy trình, đánh giá rủi ro cấp tổ chức |
| Threat Intelligence | CTI Analyst, Threat Hunter | Nghiên cứu nhóm APT, xu hướng tấn công |

Khuyến nghị: học giai đoạn 0–3 chung cho mọi hướng; Blue Team là cửa vào thực tế nhất (nhiều việc entry-level), rồi rẽ nhánh ở giai đoạn 5.

## Giai đoạn 0–1: Nền tảng IT (3–4 tháng)

Không thể bảo vệ thứ mình không hiểu: 70% công việc bảo mật là hiểu sâu mạng và hệ điều hành.

### 1. Networking

- Mô hình OSI / TCP-IP; IPv4/IPv6, subnetting, CIDR, NAT
- Giao thức: ARP, DHCP, DNS, ICMP, TCP handshake, UDP, HTTP/HTTPS, TLS, SSH, SMTP, SMB, LDAP, Kerberos
- Thiết bị & kiến trúc: switch, router, VLAN, firewall, proxy, load balancer, VPN, DMZ, network segmentation
- Công cụ: Wireshark, tcpdump, nmap, netcat, dig, curl, traceroute
- Thực hành: capture và giải thích 1 phiên HTTP, DNS lookup, TLS handshake bằng Wireshark

### 2. Hệ điều hành

- **Linux**: filesystem, permission (chmod, SUID/SGID), user/group, process, systemd, cron, package manager, log trong /var/log, journalctl, iptables/nftables
- **Windows**: Registry, Services, Event Log (4624, 4625, 4688, 4720…), PowerShell, NTFS ACL, UAC, Group Policy
- **Active Directory**: domain, OU, GPO, Kerberos vs NTLM, trust — nền tảng bắt buộc cho cả Blue lẫn Red Team
- Ảo hóa & container: VirtualBox/VMware, Docker cơ bản

### 3. Lập trình & Scripting

- **Python** (ưu tiên số 1): requests, socket, scapy, parsing log, gọi API
- **Bash** và **PowerShell**: tự động hóa tác vụ quản trị và phân tích
- Đọc hiểu: JavaScript, SQL, PHP/Java (để hiểu lỗ hổng web); C/Assembly cơ bản nếu định làm malware analysis/exploit
- Git, regex, JSON/YAML

### Nguồn học gợi ý

- Professor Messer (Network+), Cisco Networking Academy, "Computer Networking: A Top-Down Approach"
- OverTheWire **Bandit** (Linux), TryHackMe path "Pre Security" / "Cyber Security 101"
- "Automate the Boring Stuff with Python", "Black Hat Python"

### Gate

- [ ] Tự dựng home lab: 1 Linux server, 1 Windows Server (AD domain), 1 Windows client, pfSense/OPNsense làm firewall
- [ ] Giải thích được mọi gói tin trong 1 PCAP ngắn
- [ ] Hoàn thành Bandit level 0–20
- [ ] Viết script Python quét port + parse log SSH đăng nhập thất bại

## Giai đoạn 2: Security Foundations & Quản trị rủi ro (2–3 tháng)

Đây là giai đoạn hình thành năng lực **đánh giá rủi ro** — kỹ năng phân biệt người làm bảo mật có trách nhiệm với người chỉ biết dùng tool.

### 1. Kiến thức cốt lõi

- **Cryptography ứng dụng**: symmetric (AES) vs asymmetric (RSA, ECC), hashing (SHA-2, bcrypt/Argon2), digital signature, PKI, certificate chain, TLS 1.3; lỗi hay gặp (ECB mode, hard-coded key, MD5 password). Theo dõi Post-Quantum Cryptography (ML-KEM, ML-DSA)
- **IAM**: MFA, SSO, OAuth 2.0/OIDC, SAML, RBAC/ABAC, least privilege, PAM, quản lý secret
- **Threat landscape**: malware (ransomware, infostealer, RAT), phishing/BEC, supply chain attack, social engineering, insider threat
- **Vulnerability management**: CVE, CVSS, EPSS, CISA KEV catalog, patch management, vòng đời lỗ hổng
- **Security controls**: preventive / detective / corrective; administrative / technical / physical

### 2. Quản trị rủi ro (Risk Management)

Quy trình chuẩn:

1. **Asset inventory** — liệt kê tài sản, xác định owner và mức độ quan trọng (crown jewels)
2. **Threat & vulnerability identification** — ai có thể tấn công, qua đường nào
3. **Risk analysis** — định tính (ma trận 5×5) hoặc định lượng (ALE = SLE × ARO; FAIR)
4. **Risk treatment** — Mitigate / Transfer / Avoid / Accept (có người ký chấp nhận)
5. **Monitor & review** — risk register cập nhật định kỳ, KRI theo dõi

Framework cần biết:

| Framework | Dùng để làm gì |
| --- | --- |
| NIST CSF 2.0 | Khung tổng thể: Govern, Identify, Protect, Detect, Respond, Recover |
| ISO/IEC 27001 & 27005 | ISMS và quản trị rủi ro an toàn thông tin, chuẩn quốc tế phổ biến ở VN |
| NIST SP 800-30 / 800-53 | Phương pháp đánh giá rủi ro / danh mục control |
| CIS Controls v8 | 18 nhóm control ưu tiên, thực tế cho doanh nghiệp nhỏ |
| MITRE ATT&CK | Tri thức về tactic/technique của kẻ tấn công |
| Pháp lý Việt Nam | Luật An toàn thông tin mạng, Luật An ninh mạng, quy định bảo vệ dữ liệu cá nhân, bảo đảm an toàn hệ thống theo cấp độ — kiểm tra văn bản hiện hành |

### 3. Threat Modeling

- STRIDE (Spoofing, Tampering, Repudiation, Information disclosure, DoS, Elevation of privilege)
- Vẽ Data Flow Diagram, xác định trust boundary; công cụ OWASP Threat Dragon / Microsoft Threat Modeling Tool
- Các phương pháp khác: PASTA, attack tree, LINDDUN (privacy)

### Nguồn học gợi ý

- Professor Messer Security+ (miễn phí), "Threat Modeling: Designing for Security" (Adam Shostack)
- Tài liệu NIST CSF 2.0 và CIS Controls (miễn phí)

### Gate

- [ ] Viết risk register 15–20 rủi ro cho 1 đồ án của bản thân (ví dụ hệ thống bán vé hoặc quản lý lớp học)
- [ ] Threat model STRIDE có DFD cho cùng hệ thống đó
- [ ] Map được 10 control CIS vào các rủi ro đã xác định
- [ ] (Tuỳ chọn) Thi CompTIA Security+

## Giai đoạn 3: Phòng thủ — Blue Team (4–5 tháng)

Giai đoạn rèn khả năng **phản ứng linh hoạt**: phát hiện sớm, khoanh vùng nhanh, khôi phục có kiểm soát.

### 1. Hardening & Security Architecture

- CIS Benchmarks cho Linux/Windows, tắt dịch vụ thừa, quản lý patch
- Network segmentation, firewall rule review, egress filtering, WAF
- EDR/XDR, email security (SPF, DKIM, DMARC), backup 3-2-1 bất biến (immutable)

### 2. Logging, SIEM & Detection Engineering

- Nguồn log quan trọng: Windows Event Log + **Sysmon**, Linux auditd, firewall/proxy, DNS, EDR, cloud audit log
- SIEM: **Splunk**, **Elastic/ELK**, Wazuh (miễn phí), Microsoft Sentinel
- Ngôn ngữ truy vấn: SPL, KQL, EQL
- Viết rule: **Sigma** (chuẩn chung), **YARA** (file/malware), Suricata/Snort (network)
- Detection-as-Code: rule trong Git, test bằng Atomic Red Team, đo coverage theo MITRE ATT&CK
- Giảm false positive: baseline hành vi, tuning, đánh giá chất lượng alert

### 3. Incident Response

Theo NIST SP 800-61: **Preparation → Detection & Analysis → Containment, Eradication & Recovery → Post-Incident Activity**.

- Viết playbook/runbook: phishing, ransomware, tài khoản bị chiếm, lộ dữ liệu, web shell
- Severity matrix, escalation path, kênh liên lạc out-of-band, thông báo theo quy định pháp lý
- Blameless postmortem: timeline, root cause, action items có owner và deadline
- Metrics: MTTD, MTTR, số alert/analyst, tỷ lệ true positive
- SOAR: tự động hóa enrichment và containment (Shuffle, TheHive + Cortex)

### 4. Digital Forensics & Malware Analysis cơ bản

- Disk/memory forensics: FTK Imager, Autopsy, **Volatility 3**, KAPE, Eric Zimmerman tools
- Chuỗi bằng chứng (chain of custody), timeline analysis
- Phân tích tĩnh/động trong sandbox cách ly: strings, PE header, Any.Run, REMnux, FLARE VM

### 5. Threat Hunting

- Hypothesis-driven hunting dựa trên ATT&CK và báo cáo CTI mới
- Pyramid of Pain: ưu tiên phát hiện TTP hơn IOC (hash, IP thay đổi rất nhanh)

### Lab & nguồn học

- TryHackMe **SOC Level 1 / Level 2**, Blue Team Labs Online, CyberDefenders, LetsDefend
- Splunk **Boss of the SOC** (BOTS) dataset, Detection Lab / GOAD cho môi trường AD
- SANS DFIR posters & cheat sheets, The DFIR Report (case study thực tế)

### Gate

- [ ] Triển khai Wazuh hoặc ELK + Sysmon trong home lab, thu log từ 3 máy
- [ ] Viết 10 Sigma rule, test bằng Atomic Red Team, ghi lại kết quả detect/miss
- [ ] Viết 3 IR playbook và 1 postmortem cho một sự cố giả lập
- [ ] Hoàn thành 10 challenge trên CyberDefenders/BTLO
- [ ] (Tuỳ chọn) Chứng chỉ BTL1, CySA+ hoặc TryHackMe SAL1

## Giai đoạn 4: Tấn công — Red Team / Pentest (4–5 tháng)

Mục đích không phải "hack" mà là chứng minh rủi ro thật bằng bằng chứng, rồi đề xuất khắc phục. Chỉ thực hành trên lab của bản thân hoặc nền tảng được phép; tấn công hệ thống không được ủy quyền là vi phạm pháp luật.

### 1. Quy trình pentest

1. **Pre-engagement**: scope, Rules of Engagement, hợp đồng ủy quyền bằng văn bản
2. **Reconnaissance**: OSINT, subdomain enumeration, port/service scanning
3. **Vulnerability analysis**: thủ công + scanner (Nessus, OpenVAS, Nuclei)
4. **Exploitation** → **Post-exploitation**: privilege escalation, lateral movement, persistence (chỉ trong scope)
5. **Reporting**: executive summary, finding theo CVSS, bằng chứng tái tạo, remediation cụ thể — đây là sản phẩm khách hàng thực sự trả tiền

### 2. Web Application Security (ưu tiên cao nhất)

- **OWASP Top 10**: Broken Access Control, Injection (SQLi, Command, SSTI), XSS, SSRF, Insecure Deserialization, Security Misconfiguration, Vulnerable Components…
- **OWASP API Security Top 10**: BOLA/IDOR, Broken Authentication, Mass Assignment
- JWT/OAuth attack, business logic flaw, race condition (liên quan trực tiếp hệ thống flash-sale)
- Công cụ: **Burp Suite**, ffuf, sqlmap, Nuclei

### 3. Network & Active Directory

- Enumeration: nmap, enum4linux, BloodHound, NetExec
- Kỹ thuật AD phổ biến: Kerberoasting, AS-REP Roasting, Pass-the-Hash, NTLM relay, lạm dụng ACL, ADCS misconfiguration
- Privilege escalation Linux/Windows (GTFOBins, LOLBAS, WinPEAS/LinPEAS)
- Framework: Metasploit, Impacket; C2 cơ bản (Sliver) cho red team lab

### 4. Mở rộng (tuỳ hướng)

- Mobile security: OWASP MASVS/MASTG, Frida, MobSF — tận dụng nền Android
- Wireless, social engineering (phishing simulation có ủy quyền), physical security
- Exploit development, reverse engineering (Ghidra, x64dbg)

### Lab & nguồn học

- **PortSwigger Web Security Academy** (miễn phí, tốt nhất cho web)
- Hack The Box (Academy + Labs), TryHackMe Jr Penetration Tester, VulnHub, GOAD (AD lab)
- OWASP Juice Shop, DVWA; "The Web Application Hacker's Handbook", HackTricks
- Bug bounty: HackerOne, Bugcrowd, Intigriti — đọc kỹ policy trước khi test

### Gate

- [ ] Hoàn thành toàn bộ lab Apprentice + Practitioner của PortSwigger cho 8 nhóm lỗ hổng chính
- [ ] Root 30+ máy HTB/THM (ít nhất 10 Windows/AD)
- [ ] Pentest trọn vẹn 1 đồ án của bản thân và viết báo cáo 15–25 trang
- [ ] (Tuỳ chọn) eJPT → PNPT/CPTS → OSCP

## Giai đoạn 5: Chuyên sâu (4–6 tháng, chọn 1–2 hướng)

Chọn chuyên ngành dựa trên thế mạnh hiện có: với nền Java/Android và các đồ án phần mềm, **AppSec/DevSecOps** và **Cloud Security** là lợi thế tự nhiên.

### A. Application Security & DevSecOps

- Secure SDLC, OWASP SAMM, OWASP ASVS làm checklist yêu cầu
- Secure coding Java/Spring: input validation, parameterized query, CSRF, session, Spring Security, xử lý secret
- Pipeline: **SAST** (Semgrep, SonarQube, CodeQL), **SCA** (Dependency-Check, Trivy, Snyk), **DAST** (OWASP ZAP), secret scanning (Gitleaks), IaC scanning (Checkov)
- Supply chain: SBOM (CycloneDX), ký artifact (Sigstore/cosign), SLSA
- Phương án so sánh: SAST bắt lỗi sớm nhưng nhiều false positive; DAST chính xác hơn nhưng chỉ chạy được khi app đã deploy — nên kết hợp cả hai

### B. Cloud & Container Security

- Shared Responsibility Model; IAM policy, least privilege, KMS, VPC, security group
- AWS: CloudTrail, GuardDuty, Security Hub, Config; Azure: Entra ID, Defender for Cloud
- Kubernetes: RBAC, NetworkPolicy, Pod Security Standards, admission control (Kyverno/OPA), runtime (Falco)
- CSPM/CNAPP, Terraform an toàn; benchmark CIS cho cloud
- Lab: **flAWS / flAWS2**, CloudGoat, Kubernetes Goat, TryHackMe/HTB cloud

### C. Threat Intelligence

- Vòng đời CTI: direction → collection → processing → analysis → dissemination
- Diamond Model, Cyber Kill Chain, ATT&CK Navigator; STIX/TAXII, MISP, OpenCTI
- Viết báo cáo CTI có khuyến nghị hành động cho từng đối tượng (SOC, lãnh đạo)

### D. GRC (Governance, Risk, Compliance)

- Xây ISMS theo ISO 27001: Statement of Applicability, chính sách, internal audit
- Business Impact Analysis, BCP/DRP, RTO/RPO, third-party risk management
- PCI DSS (thanh toán), SOC 2, GDPR và quy định bảo vệ dữ liệu cá nhân tại VN
- Kỹ năng mềm bắt buộc: trình bày rủi ro bằng ngôn ngữ kinh doanh (tiền, thời gian, uy tín)

### E. AI Security (mảng mới, nên theo dõi)

- OWASP Top 10 for LLM Applications: prompt injection, data leakage, excessive agency
- MITRE ATLAS, NIST AI RMF; bảo mật agent có quyền gọi tool, RAG, model supply chain
- AI dùng cho cả tấn công (phishing, deepfake) lẫn phòng thủ (triage alert, phân tích log)

### Gate (portfolio)

- [ ] Dự án 1: CI/CD pipeline DevSecOps hoàn chỉnh cho 1 đồ án Java, có security gate chặn build
- [ ] Dự án 2: Kiến trúc cloud an toàn bằng Terraform + báo cáo CSPM trước/sau
- [ ] Dự án 3: Home SOC hoàn chỉnh với dashboard + 20 detection rule có tài liệu
- [ ] Blog/GitHub: 10 bài write-up hoặc nghiên cứu

## Giai đoạn 6: Thích ứng liên tục, chứng chỉ & kế hoạch học

Mối đe dọa thay đổi hàng tuần, nên kỹ năng quan trọng nhất sau 2 năm là một **quy trình cập nhật có kỷ luật**, không phải một tool cụ thể.

### 1. Quy trình phản ứng mối đe dọa mới (khi có CVE/chiến dịch mới)

1. **Tiếp nhận**: nguồn tin cảnh báo (CISA KEV, vendor advisory, VNCERT/C, NCSC)
2. **Đánh giá ảnh hưởng**: hệ thống mình có dùng thành phần đó không? (cần asset inventory/SBOM) — CVSS + EPSS + có trong KEV không
3. **Kiểm soát tạm thời**: WAF rule, tắt tính năng, cô lập mạng
4. **Hunt**: có dấu hiệu đã bị khai thác trước đó chưa?
5. **Khắc phục**: patch theo SLA (ví dụ Critical trong 72h), xác minh lại
6. **Detection mới**: viết rule cho kỹ thuật đó, cập nhật playbook, báo cáo lên quản lý

### 2. Nguồn theo dõi hàng tuần

- Tin tức: BleepingComputer, The Hacker News, The Record, Krebs on Security
- Báo cáo kỹ thuật: The DFIR Report, Mandiant/Google Threat Intelligence, Microsoft Threat Intelligence, Unit 42, Kaspersky Securelist
- Cộng đồng: Reddit r/netsec, r/blueteamsec; podcast Darknet Diaries, Risky Business; cộng đồng CTF Việt Nam
- Thiết lập RSS reader (Feedly/Inoreader) và dành 2–3 giờ/tuần đọc + ghi chú

### 3. Chứng chỉ theo lộ trình

| Cấp | Blue Team | Red Team | Cloud / AppSec | GRC |
| --- | --- | --- | --- | --- |
| Entry | CompTIA Security+, BTL1 | eJPT | AWS Cloud Practitioner | ISC2 CC |
| Intermediate | CySA+, GCIH | PNPT, HTB CPTS, OSCP | AWS Security Specialty, CCSK | ISO 27001 Lead Implementer |
| Advanced | GCFA, GREM | OSEP, CRTO, OSWE | CCSP, CKS | CISSP, CISM, CISA |

Chứng chỉ mở cửa CV, nhưng portfolio và write-up mới chứng minh năng lực; kiểm tra phiên bản đề thi và giá hiện hành trên trang chính thức trước khi đăng ký.

### 4. Home lab chuẩn

- Máy chủ: PC 32 GB RAM hoặc cloud credit; hypervisor Proxmox/VMware
- Thành phần: pfSense/OPNsense, AD domain (DC + 2 client), Kali Linux, Wazuh/ELK, Security Onion, vài máy vulnerable
- Tài liệu hoá: sơ đồ mạng, IaC/Ansible để dựng lại nhanh; snapshot trước mỗi bài tập

### 5. Lịch học mẫu (12–15 giờ/tuần, song song việc học trên trường)

| Ngày | Thời lượng | Nội dung |
| --- | --- | --- |
| Thứ 2, 4 | 2 giờ/buổi | Lý thuyết giai đoạn hiện tại (khóa học, sách) |
| Thứ 3, 5 | 2 giờ/buổi | Lab thực hành (THM/HTB/PortSwigger) |
| Thứ 6 | 1 giờ | Đọc tin & báo cáo threat mới, ghi chú |
| Thứ 7 | 3 giờ | Dự án portfolio / home lab |
| Chủ nhật | 1–2 giờ | Viết write-up, ôn tập, lên kế hoạch tuần sau |

### 6. Kỹ năng mềm & trách nhiệm nghề nghiệp

- Viết báo cáo rõ ràng cho 2 đối tượng: kỹ thuật và lãnh đạo
- Bình tĩnh dưới áp lực, ghi log mọi hành động trong sự cố, biết escalate đúng lúc
- Đạo đức: chỉ test khi có ủy quyền, responsible disclosure, bảo mật dữ liệu khách hàng
- Tham gia CTF đều đặn (CTFtime, picoCTF, ASCIS, SVATTT) để rèn tư duy dưới áp lực thời gian

### Checklist sẵn sàng ứng tuyển vị trí đầu tiên

- [ ] Hoàn thành gate giai đoạn 0–3
- [ ] 1 chứng chỉ entry (Security+ hoặc BTL1/eJPT)
- [ ] GitHub có home lab, detection rule, script và ít nhất 1 báo cáo pentest mẫu
- [ ] 5–10 bài write-up công khai
- [ ] Trả lời được: "Chuyện gì xảy ra khi gõ URL vào trình duyệt?", "Xử lý alert đăng nhập bất thường thế nào?", "Đánh giá rủi ro của một CVE mới ra sao?"
