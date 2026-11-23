# Giáo trình Giai đoạn 0–1: Nền tảng IT cho An ninh mạng

Nov 23, 2026 · @Huynh Gia Pho

Không thể bảo vệ thứ mình không hiểu: 70% công việc bảo mật là hiểu sâu mạng và hệ điều hành. Giáo trình này dẫn bạn qua 5 module trong 16 tuần, với mỗi chương gồm lý thuyết, video, tài liệu đọc, lab và tiêu chí đạt.

## Cách dùng giáo trình

Học 12–15 giờ/tuần trong 16 tuần; mỗi chương theo vòng **Xem video → Đọc tài liệu → Làm lab → Ghi chú → Tự kiểm tra**. Tỷ lệ khuyến nghị: 30% lý thuyết, 70% thực hành.

### Mục tiêu đầu ra

Kết thúc giai đoạn, bạn phải làm được:

1. Giải thích đường đi của một request từ trình duyệt đến server qua từng tầng (DNS, ARP, TCP, TLS, HTTP)
2. Chia subnet nhẩm trong 60 giây và thiết kế mạng có VLAN/DMZ
3. Đọc và phân tích một file PCAP bằng Wireshark, phát hiện traffic bất thường
4. Quản trị Linux qua dòng lệnh: user, permission, service, log, firewall
5. Quản trị Windows + Active Directory: tạo domain, GPO, đọc Event Log bảo mật
6. Tự dựng home lab nhiều máy ảo có firewall riêng
7. Viết script Python/Bash/PowerShell tự động hóa việc quét, phân tích log

### Cấu trúc

| Module | Tuần | Nội dung chính | Sản phẩm nộp |
| --- | --- | --- | --- |
| 1. Networking | 1–5 | OSI/TCP-IP, IP, subnetting, giao thức, thiết bị, Wireshark | Báo cáo phân tích 3 PCAP |
| 2. Linux | 6–8 | Shell, filesystem, permission, process, service, log, firewall | Hoàn thành Bandit 0–20, server được hardening |
| 3. Windows & AD | 9–11 | Registry, Event Log, PowerShell, AD, Kerberos, GPO | AD domain lab + báo cáo Event ID |
| 4. Ảo hóa & Home Lab | 12 (+ rải rác từ tuần 1) | Hypervisor, network ảo, Docker, pfSense | Sơ đồ + tài liệu lab |
| 5. Scripting | 13–15 (+ mỗi tuần 1 bài nhỏ) | Python, Bash, PowerShell, Git, regex | 5 tool nhỏ trên GitHub |
| Kiểm tra | 16 | Bài tổng hợp | Capstone mini |

### Quy ước ghi chú

- Tạo repo GitHub `security-foundations-notes`, mỗi chương một file Markdown: khái niệm, lệnh đã dùng, ảnh chụp, câu hỏi chưa hiểu
- Dùng Anki cho port, Event ID, lệnh Linux — ôn 10 phút/ngày
- Mỗi lab ghi theo mẫu: Mục tiêu → Môi trường → Các bước → Kết quả → Ý nghĩa bảo mật

### Cột "Góc nhìn bảo mật"

Mỗi chương kết thúc bằng phần này: kẻ tấn công lạm dụng kiến thức đó ra sao và người phòng thủ quan sát ở đâu. Đây là cầu nối sang giai đoạn 2–4.

## Module 1 — Networking (Tuần 1–5)

