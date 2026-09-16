# 02 · Chips & Devices

> The Dragonwing silicon and dev-kit lineup, a side-by-side spec table, and **which board to recommend for which use case.**
> All specs pulled from official device-overview pages — links at the bottom of each section.

---

## The mental model

Every Dragonwing SoC is the same recipe at different scale:

> **Kryo CPU (Arm)** + **Adreno GPU** + **Hexagon DSP with HTP NPU** + **Real-Time SubSystem** on one chip.

You pick the tier by **how much AI (TOPS)**, **how many cameras**, and **how much memory** the application needs. The SoC sits on a **SoM** (module with memory + PMICs), which mounts on the **EVK mainboard** with all the connectors.

**Naming quick key:**
- **IQ-series** (IQ-615, IQ-8275, IQ-9075, IQ-X…) = the Dragonwing industrial/edge-AI product line.
- **QCS-series** (QCS6490, QCS5430) = compute SoCs; QCS6490 powers the **RB3 Gen 2** kit.
- Suffix **M** (e.g. IQ-9075M) = the module (SoM) that houses the SoC + memory + PMICs.

---

## Side-by-side spec cheat table

| | **RB3 Gen 2** (QCS6490) | **IQ-615** | **IQ-8275 EVK** | **IQ-9075 EVK** ⭐ |
|---|---|---|---|---|
| **Tier** | Affordable prototyping | Industrial entry | Mid / high | Flagship |
| **AI (TOPS)** | Hexagon HTP (not stated in device docs)¹ | Hexagon HTP (entry) | **up to 40 TOPS** | **up to 100 INT8 TOPS** |
| **CPU** | Kryo (1×Prime 2.7 + 3×Gold 2.4 + 4×Silver 1.9 GHz) | Kryo (2×Gold 1.9 + 6×Silver 1.6 GHz) | Octa Kryo Gen 6 (2.35/2.1/1.95 GHz) | Octa Kryo Gen 6 (up to 2.36 GHz) |
| **GPU** | Adreno 643 (812 MHz) | Adreno 612 (845 MHz) | Adreno 623 (up to 877 MHz) | Adreno 663 (up to 800 MHz) |
| **NPU** | Hexagon (HTP) | Hexagon (HTP) | Dual Hexagon Tensor Processors | Dual Hexagon Tensor Processors |
| **Memory** | LPDDR5/4 dual-channel | LPDDR4X 1555 MHz | up to **12 GB LPDDR5** (ECC) | up to **36 GB LPDDR5** (ECC) |
| **Cameras** | multiple | multiple | up to **16 concurrent** | up to **16 concurrent** |
| **Real-time cores** | — | — | Quad RT @ 1.85 GHz | Quad RT @ 1.85 GHz |
| **Temp range** | commercial/industrial | industrial | −40 to +105 °C | −40 to +85 °C |
| **Best for** | "I want to try ROS cheaply" | industrial entry / long-life | robotics + rich multimedia | max AI, multi-camera, GenAI on device |

> ¹ The Dragonwing docs give explicit TOPS only for IQ-8275 (40) and IQ-9075 (100). QCS6490 is commonly cited around ~12 TOPS elsewhere, but **that number isn't in these docs — don't quote it as official.** Send people to the RB3 Gen 2 product page for a guaranteed figure. IQ-615/RB3 CPU/GPU details come from the QLI performance-overview subsystem tables.

---

## IQ-9075 EVK — the flagship ⭐ (lead with this at the booth)

The headline board for edge AI and robotics.

- **AI:** Dual Hexagon Tensor Processors, **up to 100 TOPS**; runs **Llama 2 13B at ~12 tokens/sec** on-device.
- **CPU/GPU:** Octa-core Kryo Gen 6 (up to 2.36 GHz) + Adreno 663.
- **Real-Time Subsystem:** Quad real-time cores @ 1.85 GHz for low-latency motor/control loops.
- **Memory/Storage:** up to **36 GB LPDDR5** @ 3200 MHz with inline ECC; 2× 128 GB UFS 3.1, NVMe via PCIe.
- **Multimedia:** up to **16 concurrent cameras**, up to 12 displays, 8K60 decode.
- **Connectivity:** 2× 2.5 GbE, Wi-Fi 6E, BT 5.3, PCIe, USB, **CAN-FD**, MIPI CSI/DSI.
- **The module (IQ-9075M):** the SoC + **4× PMICs** + **3× LPDDR5** stacks; industrial −40 to +85 °C.
- **Target apps:** factory automation, AMRs, multi-camera vision, edge GenAI, industrial gateways.

