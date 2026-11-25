# Protocol Explorer: Interactive Network Protocol Visualizer

An **interactive web app** that visualizes **39 internet protocols** with isometric network diagrams, synchronized sequence diagrams, progressive packet playback, and a **Wireshark-style hex/ASCII inspector**.

**No installation, backend, API key, or build step.** Open `protocol-explorer.html` in any modern browser and start exploring.

## Demo

**Watch the demo:** [`launch_2_xray_scrollstopper.mp4`](./launch_2_xray_scrollstopper.mp4)

Live link: **coming soon**.

## Features

- **39 protocols covered.** **11 Core**, **19 Application**, **9 Security**. **241 directional wire packets** across **236 lesson chapters**.
- **Cinematic network view.** Isometric diagrams with camera zoom/pan, typing address banners, animated wire paths, and **2-line packet cards** moving along multi-hop routes. Includes **packet drops and retransmissions** for TCP and UDP.
- **Synchronized sequence view.** UML-style participant ladder diagram tied to the same step and packet selection.
- **Progressive packet flow table.** Empty at start, appends each packet **live** as it travels. Speed control from **0.5x to 2x**, plus Play/Pause, Step Forward, Step Back, and Reset.
- **Step details and lesson stepper.** Chapter stepper inside the sidebar paired with live step details: active direction, sub-packet progress, and protocol metadata.
- **Byte-level inspector.** Click a packet row to see decoded **L2 (Ethernet II)**, **L3 (IPv4/IPv6) with RFC 1071 checksums**, **L4 (TCP/UDP/ICMP/IGMP)**, and **L7/binary headers**, next to a **hex and ASCII dump** with hover highlighting.
- **Instant search (Ctrl+K) and OSI layer filter.** Filter by category (**ALL, CORE, APPLICATION, SECURITY**), click an OSI layer (**1 to 7**), or search by name, port, RFC, or keyword.
- **Exam mode and progress tracking.** Multiple-choice quiz with explanations. Lesson completion saved in **localStorage**.
- **Light and dark blueprint themes.** Light drafting-paper blue and dark Prussian blueprint, with responsive **desktop and mobile** layout.

## Included Protocols (39)

### Core (11)

| Protocol | Layer | Default Port / Identifier | Focus |
| :--- | :---: | :--- | :--- |
| **TCP** | L4 | Dynamic Ports (IP Proto 6) | 3-way handshake, packet loss, SACK/gap retransmission, FIN close |
| **UDP** | L4 | Dynamic Ports (IP Proto 17) | 0-RTT datagrams, dropped packet with no stall |
| **IP** | L3 | IPv4 | Hop-by-hop routing, TTL decrement, NAT and reverse NAT |
| **BGP** | L7 | 179 (TCP) | OPEN, KEEPALIVE, UPDATE prefix and AS_PATH propagation |
| **IPv6** | L3 | EtherType `0x86DD` | DAD, Router Solicitation/Advertisement (SLAAC), global IPv6 |
| **DNS** | L7 | 53 (UDP/TCP) | Recursive stub query and iterative Root to TLD to Auth NS walk |
| **DHCP** | L7 | 67 / 68 (UDP) | Broadcast DORA exchange (Discover, Offer, Request, Ack) |
| **ICMP** | L3 | IP Proto 1 | Traceroute (TTL=1, Type 11) and Ping Echo Request/Reply |
| **IGMP** | L3 | IP Proto 2 | IGMPv3 Join, switch snooping, multicast IPTV delivery, Leave |
| **Ethernet** | L2 | 48-bit MAC | ARP broadcast/reply, switch MAC learning, unicast forwarding |
| **PPPoE** | L2 | `0x8863` / `0x8864` | PADI to PADO to PADR to PADS, LCP/CHAP login, IPCP public IP |

### Application (19)