Module quan trọng nhất: mọi tấn công và phòng thủ đều diễn ra trên mạng. Video chính: [Professor Messer N10-009 Network+](https://www.professormesser.com/network-plus/n10-009/n10-009-video/n10-009-training-course/) (87 video, \~13 giờ, miễn phí); video bổ trợ: [freeCodeCamp Computer Networking Fundamentals](https://www.freecodecamp.org/news/computer-networking-fundamentals/) (12 giờ).

### Chương 1.1 — Mô hình OSI và TCP/IP (Tuần 1)

**Lý thuyết cần nắm**

| Tầng OSI | Tầng TCP/IP | PDU | Ví dụ giao thức/thiết bị | Tấn công điển hình |
| --- | --- | --- | --- | --- |
| 7 Application | Application | Data | HTTP, DNS, SMTP, SSH | SQLi, XSS, DNS spoofing |
| 6 Presentation | Application | Data | TLS, encoding, compression | SSL stripping, downgrade |
| 5 Session | Application | Data | NetBIOS, RPC | Session hijacking |
| 4 Transport | Transport | Segment/Datagram | TCP, UDP | SYN flood, port scan |
| 3 Network | Internet | Packet | IP, ICMP, router | IP spoofing, ICMP tunneling |
| 2 Data Link | Link | Frame | Ethernet, ARP, switch, VLAN | ARP spoofing, MAC flooding, VLAN hopping |
| 1 Physical | Link | Bit | Cáp, Wi-Fi, hub | Wiretapping, jamming |

- Encapsulation / decapsulation: header được thêm vào ở mỗi tầng khi gửi, bóc ra khi nhận
- MAC address (48-bit, OUI) vs IP address; unicast, broadcast, multicast

**Video**: Professor Messer mục 1.1 (OSI Model); freeCodeCamp [How does the internet work?](https://www.freecodecamp.org/news/how-does-the-internet-work/) (\~2 giờ, dành cho người mới)

**Đọc**: Kurose & Ross, *Computer Networking: A Top-Down Approach*, chương 1

**Lab**: Cài Wireshark, mở 1 trang web, lọc `http || dns`, xác định từng tầng header trong 1 gói tin (Ethernet → IP → TCP → HTTP).

### Chương 1.2 — IP Addressing & Subnetting (Tuần 1–2)

**Lý thuyết cần nắm**

- IPv4 32-bit, nhị phân ↔ thập phân; subnet mask, CIDR (/8, /16, /24, /26…)
- Địa chỉ private (RFC 1918): 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16; loopback 127.0.0.0/8; APIPA 169.254.0.0/16
- Công thức: số host = 2^(32 − prefix) − 2; block size = 256 − giá trị octet của mask
- 7 thuộc tính mỗi bài subnet: network ID, broadcast, first/last host, số host, mask, CIDR
- VLSM, supernetting/summarization; NAT/PAT
- IPv6: 128-bit, viết tắt, link-local fe80::/10, SLAAC, NDP (thay ARP)

**Ví dụ giải mẫu**: 192.168.10.77/27 → block size 32 → network 192.168.10.64, broadcast 192.168.10.95, host 192.168.10.65–94, 30 host.

**Video**: [Practical Networking — Subnetting Mastery](https://www.practicalnetworking.net/?p=2110) (giải mọi bài trong 60 giây với cheat sheet); Professor Messer mục 1.7–1.8 (IPv4/IPv6)

**Lab**: Giải 50 bài trên subnettingpractice.com; dùng `ipcalc` (Linux) kiểm tra kết quả; thiết kế VLSM cho công ty 4 phòng ban (120, 60, 25, 10 host) từ 172.16.0.0/24.

### Chương 1.3 — Giao thức cốt lõi (Tuần 2–3)

| Giao thức | Port | Chức năng | Điểm cần hiểu cho bảo mật |
| --- | --- | --- | --- |
| ARP | — | IP → MAC | Không xác thực → ARP spoofing/MITM |
| DHCP | UDP 67/68 | Cấp IP (DORA) | Rogue DHCP, DHCP starvation |
| DNS | UDP/TCP 53 | Tên miền → IP | Record A, AAAA, MX, TXT, CNAME, PTR; DNS tunneling, cache poisoning |
| ICMP | — | ping, traceroute | ICMP tunneling, recon |
| TCP | — | 3-way handshake, flag SYN/ACK/FIN/RST | SYN scan, SYN flood, session hijack |
| UDP | — | Không kết nối | Amplification DDoS |
| HTTP/HTTPS | 80/443 | Web; method, status code, header, cookie | Nền tảng cho web security |
| TLS | 443 | Mã hóa, certificate | Handshake, SNI, cert validation |
| SSH | 22 | Remote shell | Brute force, key-based auth |
| FTP / Telnet | 21 / 23 | Legacy | Plaintext credential |
| SMTP/IMAP/POP3 | 25/143/110 | Email | Spoofing → SPF/DKIM/DMARC |
| SMB | 445 | File share Windows | EternalBlue, relay attack |
| RDP | 3389 | Remote desktop | Brute force, BlueKeep |
| LDAP / Kerberos | 389 / 88 | Directory, auth AD | Nền tảng Module 3 |
| SNMP / NTP / Syslog | 161 / 123 / 514 | Quản trị, đồng bộ giờ, log | Community string mặc định; giờ sai làm hỏng điều tra |

**Video**: Professor Messer mục 1.4 (Common Ports) và 1.5–1.6

**Đọc**: Kurose & Ross chương 2–3; RFC 793/9293 (TCP) phần state diagram; Cloudflare Learning Center (DNS, TLS, DDoS)

**Lab**:

1. `dig`/`nslookup` các record của 1 domain; trace đệ quy bằng `dig +trace`
2. Capture TCP handshake và teardown, vẽ lại sequence/ack number
3. `curl -v` một trang HTTPS, đọc TLS handshake và header
4. Ghi nhớ 25 port phổ biến bằng Anki

### Chương 1.4 — Thiết bị, Routing & Kiến trúc mạng (Tuần 3–4)

- Switch (MAC table), VLAN & 802.1Q trunk, STP; router, routing table, static route, OSPF/BGP ở mức khái niệm
- Firewall: stateless vs stateful, NGFW; ACL; proxy/reverse proxy; load balancer; IDS vs IPS
- Kiến trúc: DMZ, segmentation, three-tier, VPN (IPsec, SSL VPN, WireGuard), Wi-Fi (WPA2/WPA3, 802.1X)
- Mạng cloud ở mức cơ bản: VPC, subnet public/private, security group

**Video**: Professor Messer mục 1.6, 2.1–2.3, 4.1; [freeCodeCamp Network Engineering course](https://www.freecodecamp.org/news/free-computer-networking-course/) (9 giờ, Brian Ferrill)

**Lab**: Cài Cisco Packet Tracer (miễn phí qua Cisco Networking Academy); dựng mạng 2 VLAN + router-on-a-stick + ACL chặn VLAN Guest truy cập VLAN Server.

### Chương 1.5 — Phân tích traffic với Wireshark & công cụ mạng (Tuần 4–5)

- Display filter: `ip.addr==`, `tcp.port==`, `http.request`, `dns.qry.name contains`, `tcp.flags.syn==1 && tcp.flags.ack==0`
- Statistics → Conversations, Protocol Hierarchy, Follow TCP Stream, Export Objects
- tcpdump: `tcpdump -i eth0 -nn port 53 -w dns.pcap`
- nmap cơ bản (chỉ trên lab của mình): `-sn`, `-sS`, `-sV`, `-O`, `-p-`; netcat; traceroute; `ss -tulpn` / `netstat -ano`

**Đọc**: Wireshark User's Guide; Chris Sanders, *Practical Packet Analysis* (3rd ed.)

**Lab**:

1. Tải PCAP mẫu từ Wireshark SampleCaptures, phân tích 1 phiên FTP lộ mật khẩu
2. Làm 2 bài trên malware-traffic-analysis.net (mức dễ) — tìm IP nạn nhân, domain độc, file tải về
3. TryHackMe phòng Wireshark: The Basics, Nmap

### Góc nhìn bảo mật — Module 1

- Kẻ tấn công: recon bằng port scan/DNS, MITM qua ARP, exfiltration qua DNS/ICMP, lợi dụng giao thức plaintext
- Người phòng thủ: segmentation, egress filtering, giám sát DNS log, IDS (Suricata/Zeek), mã hóa mọi kênh

### Tiêu chí đạt Module 1

- [ ] Giải đúng 10/10 bài subnet, mỗi bài ≤ 60 giây
- [ ] Kể được port + chức năng của 25 dịch vụ phổ biến
- [ ] Giải thích được "chuyện gì xảy ra khi gõ https://example.com" qua đủ DNS, ARP, TCP, TLS, HTTP
- [ ] Nộp báo cáo phân tích 3 PCAP (mỗi báo cáo 1–2 trang)

## Module 2 — Linux (Tuần 6–8)

Phần lớn server, container, thiết bị mạng và công cụ bảo mật chạy trên Linux, nên mục tiêu là thao tác hoàn toàn bằng dòng lệnh. Nguồn chính: [Linux Journey](https://labex.io/linuxjourney) (tương tác, miễn phí), [MIT Missing Semester](https://missing.csail.mit.edu/) (shell, scripting, Git, video YouTube), [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) (wargame).

Môi trường: cài Ubuntu Server LTS và Kali Linux trên VirtualBox/VMware (xem Module 4), hoặc WSL2 trên Windows để làm nhanh.

### Chương 2.1 — Shell & Filesystem (Tuần 6)

- Cấu trúc FHS: `/etc` (cấu hình), `/var/log` (log), `/home`, `/root`, `/tmp`, `/proc`, `/dev`, `/usr/bin`, `/opt`
- Điều hướng: `pwd`, `ls -la`, `cd`, `find / -name x 2>/dev/null`, `locate`, `which`
- File: `cat`, `less`, `head/tail -f`, `cp`, `mv`, `rm`, `ln -s`, `file`, `stat`
- Text processing (cực quan trọng cho phân tích log): `grep -Ei`, `cut`, `sort | uniq -c | sort -nr`, `awk`, `sed`, `tr`, `wc`, `xargs`
- Redirection & pipe: `>`, `>>`, `2>&1`, `|`, `tee`; biến môi trường, `$PATH`, `.bashrc`, alias
- Trợ giúp: `man`, `--help`, [explainshell.com](https://explainshell.com/)

**Ví dụ**: top 10 IP brute-force SSH:

```bash
grep "Failed password" /var/log/auth.log \
  | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr | head
```

**Video**: MIT Missing Semester bài 1–2 (The Shell, Shell Tools & Scripting), bài 4 (Data Wrangling)

**Lab**: Bandit level 0–12; Linux Journey mục Getting Started, Command Line, Text-Fu.

### Chương 2.2 — User, Group & Permission (Tuần 6–7)

- `/etc/passwd`, `/etc/shadow`, `/etc/group`; `useradd`, `usermod -aG`, `passwd`, `id`, `su`, `sudo`, `/etc/sudoers` (`visudo`)
- Permission `rwx`, octal (755, 644, 600), `chmod`, `chown`, `umask`
- Special bit: **SUID**, SGID, sticky bit (`/tmp`) — tìm file SUID: `find / -perm -4000 -type f 2>/dev/null`
- ACL (`getfacl`, `setfacl`), capabilities (`getcap -r /`)
- SSH: key-based auth, `~/.ssh/authorized_keys`, `sshd_config` (tắt `PermitRootLogin`, `PasswordAuthentication no`)

**Lab**: Bandit level 13–20; tạo 3 user với quyền khác nhau, cấu hình sudo chỉ cho phép 1 lệnh; cấu hình SSH bằng key.

### Chương 2.3 — Process, Service & Package (Tuần 7)

- Process: `ps aux`, `top/htop`, `pstree`, `kill -9`, `nice`, `/proc/<pid>/`, `lsof -i`
- systemd: `systemctl status|start|enable`, unit file, `journalctl -u ssh --since "1 hour ago"`
- Lập lịch: `crontab -e`, `/etc/cron.*`, systemd timer
- Package: `apt`, `dpkg -l`, `dnf/rpm`; kiểm tra nguồn repository
- Boot process: BIOS/UEFI → GRUB → kernel → systemd

**Lab**: viết 1 service systemd tự khởi động script Python; tạo cron job backup `/etc` mỗi ngày.

### Chương 2.4 — Networking, Log & Firewall trên Linux (Tuần 8)

- Network: `ip a`, `ip route`, `ss -tulpn`, `/etc/hosts`, `/etc/resolv.conf`, netplan/NetworkManager, `curl`, `wget`, `nc`, `tcpdump`
- Log: `/var/log/auth.log` (Debian/Ubuntu) hoặc `/var/log/secure` (RHEL), `syslog`, `journald`, rsyslog gửi log tập trung
- auditd: rule theo dõi `/etc/passwd`, lệnh `execve`
- Firewall: `ufw`, `iptables`, `nftables` (chain INPUT/OUTPUT/FORWARD, policy DROP mặc định)
- Hardening: cập nhật tự động, tắt dịch vụ thừa, fail2ban, CIS Benchmark Ubuntu, Lynis audit

**Lab**:

1. Hardening 1 Ubuntu Server, chạy `lynis audit system` trước/sau, ghi lại điểm
2. Cấu hình ufw chỉ mở 22 (từ 1 IP) và 443
3. Cài fail2ban, dùng máy Kali brute-force SSH chính server của mình (Hydra), quan sát log và ban
4. TryHackMe: Linux Fundamentals Part 1–3

### Góc nhìn bảo mật — Module 2

- Kẻ tấn công: privilege escalation qua SUID/sudo sai cấu hình (tham khảo [GTFOBins](https://gtfobins.github.io/)), cron job ghi được, xóa log, persistence qua `.bashrc`/cron/systemd
- Người phòng thủ: least privilege, auditd, gửi log ra server tập trung (kẻ tấn công khó xóa), giám sát file integrity (AIDE)

### Tiêu chí đạt Module 2

- [ ] Hoàn thành Bandit level 0–20 và viết write-up ngắn mỗi level
- [ ] Viết one-liner trích top IP, top user, khoảng thời gian từ auth.log
- [ ] Server Ubuntu được hardening, điểm Lynis tăng rõ rệt, có tài liệu từng thay đổi
- [ ] Giải thích được vì sao SUID trên `find` hoặc `vim` là nguy hiểm

## Module 3 — Windows & Active Directory (Tuần 9–11)

Hầu hết doanh nghiệp quản lý danh tính bằng Active Directory, và AD là mục tiêu chính trong các vụ ransomware. Nguồn chính: [Microsoft Learn](https://learn.microsoft.com/) (tài liệu gốc), TryHackMe path Windows, [Ultimate Windows Security — Event ID Encyclopedia](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/).

Môi trường: tải bản Evaluation miễn phí (180 ngày) của Windows Server và Windows Enterprise từ Microsoft Evaluation Center.

### Chương 3.1 — Kiến trúc Windows (Tuần 9)

- Tiến trình hệ thống quan trọng: `System`, `smss.exe`, `csrss.exe`, `wininit.exe`, `services.exe`, `lsass.exe` (giữ credential), `svchost.exe`, `explorer.exe` — biết parent/child chuẩn để phát hiện bất thường
- Registry: hive HKLM, HKCU; khóa persistence `Run`, `RunOnce`, Services
- Services, Scheduled Tasks, WMI
- NTFS permission, ACL, Alternate Data Streams; UAC, integrity level; tài khoản SYSTEM, Administrator, local vs domain account
- SAM, LSASS, NTLM hash; Windows Defender, Firewall, BitLocker
- Công cụ Sysinternals: Process Explorer, Autoruns, Procmon, TCPView

**Lab**: dùng Autoruns liệt kê mọi điểm tự khởi động; Process Explorer kiểm tra chữ ký số và parent process; TryHackMe Windows Fundamentals 1–3.

### Chương 3.2 — PowerShell (Tuần 9–10)

- Cú pháp Verb-Noun, pipeline đối tượng, `Get-Help`, `Get-Command`, `Get-Member`
- Quản trị: `Get-Process`, `Get-Service`, `Get-LocalUser`, `Get-NetTCPConnection`, `Get-ScheduledTask`, `Get-WinEvent`
- Remoting: WinRM, `Enter-PSSession`; execution policy (không phải ranh giới bảo mật)
- Logging PowerShell: Script Block Logging (Event 4104), Module Logging, Transcription

**Ví dụ**: 20 lần đăng nhập thất bại gần nhất:

```powershell
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} -MaxEvents 20 |
  Select-Object TimeCreated, @{n='User';e={$_.Properties[5].Value}}, @{n='IP';e={$_.Properties[19].Value}}
```

**Tài liệu**: [PowerShell documentation](https://learn.microsoft.com/powershell/); sách *Learn PowerShell in a Month of Lunches*.

### Chương 3.3 — Windows Event Log & Sysmon (Tuần 10)

| Event ID | Ý nghĩa | Vì sao quan trọng |
| --- | --- | --- |
| 4624 / 4625 | Đăng nhập thành công / thất bại (xem Logon Type 2, 3, 10) | Brute force, lateral movement |
| 4648 | Đăng nhập bằng credential tường minh | runas, lạm dụng credential |
| 4672 | Gán đặc quyền admin cho phiên | Theo dõi tài khoản đặc quyền |
| 4688 | Tạo process mới (bật command line logging) | Phát hiện lệnh độc |
| 4697 / 7045 | Cài service mới | Persistence, PsExec |
| 4698 | Tạo scheduled task | Persistence |
| 4720 / 4728 / 4732 | Tạo user / thêm vào group đặc quyền | Tạo backdoor account |
| 4768 / 4769 / 4771 | Kerberos TGT / service ticket / pre-auth thất bại | Kerberoasting, password spraying |
| 1102 | Xóa Security log | Dấu hiệu che giấu rất mạnh |
| 4104 | PowerShell Script Block | Lệnh PowerShell bị làm rối |

- **Sysmon**: cài từ [Microsoft Sysinternals](https://learn.microsoft.com/sysinternals/downloads/sysmon) với cấu hình [SwiftOnSecurity sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config); event 1 (process + hash), 3 (network), 11 (file), 13 (registry), 22 (DNS)
- Event Viewer, custom view, chuyển tiếp log (Windows Event Forwarding)

**Lab**: bật Advanced Audit Policy + command line logging; cài Sysmon; mô phỏng 5 hành vi (sai mật khẩu, tạo user, tạo task, chạy PowerShell encode, xóa log) và tìm event tương ứng.

### Chương 3.4 — Active Directory (Tuần 10–11)

- Khái niệm: forest, domain, tree, OU, Domain Controller, Global Catalog, FSMO, site, trust
- Đối tượng: user, group (security/distribution, scope), computer, service account, gMSA
- Group Policy: GPO, thứ tự áp dụng LSDOU, `gpupdate /force`, `gpresult /r`
- DNS tích hợp AD, LDAP, SYSVOL
- Xác thực: **Kerberos** (AS-REQ/REP → TGT → TGS-REQ/REP → service ticket, KDC, krbtgt) vs **NTLM** (challenge-response)
- Nhóm đặc quyền: Domain Admins, Enterprise Admins, Administrators, Backup Operators; mô hình tiering, LAPS

**Lab**:

1. Dựng domain `lab.local`: 1 DC (Windows Server), 2 client join domain
2. Tạo cấu trúc OU (IT, HR, Sales), 15 user bằng script PowerShell đọc CSV
3. GPO: chính sách mật khẩu, khóa tài khoản sau 5 lần sai, chặn USB, bật audit
4. Capture Kerberos bằng Wireshark khi user đăng nhập và truy cập file share
5. Nâng cao (tuỳ chọn): triển khai [GOAD — Game of Active Directory](https://github.com/Orange-Cyberdefense/GOAD) để chuẩn bị cho giai đoạn Red Team

**Video**: TryHackMe phòng Active Directory Basics; Microsoft Learn module AD DS; kênh YouTube John Savill's Technical Training (Windows/Azure)

### Góc nhìn bảo mật — Module 3

- Kẻ tấn công: dump credential từ LSASS, Pass-the-Hash, Kerberoasting, lạm dụng GPO/ACL, persistence qua Registry/Service/Task, living-off-the-land (LOLBAS)
- Người phòng thủ: audit policy đầy đủ + Sysmon, Credential Guard, LAPS, tiering admin, giám sát event 4769 với mã hóa RC4, giới hạn Domain Admins

### Tiêu chí đạt Module 3

- [ ] Domain lab hoạt động với OU, GPO, 15 user tạo bằng script
- [ ] Báo cáo: 10 Event ID quan trọng kèm ảnh chụp event thật từ lab
- [ ] Vẽ lại được luồng Kerberos và chỉ ra bước Kerberoasting lợi dụng
- [ ] Phân biệt được process tree chuẩn và bất thường (ví dụ `winword.exe` sinh `powershell.exe`)

## Module 4 — Ảo hóa, Docker & Home Lab (bắt đầu tuần 1, hoàn thiện tuần 12)

Home lab là nơi bạn được phép phá hỏng và tấn công hợp pháp; nó cũng là portfolio đầu tiên khi phỏng vấn.

### Chương 4.1 — Kiến thức ảo hóa

- Hypervisor type 1 (Proxmox VE, ESXi, Hyper-V) vs type 2 (VirtualBox, VMware Workstation)
- Chế độ mạng ảo: NAT, Bridged, Host-only, Internal network — lab tấn công phải dùng Host-only/Internal để không ảnh hưởng mạng thật
- Snapshot, clone, template; tài nguyên (CPU, RAM, disk thin provisioning)
- Container vs VM: container chung kernel, nhẹ hơn nhưng cách ly yếu hơn

**So sánh lựa chọn**

| Lựa chọn | Ưu điểm | Nhược điểm | Phù hợp |
| --- | --- | --- | --- |
| VirtualBox trên laptop | Miễn phí, dễ cài | Hiệu năng thấp, giới hạn RAM | Bắt đầu, 16 GB RAM |
| VMware Workstation Pro | Ổn định, mạng ảo tốt (miễn phí cho cá nhân) | Chỉ chạy khi mở laptop | Lab trung bình |
| Proxmox trên PC/mini PC cũ | Chạy 24/7, quản lý qua web, giống môi trường thật | Cần máy riêng | Lab lâu dài, 32 GB+ |
| Cloud (AWS/Azure free tier, credit sinh viên) | Không cần phần cứng | Tốn phí nếu quên tắt, giới hạn chính sách tấn công | Bổ trợ, học cloud |

### Chương 4.2 — Docker cơ bản

- Image, container, volume, network; `docker run -d -p`, `docker ps`, `docker exec -it`, `docker logs`
- Dockerfile, docker compose
- Ứng dụng cho lab: chạy nhanh DVWA, OWASP Juice Shop, Wazuh, ELK
- Bảo mật container mức cơ bản: không chạy root, không mount `docker.sock`, dùng image chính thức, quét bằng Trivy

**Tài liệu**: [Docker Docs — Get started](https://docs.docker.com/get-started/)

### Chương 4.3 — Kiến trúc home lab chuẩn

| Thành phần | OS | RAM đề xuất | Mạng | Vai trò |
| --- | --- | --- | --- | --- |
| Firewall | pfSense hoặc OPNsense | 1–2 GB | WAN (NAT) + LAN + DMZ + ATTACK | Định tuyến, chặn giữa các vùng, log |
| Domain Controller | Windows Server (Evaluation) | 4 GB | LAN | AD, DNS, GPO |
| Workstation | Windows 10/11 Enterprise (Evaluation) | 4 GB | LAN | Máy người dùng, Sysmon |
| Linux server | Ubuntu Server LTS | 2 GB | DMZ | Web server, SSH, Docker |
| Attacker | Kali Linux | 4 GB | ATTACK | Công cụ quét, tấn công lab |
| SIEM (giai đoạn sau) | Wazuh/ELK hoặc Security Onion | 8 GB+ | LAN (mgmt) | Thu log tập trung |

Tổng tối thiểu khoảng 16 GB RAM cho 4 máy chạy cùng lúc; 32 GB để thêm SIEM.

### Chương 4.4 — Các bước dựng lab

1. Cài hypervisor, tạo 3 mạng nội bộ (LAN 10.10.10.0/24, DMZ 10.10.20.0/24, ATTACK 10.10.99.0/24)
2. Cài pfSense/OPNsense với 4 interface, bật DHCP cho mỗi vùng
3. Viết firewall rule: LAN ra Internet được; DMZ không vào được LAN; ATTACK chỉ vào được DMZ và LAN khi bật lab
4. Cài Ubuntu Server vào DMZ, Windows Server làm DC, Windows client join domain
5. Cài Kali vào ATTACK, kiểm tra kết nối bằng `ping` và `nmap -sn`
6. Snapshot "clean" cho mọi máy
7. Viết tài liệu: sơ đồ mạng (draw.io), bảng IP, tài khoản lab, rule firewall; đẩy lên GitHub (không để mật khẩu thật)

**Tài liệu**: [pfSense Documentation](https://docs.netgate.com/pfsense/en/latest/), [Proxmox VE Documentation](https://pve.proxmox.com/pve-docs/), [Kali Linux Documentation](https://www.kali.org/docs/)

### Tiêu chí đạt Module 4

- [ ] Lab đủ 5 máy, 3 vùng mạng, firewall chặn đúng chính sách (kiểm chứng bằng nmap từ Kali)
- [ ] Có sơ đồ + tài liệu để người khác dựng lại được
- [ ] Chạy được DVWA và Juice Shop bằng docker compose trong DMZ

## Module 5 — Lập trình & Scripting (Tuần 13–15, kèm 1 bài nhỏ mỗi tuần từ tuần 2)

Bạn đã có nền Java, nên trọng tâm là viết công cụ bảo mật nhỏ, tự động hóa công việc lặp lại, và đọc hiểu code của người khác (kể cả mã độc dạng script).

### Chương 5.1 — Python cho bảo mật (Tuần 13–14)

- Cơ bản nhanh: kiểu dữ liệu, list/dict comprehension, hàm, module, virtualenv, xử lý ngoại lệ (`try/except`), `argparse`, `logging`
- Thư viện hay dùng: `socket`, `requests`, `scapy`, `re`, `json`, `csv`, `hashlib`, `base64`, `subprocess`, `pathlib`, `concurrent.futures`
- Đọc/ghi file log lớn theo stream (không đọc toàn bộ vào RAM), gọi REST API (VirusTotal, AbuseIPDB, Shodan)

**Ví dụ mẫu — TCP connect scanner đơn giản (chỉ dùng trong lab của bạn):**

```python
import argparse
import socket
from concurrent.futures import ThreadPoolExecutor


def scan_port(host: str, port: int, timeout: float = 0.5) -> int | None:
    """Trả về port nếu mở, None nếu đóng/lọc hoặc lỗi."""
    try:
        with socket.create_connection((host, port), timeout=timeout):
            return port
    except (socket.timeout, ConnectionRefusedError, OSError):
        # Port đóng, bị firewall chặn hoặc host không phản hồi
        return None


def main() -> None:
    parser = argparse.ArgumentParser(description="Simple TCP connect scanner")
    parser.add_argument("host")
    parser.add_argument("--ports", default="1-1024", help="Ví dụ: 1-1024")
    args = parser.parse_args()

    try:
        start, end = map(int, args.ports.split("-"))
        target = socket.gethostbyname(args.host)
    except ValueError:
        parser.error("--ports phải có dạng START-END")
    except socket.gaierror:
        parser.error(f"Không phân giải được host: {args.host}")

    # Dùng thread pool vì tác vụ chủ yếu chờ I/O mạng
    with ThreadPoolExecutor(max_workers=100) as pool:
        results = pool.map(lambda p: scan_port(target, p), range(start, end + 1))

    open_ports = [p for p in results if p is not None]
    print(f"{target}: open ports = {open_ports or 'none'}")


if __name__ == "__main__":
    main()
```

**Tài liệu**: [The Python Tutorial](https://docs.python.org/3/tutorial/), [Automate the Boring Stuff with Python](https://automatetheboringstuff.com/) (đọc online miễn phí), sách *Black Hat Python* (2nd ed.), [Scapy documentation](https://scapy.readthedocs.io/)

### Chương 5.2 — Bash scripting (Tuần 14)

- Shebang, biến, `$1 $@ $#`, `if/[[ ]]`, `for/while`, function, exit code, `set -euo pipefail`, `trap`
- Kết hợp với `grep/awk/sed`, `cron`
- **Bài tập**: script kiểm tra nhanh server (user có UID 0, file SUID mới, port đang lắng nghe, lần đăng nhập gần nhất) và xuất báo cáo

**Tài liệu**: MIT Missing Semester bài 2; [ShellCheck](https://www.shellcheck.net/) để bắt lỗi script

### Chương 5.3 — PowerShell scripting (Tuần 14–15)

- Script `.ps1`, param block, `try/catch/finally`, `-ErrorAction Stop`, xuất CSV/JSON
- **Bài tập**: script quét mọi máy trong domain lab, liệt kê local admin, service chạy bằng tài khoản user, scheduled task lạ

### Chương 5.4 — Công cụ hỗ trợ (Tuần 15)

- **Git**: commit, branch, merge, `.gitignore`, không bao giờ commit secret — luyện tại [Learn Git Branching](https://learngitbranching.js.org/)
- **Regex**: character class, quantifier, group, lookahead — luyện tại [regex101](https://regex101.com/) với mẫu IP, email, URL, hash
- **Định dạng dữ liệu**: JSON (`jq`), YAML, CSV, base64/hex (CyberChef)
- **Đọc hiểu**: SQL (SELECT/JOIN/UNION — nền cho SQLi), JavaScript (DOM, fetch — nền cho XSS), HTTP request trong code

### Danh sách 5 tool portfolio

| Tool | Ngôn ngữ | Chức năng | Kỹ năng rèn |
| --- | --- | --- | --- |
| port-scanner | Python | Quét TCP đa luồng, xuất JSON | socket, concurrency |
| ssh-log-analyzer | Python | Phân tích auth.log, phát hiện brute force theo ngưỡng | regex, xử lý file lớn |
| ioc-enricher | Python | Tra IP/hash qua API VirusTotal/AbuseIPDB | REST API, rate limit, secret qua biến môi trường |
| linux-audit.sh | Bash | Kiểm tra cấu hình bảo mật cơ bản | shell, permission |
| ad-inventory.ps1 | PowerShell | Kiểm kê user, admin, task trong domain | AD, WinRM |

Mỗi tool cần README (mục đích, cách chạy, ví dụ output), xử lý lỗi rõ ràng, và cảnh báo "chỉ dùng trên hệ thống được ủy quyền".

### Tiêu chí đạt Module 5

- [ ] 5 tool trên GitHub, mỗi tool có README và xử lý ngoại lệ
- [ ] Viết regex bắt IPv4, email, SHA-256 không cần tra cứu
- [ ] Đọc hiểu 1 script PowerShell bị làm rối (base64) bằng CyberChef

## Lịch học 16 tuần

Mỗi tuần khoảng 12–15 giờ: 4 giờ video/đọc, 7–8 giờ lab, 1 giờ script nhỏ, 1 giờ ghi chú + Anki. Nếu trượt quá 1 tuần, cắt bớt phần "tuỳ chọn" chứ không bỏ lab.

| Tuần | Chủ đề | Video / đọc | Lab | Script nhỏ / sản phẩm |
| --- | --- | --- | --- | --- |
| 1 | OSI/TCP-IP, bắt đầu subnet; cài hypervisor | Messer 1.1–1.3; freeCodeCamp "How the internet works" | Cài VirtualBox/VMware, Kali, Ubuntu; Wireshark bài đầu | Repo ghi chú GitHub |
| 2 | Subnetting, IPv6 | Practical Networking Subnetting Mastery; Messer 1.7–1.8 | 50 bài subnet; thiết kế VLSM | Python: chuyển IP ↔ nhị phân |
| 3 | ARP, DHCP, DNS, TCP/UDP, ICMP | Messer 1.4–1.5; Kurose chương 3 | Capture handshake, `dig +trace` | Anki 25 port |
| 4 | HTTP, TLS, SSH, SMB, email; thiết bị & routing | Messer 2.x; Cloudflare Learning (TLS, DNS) | Packet Tracer: VLAN + ACL | Python: gọi HTTP, in header |
| 5 | Wireshark nâng cao, nmap, tổng kết Module 1 | Practical Packet Analysis | 3 PCAP (SampleCaptures, malware-traffic-analysis) | **Báo cáo 3 PCAP** |
| 6 | Linux shell, filesystem, text processing | Missing Semester 1–2, 4; Linux Journey | Bandit 0–12 | Bash: đếm IP trong log |
| 7 | User/permission, process, systemd, cron | Linux Journey (Permissions, Processes) | Bandit 13–20; tạo service systemd | Bash: tìm file SUID |
| 8 | Network Linux, log, firewall, hardening | CIS Benchmark Ubuntu (đọc lướt) | ufw, fail2ban, Lynis; brute-force thử bằng Hydra | **Server hardening + báo cáo** |
| 9 | Kiến trúc Windows, Sysinternals, PowerShell cơ bản | THM Windows Fundamentals 1–3 | Autoruns, Process Explorer | PowerShell: liệt kê service lạ |
| 10 | Event Log, Sysmon, audit policy; AD khái niệm | Ultimate Windows Security; Microsoft Learn AD DS | Cài Sysmon, mô phỏng 5 hành vi | Bảng 10 Event ID |
| 11 | Dựng AD, GPO, Kerberos | THM Active Directory Basics | Domain `lab.local`, 15 user, GPO, capture Kerberos | **AD lab + báo cáo Event ID** |
| 12 | Hoàn thiện home lab, Docker | Docker Get Started; pfSense docs | pfSense 3 vùng mạng; DVWA/Juice Shop bằng compose | **Sơ đồ + tài liệu lab** |
| 13 | Python cho bảo mật | Python Tutorial; Automate the Boring Stuff | port-scanner, ssh-log-analyzer | 2 tool |
| 14 | Python API + Bash scripting | Black Hat Python (chương đầu); ShellCheck | ioc-enricher, linux-audit.sh | 2 tool |
| 15 | PowerShell scripting, Git, regex, CyberChef | Learn Git Branching; regex101 | ad-inventory.ps1 | **5 tool trên GitHub** |
| 16 | Ôn tập & kiểm tra cuối giai đoạn | Ôn Anki, ghi chú | Capstone mini (xem mục dưới) | **Báo cáo capstone** |

Tuỳ chọn song song: nếu muốn học networking sâu kiểu CCNA, theo thêm khoá miễn phí "Free CCNA 200-301 Complete Course" của kênh YouTube Jeremy's IT Lab (có lab Packet Tracer kèm theo).

## Kiểm tra cuối giai đoạn (Tuần 16)

Đạt khi trả lời trơn tru ≥ 80% câu hỏi (không tra cứu) và hoàn thành capstone mini có báo cáo.

### Câu hỏi tự đánh giá

**Networking**

1. Mô tả đầy đủ những gì xảy ra khi gõ `https://example.com` vào trình duyệt.
2. 10.20.30.150/26 thuộc network nào, broadcast là gì, có bao nhiêu host?
3. Vì sao ARP spoofing khả thi và hai cách phòng chống ở tầng switch?
4. Phân biệt TCP SYN scan và TCP connect scan; cái nào để lại log trên ứng dụng?
5. DNS tunneling hoạt động thế nào và dấu hiệu nào trong log DNS gợi ý nó?
6. Stateful firewall khác stateless ở điểm nào? Vì sao cần egress filtering?
7. Trong TLS handshake, certificate được xác thực ra sao?

**Linux**

8. Giải thích permission `-rwsr-xr-x` và rủi ro của nó.
9. Log đăng nhập SSH nằm ở đâu trên Ubuntu và RHEL? Lệnh xem log của 1 service bằng systemd?
10. Nêu 4 vị trí kẻ tấn công thường đặt persistence trên Linux.
11. Viết one-liner đếm số request theo HTTP status code từ access log Nginx.

**Windows & AD**

12. Parent process bình thường của `lsass.exe` và `svchost.exe` là gì?
13. Event 4624 với Logon Type 3 và 10 khác nhau thế nào?
14. Vẽ luồng Kerberos và chỉ ra vì sao Kerberoasting khả thi.
15. Thứ tự áp dụng GPO là gì? Vì sao không nên dùng Domain Admin để đăng nhập máy trạm?
16. Sysmon bổ sung gì mà Security log mặc định không có?

**Scripting**

17. Vì sao dùng thread pool cho port scanner mà không dùng vòng lặp tuần tự?
18. Làm sao giữ API key ngoài source code?
19. Giải mã một lệnh `powershell -enc <base64>` bằng cách nào?
20. `set -euo pipefail` giúp gì cho Bash script?

### Capstone mini: "Điều tra một cuộc tấn công trong lab của bạn"

Kịch bản (toàn bộ trong home lab, hệ thống của bạn):

1. Từ Kali, quét mạng DMZ bằng nmap
2. Brute-force SSH vào Ubuntu (mật khẩu yếu cố ý đặt), đăng nhập thành công
3. Tạo cron job persistence và user mới
4. Từ Windows client, chạy 1 lệnh PowerShell encode tải file từ Ubuntu
5. Capture toàn bộ traffic bằng tcpdump trên pfSense/Ubuntu

Nhiệm vụ của bạn với vai trò người phòng thủ:

- [ ] Dựng timeline sự kiện từ PCAP, auth.log, journal, Windows Event Log và Sysmon
- [ ] Xác định IOC: IP, user, file, cron job, lệnh PowerShell đã giải mã
- [ ] Dùng script của chính mình (ssh-log-analyzer, linux-audit.sh) hỗ trợ điều tra
- [ ] Đề xuất 5 biện pháp khắc phục có ưu tiên (ví dụ SSH key-only, fail2ban, egress rule, bật Script Block Logging)
- [ ] Viết báo cáo 4–6 trang: tóm tắt cho quản lý, timeline, phân tích kỹ thuật, khuyến nghị

Hoàn thành capstone = sẵn sàng vào Giai đoạn 2 (Security Foundations & Quản trị rủi ro).

## Nguồn tham khảo

Các link đánh dấu (✓) đã được kiểm tra qua tìm kiếm ngày 23/11/2026; các link còn lại là trang chính thức của dự án/nhà cung cấp, nên mở lại để xác nhận trước khi dùng.

### Video & khóa học

| Nguồn | Loại | Chi phí | Dùng cho |
| --- | --- | --- | --- |
| [Professor Messer — N10-009 Network+ Training Course](https://www.professormesser.com/network-plus/n10-009/n10-009-video/n10-009-training-course/) ✓ | Video, 87 bài | Miễn phí | Module 1 |
| [freeCodeCamp — Computer Networking Fundamentals (12 giờ)](https://www.freecodecamp.org/news/computer-networking-fundamentals/) ✓ | Video YouTube | Miễn phí | Module 1 |
| [freeCodeCamp — Computer Networking Course, Network Engineering (9 giờ)](https://www.freecodecamp.org/news/free-computer-networking-course/) ✓ | Video YouTube | Miễn phí | Module 1 |
| [freeCodeCamp — How does the internet work? (\~2 giờ)](https://www.freecodecamp.org/news/how-does-the-internet-work/) ✓ | Video YouTube | Miễn phí | Module 1, người mới |
| [Practical Networking — Subnetting Mastery](https://www.practicalnetworking.net/?p=2110) ✓ | Video series | Miễn phí | Subnetting |
| Jeremy's IT Lab — Free CCNA 200-301 Complete Course (YouTube) ✓ | Video + lab Packet Tracer | Miễn phí | Networking sâu (tuỳ chọn) |
| [MIT — The Missing Semester of Your CS Education](https://missing.csail.mit.edu/) ✓ | Bài giảng + video | Miễn phí | Module 2, 5 |
| [Linux Journey](https://labex.io/linuxjourney) ✓ | Bài học tương tác | Miễn phí | Module 2 |
| [Cisco Networking Academy](https://www.netacad.com/) | Khóa học + Packet Tracer | Miễn phí (đăng ký) | Module 1 |
| [TryHackMe](https://tryhackme.com/) | Lab trình duyệt | Freemium | Mọi module |

### Lab & công cụ thực hành

| Nguồn | Dùng cho |
| --- | --- |
| [OverTheWire — Bandit](https://overthewire.org/wargames/bandit/) | Linux wargame |
| [Wireshark User's Guide](https://www.wireshark.org/docs/wsug_html_chunked/) và [Wireshark SampleCaptures](https://wiki.wireshark.org/SampleCaptures) | Phân tích gói tin |
| [Malware-Traffic-Analysis.net](https://www.malware-traffic-analysis.net/) | PCAP thực tế có bài tập |
| [explainshell](https://explainshell.com/) | Giải thích lệnh shell |
| [GTFOBins](https://gtfobins.github.io/) | Binary Linux bị lạm dụng |
| [Sysmon — Microsoft Sysinternals](https://learn.microsoft.com/sysinternals/downloads/sysmon) và [SwiftOnSecurity sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config) | Logging Windows |
| [Ultimate Windows Security — Event ID Encyclopedia](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/) | Tra cứu Event ID |
| [GOAD — Game of Active Directory](https://github.com/Orange-Cyberdefense/GOAD) | Lab AD nâng cao |
| [Docker Docs — Get started](https://docs.docker.com/get-started/) | Module 4 |
| [pfSense Documentation](https://docs.netgate.com/pfsense/en/latest/), [Proxmox VE Documentation](https://pve.proxmox.com/pve-docs/), [Kali Linux Documentation](https://www.kali.org/docs/) | Home lab |
| [Learn Git Branching](https://learngitbranching.js.org/), [regex101](https://regex101.com/), [ShellCheck](https://www.shellcheck.net/) | Module 5 |

### Tài liệu đọc

| Tài liệu | Tác giả | Dùng cho |
| --- | --- | --- |
| *Computer Networking: A Top-Down Approach* | Kurose & Ross | Module 1 (sách gốc) |
| *Practical Packet Analysis* (3rd ed.) | Chris Sanders | Wireshark |
| *The Linux Command Line* | William Shotts (bản online miễn phí tại linuxcommand.org) | Module 2 |
| *Learn PowerShell in a Month of Lunches* | Travis Plunk, James Petty, Tyler Leonhardt, Jeffery Hicks | Module 3 |
| [Microsoft Learn — PowerShell documentation](https://learn.microsoft.com/powershell/) | Microsoft | Module 3 |
| [The Python Tutorial](https://docs.python.org/3/tutorial/) | Python Software Foundation | Module 5 |
| [Automate the Boring Stuff with Python](https://automatetheboringstuff.com/) | Al Sweigart | Module 5 |
| *Black Hat Python* (2nd ed.) | Justin Seitz, Tim Arnold | Module 5 |
| [Scapy documentation](https://scapy.readthedocs.io/) | Scapy project | Module 5 |
| [Cloudflare Learning Center](https://www.cloudflare.com/learning/) | Cloudflare | DNS, TLS, DDoS |
