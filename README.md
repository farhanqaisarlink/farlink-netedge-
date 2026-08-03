# farlink-netedge-
Description: A Raspberry Pi CM5-based edge network analyzer for real-time iPerf3 telemetry and network diagnostic
# Farlink NetEdge

**Farlink NetEdge** is a compact, hardware-accelerated edge network analyzer based on the **Raspberry Pi Compute Module 5 (CM5)**. Designed for network engineers and IT professionals, it provides real-time iPerf3 telemetry, hardware diagnostics, and automated local/point-to-point throughput analysis.

---

## 🔑 Key Features

* **Edge Diagnostic Engine:** Automated TCP/UDP throughput testing using integrated `iPerf3` services.
* **Hardware Push-Button Trigger:** On-demand physical test initiation via panel-mounted GPIO trigger.
* **Compact Telemetry Display:** Real-time metrics output directly on a 3.2-inch status display.
* **PCIe Port Expansion:** Enhanced high-speed Gigabit / 10GbE network interface testing via direct PCIe bus expansion.
* **JSON Telemetry Logging:** Standardized output format for integration into central monitoring dashboards.

---

## 🛠️ System Architecture

```text
+--------------------------------------------------------+
|                   Farlink NetEdge                      |
|                                                        |
|   +-------------------+       +--------------------+   |
|   | Raspberry Pi CM5  | <---> |  3.2" Display UI   |   |
|   +-------------------+       +--------------------+   |
|             |                                          |
|             +---------------> | Hardware Trigger   |   |
|             |                 | (Panel Push Button)|   |
|             |                                          |
|             v                                          |
|   +-------------------+                                |
|   | PCIe Ethernet IO  | --->  Target Network / Server  |
|   +-------------------+                                |
+--------------------------------------------------------+