| Protocol | Layer | Default Port | Focus |
| :--- | :---: | :--- | :--- |
| **HTTP** | L7 | 80 | DNS lookup, TCP handshake, GET /, 200 OK, page render |
| **HTTPS** | L7 | 443 | DNS, TCP, TLS 1.3 1-RTT handshake, encrypted HTTP/2 |
| **WebSocket** | L7 | 80 / 443 | HTTP 101 Switching Protocols, masked/unmasked frames, Ping/Pong |
| **WebRTC** | L7 | UDP Dynamic / 3478 | SDP signaling, STUN/ICE NAT traversal, DTLS-SRTP P2P media |
| **SIP** | L7 | 5060 / 5061 | REGISTER, INVITE, 180 Ringing, 200 OK, RTP voice, BYE |
| **RTSP** | L7 | 554 | OPTIONS, DESCRIBE, SETUP, PLAY, H.264 IP camera RTP |
| **RTMP** | L7 | 1935 | C0/C1/S0/S1/S2 handshake, AMF0 connect/publish, A/V chunks |
| **QUIC** | L4 | 443 (UDP) | Combined transport and TLS 1.3 1-RTT handshake, HTTP/3 streams |
| **NTP** | L7 | 123 (UDP) | 4-timestamp (T1 to T4) Stratum 1 clock offset and slewing |
| **Captive Portal** | L7 | 80 / 443 | OS HTTP probe, 302 intercept, portal login, MAC allowlisting |
| **SMTP** | L7 | 25 / 465 / 587 | TLS submission, envelope and DATA, DNS MX lookup, STARTTLS relay |
| **POP3** | L7 | 110 / 995 | USER/PASS, RETR, DELE, commit on QUIT |
| **IMAP** | L7 | 143 / 993 | Tagged commands (A001 to A004), \Seen sync, IDLE push |
| **FTP** | L7 | 21 / PASV | Control login, PASV port negotiation, separate binary data socket |
| **SMB** | L7 | 445 | SMB 3.1.1 negotiate, NTLM challenge-response, share mount and read |
| **HTTP Proxy** | L7 | 8080 / 3128 | CONNECT host:443 raw TCP tunnel with end-to-end TLS |
| **SOCKS5** | L5 | 1080 | Binary greeting, remote DNS CONNECT, protocol-agnostic relay |
| **Reverse Proxy** | L7 | 443 to 8080 | Edge TLS termination, X-Forwarded-For, private VPC upstream |
| **Modbus** | L7 | 502 | Industrial OT MBAP header, FC 0x03 read registers, FC 0x05 coil |

### Security (9)

| Protocol | Layer | Default Port / Identifier | Focus |
| :--- | :---: | :--- | :--- |
| **DNS over HTTPS** | L7 | 443 | Encrypted POST /dns-query (application/dns-message) |
| **DNSSEC** | L7 | 53 (EDNS0 DO=1) | DS + DNSKEY + RRSIG chain of trust, AD=1 validation |
| **Wi-Fi (WPA2)** | L2 | `0x888E` (EAPOL) | Beacon, Association, 4-Way EAPOL handshake, AES-CCMP |
| **WPA3** | L2 | SAE + EAPOL | Dragonfly SAE Commit/Confirm, Forward Secrecy, PMF (802.11w) |
| **RADIUS** | L7 | 1812 (UDP) + 802.1X | EAP Identity, Access-Request/Challenge/Accept, dynamic VLAN |
| **SSH** | L7 | 22 | Banners, Curve25519 KEX, Ed25519 host key and pubkey auth, shell |
| **TLS/SSL** | L6 | 443 | TLS 1.3 ClientHello, ServerHello, encrypted cert, AEAD records |
| **WireGuard** | L3 | 51820 (UDP) | Noise_IKpsk2 Type 1/2 handshake, Type 4 ChaCha20-Poly1305 tunnel |
| **IPsec** | L3 | 500 / 4500 (UDP) + ESP | IKE_SA_INIT, NAT-T port 4500, IKE_AUTH, ESP Tunnel Mode |

## Quick Start

1. Put `protocol-explorer.html` **anywhere** on your computer.
2. **Double-click** it to open in Chrome, Firefox, Edge, or Safari.
3. Pick a protocol from the left sidebar, or press **Ctrl+K**, then click **PLAY** or **STEP**.
4. Click any packet row in **Packet Flow**, or switch to the **BYTE INSPECTOR** tab, to explore decoded headers. Hover fields to highlight their **hex and ASCII** bytes.

### Hosting Online

The whole app is **one self-contained HTML file**. Deploy it as `index.html` on **GitHub Pages**, **Cloudflare Pages**, **Netlify**, or **Vercel** with **no configuration**.

## Keyboard Shortcuts

| Shortcut | Action |
| :--- | :--- |
| `Space` | Play / Pause animation |
| `→` / `↓` | Step forward |
| `←` / `↑` | Step back |
| `R` | Reset current trace to overview |
| `V` | Toggle Network and Sequence views |
| `I` | Toggle Overview/Step Details and Byte Inspector |
| `Ctrl + K` / `⌘ + K` | Open instant protocol search |
| `T` | Toggle light and dark theme |
| `?` | Open keyboard shortcuts guide |
| `Esc` | Close active modal |

## Note on Educational Traces

Protocol Explorer runs **predefined teaching scenarios** **offline** in your browser. It does **not capture live traffic**. Timestamps and example IPs (`192.168.1.x`, `203.0.113.x`, `198.51.100.x`, `2001:db8::`) follow **RFC documentation ranges**, so you can learn protocol behavior before inspecting live captures in **Wireshark or tcpdump**.