**Talk-track:** *"This is 100 TOPS of edge AI with a real-time subsystem for control and 16-camera ingest — one chip for the perception, the AI, and the motion control of a robot."*

📎 [IQ-9075 device overview](https://dragonwingdocs.qualcomm.com/Linux/devices/iq9075-evk/device-overview)

---

## IQ-8275 EVK — the mid/high tier

Same architecture, tuned lower power/cost, widest temperature range.

- **AI:** Dual Hexagon Tensor Processors, **up to 40 TOPS**; also cites Llama 2 13B ~12 tok/s.
- **CPU/GPU:** Octa Kryo Gen 6 (2×Prime 2.35 + 2×Gold 2.1 + 4×Silver 1.95 GHz) + Adreno 623.
- **Memory:** up to **12 GB LPDDR5** with inline ECC; UFS 3.1, NVMe.
- **Multimedia:** up to 16 cameras, up to 12 displays.
- **Temp:** industrial **−40 to +105 °C**, junction up to +125 °C — the ruggedest of the group.
- **Part of the IQ8 Series.**

**Talk-track:** *"Same robotics-grade stack as the 9075, half the TOPS, even tougher temperature spec — great for deployed industrial units."*

📎 [IQ-8275 device overview](https://dragonwingdocs.qualcomm.com/Linux/devices/iq8275-evk/device-overview)

---

## IQ-615 — industrial entry

- **CPU:** Kryo — 2× Gold @ 1.9 GHz + 6× Silver @ 1.6 GHz.
- **GPU:** Adreno 612 @ 845 MHz.
- **Memory:** two-channel **LPDDR4X @ 1555 MHz**.
- Positioned for **industrial-grade** entry workloads on Qualcomm Linux.

📎 [IQ-615 in the QLI performance overview](https://dragonwingdocs.qualcomm.com/System/Performance/performance-overview#dragonwing-iq-615)

---

## RB3 Gen 2 Development Kit — the cheap on-ramp (QCS6490)

The board most ROS hobbyists/startups will actually start with.

- **SoC:** **QCS6490** — Kryo (1× Prime @ 2.7 GHz, 3× Gold @ 2.4 GHz, 4× Silver @ 1.9 GHz), **Adreno 643** @ 812 MHz.
- **Memory:** dual-channel LPDDR5 (3200 MHz) / LPDDR4.
- Includes the **Hexagon DSP** ("low-power processor") + **Qualcomm Sensing Hub (QSH)** running QuRT.
- Also a **RB3 Gen 2 Lite** variant (QCS5430).
- **AI Hub** supports RB3 Gen 2 via the **LiteRT** runtime (INT8/FP16/FP32 on CPU/GPU/HTP).

**Talk-track:** *"Want to try Qualcomm + ROS 2 without a big spend? Start on RB3 Gen 2 — same Hexagon NPU family, AI Hub support, runs the QRB ROS packages."*

📎 [RB3 Gen 2 / QCS6490 platform](https://dragonwingdocs.qualcomm.com/Technologies/Sensors/sensors-guide/topic/qcs6490/platform) · [QCS6490 subsystem specs](https://dragonwingdocs.qualcomm.com/System/Performance/performance-overview)

---

## IQ-X series — next-gen industrial

**IQ-X7181** and **IQ-X5121** are positioned as the **next-gen industrial platform and edge controllers**. Detailed specs live on the hardware doc portal (linked). Mention them as "the newer/higher industrial-controller tier" and hand off the link.

📎 [IQ-X7181 EVK](https://docs.qualcomm.com/doc/80-80023-261/topic/iqx-ug-landing-page.html) · [IQ-X5121 EVK](https://docs.qualcomm.com/doc/80-80022-297/80-80022-297_REV_AD_Qualcomm_IQ-X5xxx_Series_Evaluation_Kit_-_Linux.pdf)

---

## "Which board should I get?" — quick decision

- **"Cheapest way to try ROS 2 + Qualcomm AI"** → **RB3 Gen 2**.
- **"Serious robot, lots of cameras, on-device GenAI"** → **IQ-9075 EVK**.
- **"Deployed industrial unit, wide temp, cost-sensitive"** → **IQ-8275** (or **IQ-615** for entry).
- **"Edge controller / next-gen industrial"** → **IQ-X** series.
- **"I don't want to buy hardware yet"** → **Qualcomm Device Cloud** (remote real boards) — see [05](05-tools-and-support.md).

📎 Overview & board selector: [dragonwingdocs.qualcomm.com](https://dragonwingdocs.qualcomm.com)
