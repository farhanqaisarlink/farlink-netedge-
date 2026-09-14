# FarLink

FarLink is a network performance monitoring platform built on the Raspberry Pi Compute Module 5 (CM5). It ships as two hardware variants that share a single codebase, plus a central dashboard server.

---

## Devices

### FarLink Go — with screen & push button

- On-demand speed test triggered by a push button; result shown on a 3.2" display
- Screen shows **only** the button-triggered speed test result — no other test output is displayed on-device
- Networking: DHCP by default, with a manual static IP option (`network_mode: dhcp | static`)
- Speed test engine: self-hosted **LibreSpeed** (configurable server address — no Ookla/speedtest.net, due to commercial licensing restrictions)
- Additional diagnostics (server-logged only, not shown on screen): `mtr`, `dig`, `curl`, `openssl`, `ping`, TCP port check
- Server can set a periodic test interval (15 min / 1 hour / 24 hours) in addition to the manual button trigger
- Results are saved locally with a timestamp; the server fetches the result file whenever the device is reachable and idle
- Device registers with the server

### FarLink Edge — headless, no screen or button

- Two units operate in **master/slave** configuration, running `iperf3` between them over a dedicated point-to-point link
- Physical connectivity: onboard RJ45 (ETH1) is used for uplink to the dashboard/internet; a USB-to-Ethernet adapter provides the dedicated master/slave link
- Same diagnostic suite as Go: `iperf3` (throughput / jitter / loss / retransmissions), `mtr`, `dig`, `curl`, `openssl`, `ping`, TCP port check
- Test schedule is set by the server; execution happens on the device
- Results are saved locally with a timestamp; the server fetches the result file whenever the device is reachable and idle
- Device registers with the server

### Shared codebase

Both devices run from **one common script**, not separate codebases. Hardware-specific behavior — screen output, push-button trigger, iPerf3 master/slave role — is enabled or disabled through configuration, so the same software runs on either hardware variant depending on which features are present.

---

## Server

- Receives device registrations and assigns device IDs
- Sets the periodic test interval (Go) or test schedule (Edge) per device
- Fetches each device's result file when the device is reachable and idle
- Combines fetched data into a report containing device ID, name, time, and per-test results

---

## Test tools

| Tool | Purpose |
|---|---|
| `librespeed-cli` | Internet speed test (Go) |
| `iperf3` | Throughput / jitter / loss / retransmissions, master/slave (Edge) |
| `mtr` | Path tracing |
| `dig` | DNS resolution timing |
| `curl` | HTTP/HTTPS response time |
| `openssl` | SSL/TLS certificate check |
| `ping` | ICMP latency |
| Python `socket` | TCP port reachability |

Install: `apt install iperf3 mtr dnsutils curl openssl`

---

## Hardware

- Raspberry Pi Compute Module 5 (non-wireless), single Gigabit Ethernet (RJ45), USB-C power, 3.2" ILI9341 display (Go only)
- Non-wireless CM5 is used deliberately to keep FCC/CE certification in the lower-cost unintentional-radiator path

---

## Out of scope for this phase

- ZTP provisioning / auto-registration beyond basic device registration
- AI-generated report summaries
- Ookla / speedtest.net as a test engine
