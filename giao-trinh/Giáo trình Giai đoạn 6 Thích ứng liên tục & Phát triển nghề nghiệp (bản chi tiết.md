# Giáo trình Giai đoạn 6: Thích ứng liên tục & Phát triển nghề nghiệp (bản chi tiết)

Nov 23, 2026 · @Huynh Gia Pho

Mối đe dọa thay đổi hàng tuần, nên kỹ năng quan trọng nhất sau 2 năm là một quy trình cập nhật có kỷ luật. Giai đoạn này kéo dài suốt sự nghiệp và nên bắt đầu song song từ Giai đoạn 2; mỗi module gồm lý thuyết, video, tài liệu, bài tập và tiêu chí đạt.

## Cách dùng giáo trình

Khác các giai đoạn trước, giai đoạn này không học theo tuần liên tục mà theo **nhịp đều đặn**: 20–30 phút/ngày, 2–3 giờ/tuần, 3–4 giờ/tháng, 1 ngày/quý.

### Mục tiêu đầu ra

1. Trả lời được 3 câu hỏi trong vài giờ khi có mối đe dọa mới: ta có bị ảnh hưởng không, đã bị khai thác chưa, làm gì ngay
2. Vận hành hệ thống theo dõi threat cá nhân không bị ngợp tin
3. Có bằng chứng năng lực công khai: write-up, CTF, bug bounty, đóng góp mã nguồn mở
4. Có lộ trình chứng chỉ và nghề nghiệp rõ ràng, sẵn sàng phỏng vấn
5. Hành nghề có đạo đức và trách nhiệm khi "sở hữu" một hệ thống

### Cấu trúc

| Module | Nhịp | Nội dung chính | Sản phẩm |
| --- | --- | --- | --- |
| 1. Phản ứng mối đe dọa mới | Mỗi tháng 1 bài tập | Quy trình 6 bước, flash alert | 12 bài tập/năm |
| 2. Theo dõi threat | Hàng ngày/tuần | RSS, báo cáo, cảnh báo tự động | Bản tóm tắt tuần |
| 3. Cộng đồng | Hàng tháng | CTF, bug bounty, mã nguồn mở, hội thảo | Write-up, report, PR |
| 4. Nghề nghiệp | Hàng quý | Chứng chỉ, CV, phỏng vấn | Portfolio, CV |
| 5. Kỹ năng mềm & đạo đức | Liên tục | Viết, giao tiếp rủi ro, đạo đức | Checklist trách nhiệm |

Mỗi module theo khuôn: **Lý thuyết cần nắm → Video → Đọc → Bài tập → Tiêu chí đạt**.

## Module 1 — Phản ứng mối đe dọa mới

Khi một CVE nghiêm trọng hoặc chiến dịch mới xuất hiện, mục tiêu là trả lời trong vài giờ: **Ta có bị ảnh hưởng không? Đã bị khai thác chưa? Làm gì ngay bây giờ?**

### Chương 1.1 — Quy trình 6 bước

**Lý thuyết cần nắm**

| Bước | Thời hạn mục tiêu | Hành động | Đầu ra |
| --- | --- | --- | --- |
| 1. Tiếp nhận & xác minh | ≤ 1 giờ | Đọc advisory gốc (vendor, CISA, NVD); kiểm tra KEV, EPSS, PoC công khai | Tóm tắt 5 dòng |
| 2. Đánh giá ảnh hưởng | ≤ 4 giờ | Tra asset inventory, SBOM, kết quả scan; mức độ lộ diện Internet | Danh sách tài sản + ưu tiên |
| 3. Kiểm soát tạm thời | ≤ 8 giờ | Workaround vendor, WAF virtual patch, tắt tính năng, cô lập mạng | Change record |
| 4. Hunt | Song song bước 3 | Tìm dấu hiệu khai thác trước đó theo IOC/TTP | Hunt report; thấy dấu hiệu → kích hoạt IR |
| 5. Khắc phục | Theo SLA (ví dụ KEV/Critical Internet-facing ≤ 72 giờ) | Patch, xác minh bằng scan lại | Bằng chứng đã vá |
| 6. Học & cải tiến | ≤ 1 tuần | Rule mới, cập nhật playbook, báo cáo lãnh đạo | Postmortem ngắn |

**Video**: [Professor Messer SY0-701](https://www.professormesser.com/security-plus/sy0-701/sy0-701-video/sy0-701-comptia-security-plus-course/) mục 4.3 (Analyzing Vulnerabilities, Vulnerability Remediation) — ôn lại

**Đọc**: [CISA KEV Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog), [FIRST EPSS](https://www.first.org/epss/), [CISA — Incident & Vulnerability Response Playbooks](https://www.cisa.gov/resources-tools/resources/federal-government-cybersecurity-incident-and-vulnerability-response-playbooks)

### Chương 1.2 — Template Flash Alert nội bộ

```
TIÊU ĐỀ: [Mức độ] <Tên lỗ hổng/chiến dịch> — <Sản phẩm bị ảnh hưởng>
THỜI ĐIỂM: <ngày giờ, múi giờ>       NGƯỜI PHỤ TRÁCH: <tên>

1. Tóm tắt (BLUF): <1–2 câu: chuyện gì, ta có bị ảnh hưởng không>
2. Bằng chứng bên ngoài: CVE / CVSS / EPSS / KEV / khai thác thực tế?
3. Tài sản bị ảnh hưởng: <số lượng, danh sách, Internet-facing?>
4. Hành động đã làm: <workaround, hunt, kết quả>
5. Hành động cần làm + owner + hạn: <...>
6. Độ tin cậy của đánh giá: <cao/trung bình/thấp> — điều còn chưa biết
7. Lần cập nhật tiếp theo: <thời điểm>
```

### Chương 1.3 — Học từ sự kiện lịch sử

**Đọc**: timeline của các sự kiện lớn trên trang CISA và vendor — Log4Shell ([CISA Apache Log4j guidance](https://www.cisa.gov/news-events/news/apache-log4j-vulnerability-guidance)), MOVEit, XZ Utils backdoor; [The DFIR Report](https://thedfirreport.com/) cho từng vụ xâm nhập cụ thể

**Bài tập**:

1. Mỗi tháng chọn 1 lỗ hổng lớn vừa vào CISA KEV, làm trọn 6 bước trên home lab (giả định lab là tổ chức của bạn)
2. Viết flash alert theo template cho lỗ hổng đó
3. Với 1 sự kiện lịch sử, tự hỏi: "nếu là mình, bước nào sẽ chậm nhất?" và viết cách rút ngắn

### Tiêu chí đạt Module 1

- [ ] 3 bài tập phản ứng 6 bước liên tiếp, mỗi bài có flash alert
- [ ] Thời gian từ lúc đọc tin đến có danh sách tài sản ảnh hưởng ≤ 4 giờ trong lab
- [ ] Script cảnh báo tự động khi KEV có sản phẩm trong danh sách của bạn (xem Module 2)

## Module 2 — Hệ thống theo dõi threat cá nhân

Mục tiêu: 20–30 phút/ngày, không bị ngợp tin nhưng không bỏ lỡ sự kiện quan trọng.

### Chương 2.1 — Nhịp độ & nguồn

| Nhịp | Thời lượng | Việc làm | Nguồn |
| --- | --- | --- | --- |
| Hàng ngày | 20–30 phút | Lướt tin, đánh dấu 1–3 mục đọc kỹ | [BleepingComputer](https://www.bleepingcomputer.com/), [The Hacker News](https://thehackernews.com/), [The Record](https://therecord.media/), [SecurityWeek](https://www.securityweek.com/), [CISA KEV](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) |
| Hàng tuần | 2–3 giờ | Đọc sâu 2–3 báo cáo, ghi TTP, viết tóm tắt | [The DFIR Report](https://thedfirreport.com/), [Google Threat Intelligence](https://cloud.google.com/blog/topics/threat-intelligence), [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/), [Unit 42](https://unit42.paloaltonetworks.com/), [Talos](https://blog.talosintelligence.com/), [Securelist](https://securelist.com/), [Elastic Security Labs](https://www.elastic.co/security-labs) |
| Hàng tháng | 3–4 giờ | Patch Tuesday, bài tập Module 1, cập nhật lab, 1 bài blog | [Microsoft MSRC Update Guide](https://msrc.microsoft.com/update-guide) |
| Hàng quý | 1 ngày | Đối chiếu kỹ năng với xu hướng | [Verizon DBIR](https://www.verizon.com/business/resources/reports/dbir/), [ENISA Threat Landscape](https://www.enisa.europa.eu/topics/cyber-threats/threat-landscape) |

Nguồn Việt Nam: [VNCERT/CC](https://vncert.vn/) và cảnh báo của cơ quan quản lý ATTT; blog kỹ thuật của các công ty bảo mật trong nước; cộng đồng CTF và nhóm ngành.

### Chương 2.2 — Video & podcast

**Video**: kênh [Antisyphon Training](https://www.youtube.com/@AntisyphonTraining) (webcast miễn phí hàng tuần), [Simply Cyber](https://www.youtube.com/c/GeraldAuger) (bản tin hàng ngày + nghề nghiệp), video hội thảo DEF CON, Black Hat, BSides trên YouTube

**Podcast**: [SANS Internet Stormcast](https://isc.sans.edu/podcast.html) (5 phút/ngày), [Risky Business](https://risky.biz/), [Darknet Diaries](https://darknetdiaries.com/)

### Chương 2.3 — Công cụ & tự động hóa

- RSS reader (Feedly, Inoreader hoặc tự host [FreshRSS](https://freshrss.org/)) chia thư mục: News / Technical / Vulnerabilities / Việt Nam
- Ghi chú Obsidian/Notion với template "Threat note": nguồn, ngày, tác nhân, TTP (ATT&CK ID), IOC, ý nghĩa, hành động
- Cảnh báo tự động cho stack công nghệ của bạn qua [GitHub Advisory Database](https://github.com/advisories), [OSV](https://osv.dev/)

**Ví dụ Python — báo khi CISA KEV có sản phẩm bạn dùng:**

```python
import json
import urllib.request
from urllib.error import URLError

KEV_URL = "https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json"
WATCHLIST = {"spring", "apache", "postgresql", "android", "nginx"}  # sản phẩm bạn quan tâm

def fetch_kev() -> list[dict]:
    try:
        with urllib.request.urlopen(KEV_URL, timeout=30) as resp:
            return json.load(resp).get("vulnerabilities", [])
    except (URLError, TimeoutError, json.JSONDecodeError) as e:
        # Lỗi mạng hoặc định dạng thay đổi: báo rõ thay vì im lặng bỏ qua
        raise SystemExit(f"Không tải được KEV: {e}")

def matches(vuln: dict) -> bool:
    text = f"{vuln.get('vendorProject', '')} {vuln.get('product', '')}".lower()
    return any(word in text for word in WATCHLIST)

if __name__ == "__main__":
    hits = [v for v in fetch_kev() if matches(v)]
    # Sắp xếp mới nhất trước theo ngày được thêm vào KEV
    for v in sorted(hits, key=lambda x: x.get("dateAdded", ""), reverse=True)[:20]:
        print(f"{v.get('dateAdded')}  {v.get('cveID')}  {v.get('vendorProject')} {v.get('product')}")
```

(Kiểm tra lại đường dẫn feed JSON trên trang CISA KEV trước khi dùng.)

### Tiêu chí đạt Module 2

- [ ] RSS ≥ 20 nguồn đã lọc, chia thư mục
- [ ] 12 tuần liên tiếp có bản tóm tắt tuần
- [ ] Script cảnh báo KEV chạy tự động hàng ngày (cron/GitHub Actions)

## Module 3 — Cộng đồng, CTF, bug bounty & mã nguồn mở

Tham gia cộng đồng giúp học nhanh hơn, có mạng lưới giới thiệu việc, và tạo bằng chứng công khai về năng lực.

### Chương 3.1 — CTF

| Loại | Nơi chơi | Rèn kỹ năng |
| --- | --- | --- |
| Jeopardy (web, crypto, pwn, rev, forensics) | [picoCTF](https://picoctf.org/), giải trên [CTFtime](https://ctftime.org/) | Giải quyết vấn đề dưới áp lực thời gian |
| Blue team / DFIR | [CyberDefenders](https://cyberdefenders.org/), [Blue Team Labs Online](https://blueteamlabs.online/) | Phân tích log, forensics |
| Sinh viên Việt Nam | SVATTT (Sinh viên với An toàn thông tin), ASCIS | Thi đấu đội, kết nối doanh nghiệp |

**Video**: [freeCodeCamp — Improve Cybersecurity Skills with CTFs (picoCTF walkthrough)](https://classcentral.com/classroom/freecodecamp-ethical-hacking-56987)

**Bài tập**: vào/lập CLB CTF của trường, thi ≥ 1 giải/tháng trên CTFtime, viết write-up sau mỗi giải (kể cả bài chưa giải được — đọc write-up người khác rồi tự làm lại).

### Chương 3.2 — Bug bounty & VDP

**Lý thuyết cần nắm**

- Nền tảng: [HackerOne](https://www.hackerone.com/), [Bugcrowd](https://www.bugcrowd.com/), [Intigriti](https://www.intigriti.com/), [YesWeHack](https://www.yeswehack.com/); VDP không trả thưởng nhưng phù hợp để bắt đầu
- Quy tắc: đọc kỹ policy (scope, out-of-scope, lỗi không nhận, giới hạn tốc độ), không truy cập dữ liệu người khác quá mức cần chứng minh, không DoS, không công bố trước khi được cho phép
- Chiến lược người mới: 1 chương trình scope rộng, tập trung 1 lớp lỗ hổng (IDOR/access control), hiểu sâu nghiệp vụ; vài tháng đầu có thể chưa có finding hợp lệ

**Video**: [HackerOne Hacker101](https://www.hacker101.com/) (bài giảng video + CTF miễn phí)

**Đọc**: sách *Real-World Bug Hunting* (Peter Yaworski); [HackerOne Hacktivity](https://hackerone.com/hacktivity) để đọc report đã công khai

### Chương 3.3 — Đóng góp mã nguồn mở & hội thảo

- Bắt đầu nhỏ: sửa tài liệu, dịch, thêm test cho công cụ bạn đã dùng
- Đóng góp detection: Sigma rule cho [SigmaHQ](https://github.com/SigmaHQ/sigma), Nuclei template, test cho [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team)
- Đóng góp nội dung: [OWASP Cheat Sheet Series](https://github.com/OWASP/CheatSheetSeries), OWASP WSTG/MASTG
- Hội thảo (video miễn phí): DEF CON, Black Hat, [BSides](https://bsides.org/), OWASP Global AppSec; trong nước: sự kiện VNISA và hội thảo ngành hằng năm

### Tiêu chí đạt Module 3 (12 tháng)

- [ ] ≥ 10 CTF, 10 write-up công khai
- [ ] ≥ 3 báo cáo lỗ hổng hợp lệ qua bug bounty/VDP
- [ ] ≥ 3 pull request được merge vào dự án bảo mật mã nguồn mở
- [ ] 1 talk hoặc workshop chia sẻ kiến thức

## Module 4 — Chứng chỉ, nghề nghiệp & phỏng vấn

Chứng chỉ là bộ lọc CV, portfolio mới là bằng chứng năng lực. Video chính: kênh [Simply Cyber](https://www.youtube.com/c/GeraldAuger) (nhiều video về lộ trình nghề, CV, phỏng vấn).

### Chương 4.1 — Chứng chỉ theo cấp và hướng

| Cấp | Blue Team | Red Team | AppSec | Cloud | GRC |
| --- | --- | --- | --- | --- | --- |
| Entry | CompTIA Security+, BTL1, ISC2 CC | eJPT | — | AWS Cloud Practitioner, AZ-900 | ISC2 CC |
| Intermediate | CySA+, GCIH, TryHackMe SAL1 | PNPT, HTB CPTS, OSCP | Burp Suite Certified Practitioner | AWS Security Specialty, AZ-500, CCSK | ISO 27001 Lead Implementer/Auditor |
| Advanced | GCFA, GREM, GCTI | OSEP, CRTO, OSWE | OSWE, GWEB | CCSP, CKS | CISSP, CISM, CISA, CRISC |

Nguyên tắc: ưu tiên chứng chỉ thi thực hành khi ngân sách có hạn; tìm voucher sinh viên; CISSP/CISM yêu cầu số năm kinh nghiệm — luôn kiểm tra điều kiện, giá và phiên bản đề trên trang chính thức.

**Đọc**: [Paul Jerimy — Security Certification Roadmap](https://pauljerimy.com/security-certification-roadmap/) (bản đồ tổng hợp chứng chỉ), [TryHackMe — SOC Analyst learning path to job ready](https://tryhackme.com/resources/blog/complete-soc-analyst-learning-path-from-beginner-to-job-ready-in-2026)

### Chương 4.2 — Lộ trình nghề nghiệp

1. **Intern / Fresher** (0–1 năm): SOC Analyst L1, Security Intern, Junior Pentester, Junior DevSecOps
2. **Junior–Mid** (1–3 năm): SOC L2/IR, Pentester, AppSec Engineer, Cloud Security Engineer
3. **Senior** (3–6 năm): Detection Engineering Lead, Senior Pentester, Security Architect
4. **Lead / Principal / Manager** (6+ năm): SOC Manager, Head of AppSec, Principal Engineer
5. **Executive**: CISO — kết hợp kỹ thuật, rủi ro, kinh doanh, lãnh đạo

Với nền kỹ sư phần mềm: con đường phổ biến là làm Software Engineer 1–2 năm kèm vai trò Security Champion, rồi chuyển sang AppSec/DevSecOps — hoặc vào thẳng SOC/Pentest junior nếu đã có portfolio mạnh.

**Đọc**: [NICE Framework (NIST)](https://niccs.cisa.gov/workforce-development/nice-framework) — mô tả chuẩn các vai trò an ninh mạng và kỹ năng cần có

### Chương 4.3 — Hồ sơ & phỏng vấn

- CV 1 trang: kỹ năng theo nhóm, 3–4 dự án với kết quả đo được, chứng chỉ, link GitHub/blog
- GitHub: home lab, detection rule, tool, IaC, báo cáo mẫu (đã loại thông tin nhạy cảm)
- LinkedIn: tiêu đề rõ hướng, chia sẻ write-up đều đặn

| Dạng câu hỏi | Ví dụ | Cách chuẩn bị |
| --- | --- | --- |
| Nền tảng | "Chuyện gì xảy ra khi gõ URL?", "Kerberos hoạt động thế nào?" | Ôn Giai đoạn 0–2, giải thích bằng lời đơn giản |
| Tình huống | "Alert đăng nhập từ quốc gia lạ lúc 3h sáng, bạn làm gì?" | Khung: xác minh → phạm vi → ngăn chặn → giao tiếp |
| Thực hành | Phân tích log/PCAP, review code, lab 2–4 giờ | Luyện BTLO/HTB có bấm giờ |
| Thiết kế | "Thiết kế xác thực cho app mobile banking" | Threat modeling, nêu ưu/nhược lựa chọn |
| Hành vi | "Kể về lần bạn mắc sai lầm" | Phương pháp STAR, chuẩn bị 5 câu chuyện |
| Cập nhật | "Gần đây bạn đọc về sự cố nào?" | Dùng bản tóm tắt tuần ở Module 2 |

**Bài tập**: phỏng vấn thử với bạn/mentor mỗi quý; ghi âm, tự nghe lại và sửa câu trả lời.

### Tiêu chí đạt Module 4

- [ ] Kế hoạch chứng chỉ 12 tháng có ngân sách và lịch thi
- [ ] CV + GitHub + LinkedIn sẵn sàng
- [ ] Trả lời trơn tru 6 dạng câu hỏi trong bảng

## Module 5 — Kỹ năng mềm, đạo đức & trách nhiệm nghề nghiệp

Người chịu trách nhiệm bảo vệ hệ thống được tin tưởng nhờ phán đoán, sự minh bạch và đạo đức — không chỉ nhờ kỹ thuật.

### Chương 5.1 — Kỹ năng mềm cốt lõi

- **Viết**: báo cáo hai tầng (lãnh đạo / kỹ thuật), BLUF, số liệu cụ thể, khuyến nghị hành động được
- **Giao tiếp rủi ro**: dịch kỹ thuật sang tiền, thời gian, uy tín, nghĩa vụ pháp lý; đưa lựa chọn thay vì chỉ nói "không"
- **Làm việc với dev/ops**: hiểu áp lực deadline, đề xuất fix cụ thể, tự động hóa thay vì thêm thủ tục
- **Bình tĩnh dưới áp lực**: ghi lại mọi hành động, không đoán, escalate sớm khi vượt thẩm quyền
- **Học có hệ thống & dạy lại**: thừa nhận "tôi chưa biết, tôi sẽ kiểm tra"
- **Phòng burnout**: ca trực SOC và sự cố kéo dài gây mệt mỏi — đặt giới hạn thời gian học, nghỉ ngơi đều

**Đọc**: [Google SRE Book — Postmortem Culture](https://sre.google/sre-book/postmortem-culture/) (văn hóa không đổ lỗi), [Google Technical Writing courses](https://developers.google.com/tech-writing) (miễn phí)

**Bài tập**: viết lại 1 báo cáo cũ của bạn thành 2 phiên bản: 1 trang cho lãnh đạo và bản kỹ thuật đầy đủ.

### Chương 5.2 — Đạo đức nghề nghiệp

- Chỉ kiểm thử khi có ủy quyền bằng văn bản, đúng phạm vi
- Quyền truy cập đặc quyền (admin, log, email người khác) chỉ dùng cho công việc được giao
- Responsible disclosure; không bán hoặc lạm dụng lỗ hổng
- Minh bạch khi mắc lỗi — báo sớm và cùng khắc phục

**Đọc**: [ISC2 Code of Ethics](https://www.isc2.org/Ethics), [ISACA Code of Professional Ethics](https://www.isaca.org/credentialing/code-of-professional-ethics), [CISA — Coordinated Vulnerability Disclosure](https://www.cisa.gov/coordinated-vulnerability-disclosure-process)

### Chương 5.3 — Trách nhiệm khi "sở hữu" một hệ thống

- [ ] Biết hệ thống có gì (asset inventory, data flow, owner)
- [ ] Biết rủi ro lớn nhất và ai đã chấp nhận chúng
- [ ] Biết khi có chuyện thì phát hiện bằng gì (log, alert, ai trực)
- [ ] Có playbook và đã diễn tập ít nhất 1 lần/năm
- [ ] Backup đã test restore
- [ ] Báo cáo định kỳ cho lãnh đạo về tình trạng và xu hướng
- [ ] Có người dự phòng hiểu hệ thống (không phụ thuộc 1 người)

**Bài tập**: áp checklist trên cho home lab và 1 đồ án của bạn; mỗi mục chưa đạt → 1 việc cần làm có hạn.

## Kế hoạch 12 tháng & tự đánh giá

### Kế hoạch 12 tháng sau roadmap

| Quý | Trọng tâm kỹ thuật | Cộng đồng | Nghề nghiệp |
| --- | --- | --- | --- |
| Q1 | Hoàn thiện portfolio Giai đoạn 5; 3 bài tập phản ứng threat | 3 CTF, 3 write-up | CV, LinkedIn, nộp đơn thực tập/fresher |
| Q2 | Chứng chỉ intermediate track chính | 1 report VDP, 1 PR mã nguồn mở | Phỏng vấn thử với mentor |
| Q3 | Học sâu track phụ; tự động hóa lab bằng IaC | 3 CTF, SVATTT/ASCIS nếu còn là sinh viên | Bắt đầu công việc/thực tập |
| Q4 | Dự án nghiên cứu cá nhân (ví dụ AI security hoặc detection cho 1 họ malware) | 1 lightning talk, 2 PR | Đánh giá năm, chọn chứng chỉ advanced |

### Chỉ số tự theo dõi hàng tháng

- Giờ học thực tế so với kế hoạch
- Số lab/máy/challenge hoàn thành
- Số bài viết công khai
- Số detection/tool/PR tạo ra
- 1 điều mới về threat landscape bạn giải thích được cho người khác

### Câu hỏi tự đánh giá hàng quý

1. Một CVE Critical vừa vào KEV cho sản phẩm bạn dùng — bạn làm gì trong 4 giờ đầu?
2. 3 xu hướng tấn công nổi bật quý này là gì, và hệ thống của bạn đã có detection cho chúng chưa?
3. Kỹ năng nào trong JD vị trí mơ ước của bạn mà bạn chưa có bằng chứng trên portfolio?
4. Bạn đã chia sẻ gì cho cộng đồng trong quý?
5. Checklist "sở hữu hệ thống" còn mục nào chưa đạt?

### Tiêu chí hoàn thành năm đầu

- [ ] 12 bài tập phản ứng mối đe dọa mới
- [ ] 52 bản tóm tắt tuần (cho phép thiếu tối đa 8)
- [ ] ≥ 10 write-up, ≥ 3 report bug bounty/VDP, ≥ 3 PR
- [ ] 1 chứng chỉ intermediate
- [ ] 1 vị trí thực tập hoặc công việc trong ngành

## Nguồn tham khảo

Các link đánh dấu (✓) đã được kiểm tra qua tìm kiếm ngày 23/11/2026; các link còn lại là trang chính thức của tổ chức/dự án, nên mở lại để xác nhận trước khi dùng.

### Video & khóa học

| Nguồn | Dùng cho |
| --- | --- |
| [Professor Messer SY0-701](https://www.professormesser.com/security-plus/sy0-701/sy0-701-video/sy0-701-comptia-security-plus-course/) ✓ | Module 1 |
| [Simply Cyber — Gerald Auger (YouTube)](https://www.youtube.com/c/GeraldAuger) ✓, [SimplyCyber.io](https://SimplyCyber.io) ✓ | Module 2, 4 |
| [TryHackMe — SOC Analyst learning path to job ready](https://tryhackme.com/resources/blog/complete-soc-analyst-learning-path-from-beginner-to-job-ready-in-2026) ✓ | Module 4 |
| [freeCodeCamp — Ethical Hacking playlist (có picoCTF walkthrough)](https://classcentral.com/classroom/freecodecamp-ethical-hacking-56987) ✓ | Module 3 |
| [Antisyphon Training (YouTube)](https://www.youtube.com/@AntisyphonTraining) | Module 2 |
| [HackerOne Hacker101](https://www.hacker101.com/) | Module 3 |
| [Google Technical Writing courses](https://developers.google.com/tech-writing) | Module 5 |

### Cảnh báo, lỗ hổng & báo cáo

| Nguồn | Loại |
| --- | --- |
| [CISA KEV](https://www.cisa.gov/known-exploited-vulnerabilities-catalog), [CISA Advisories](https://www.cisa.gov/news-events/cybersecurity-advisories), [NVD](https://nvd.nist.gov/), [FIRST EPSS](https://www.first.org/epss/), [GitHub Advisory Database](https://github.com/advisories), [OSV](https://osv.dev/), [Microsoft MSRC](https://msrc.microsoft.com/update-guide), [VNCERT/CC](https://vncert.vn/) | Cảnh báo & lỗ hổng |
| [BleepingComputer](https://www.bleepingcomputer.com/), [The Hacker News](https://thehackernews.com/), [The Record](https://therecord.media/), [SecurityWeek](https://www.securityweek.com/) | Tin tức |
| [The DFIR Report](https://thedfirreport.com/), [Google Threat Intelligence](https://cloud.google.com/blog/topics/threat-intelligence), [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/), [Unit 42](https://unit42.paloaltonetworks.com/), [Cisco Talos](https://blog.talosintelligence.com/), [Securelist](https://securelist.com/), [Elastic Security Labs](https://www.elastic.co/security-labs) | Báo cáo kỹ thuật |
| [Verizon DBIR](https://www.verizon.com/business/resources/reports/dbir/), [ENISA Threat Landscape](https://www.enisa.europa.eu/topics/cyber-threats/threat-landscape) | Báo cáo năm |
| [SANS Internet Stormcast](https://isc.sans.edu/podcast.html), [Risky Business](https://risky.biz/), [Darknet Diaries](https://darknetdiaries.com/) | Podcast |

### Cộng đồng, CTF & bug bounty

| Nguồn | Loại |
| --- | --- |
| [CTFtime](https://ctftime.org/), [picoCTF](https://picoctf.org/), [CyberDefenders](https://cyberdefenders.org/), [Blue Team Labs Online](https://blueteamlabs.online/) | CTF |
| [HackerOne](https://www.hackerone.com/), [Bugcrowd](https://www.bugcrowd.com/), [Intigriti](https://www.intigriti.com/), [YesWeHack](https://www.yeswehack.com/) | Bug bounty |
| [SigmaHQ](https://github.com/SigmaHQ/sigma), [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team), [OWASP Cheat Sheet Series](https://github.com/OWASP/CheatSheetSeries), [BSides](https://bsides.org/) | Mã nguồn mở & hội thảo |

### Nghề nghiệp & đạo đức

| Nguồn | Dùng cho |
| --- | --- |
| [Security Certification Roadmap (Paul Jerimy)](https://pauljerimy.com/security-certification-roadmap/) | Chọn chứng chỉ |
| [NICE Framework](https://niccs.cisa.gov/workforce-development/nice-framework) | Vai trò & kỹ năng |
| [ISC2 Code of Ethics](https://www.isc2.org/Ethics), [ISACA Code of Professional Ethics](https://www.isaca.org/credentialing/code-of-professional-ethics), [CISA Coordinated Vulnerability Disclosure](https://www.cisa.gov/coordinated-vulnerability-disclosure-process) | Đạo đức |
| [Google SRE Book — Postmortem Culture](https://sre.google/sre-book/postmortem-culture/) | Văn hóa học từ sự cố |

### Sách

| Sách | Tác giả |
| --- | --- |
| *Cybersecurity Career Master Plan* | Gerald Auger và cộng sự |
| *Hack the Cybersecurity Interview* | Ken Underhill và cộng sự |
| *Real-World Bug Hunting* | Peter Yaworski |
| *The Cuckoo's Egg* | Cliff Stoll |
| *Sandworm* | Andy Greenberg |
