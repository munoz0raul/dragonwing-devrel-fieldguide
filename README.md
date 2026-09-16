# Dragonwing DevRel Field Guide

> A booth-ready reference for talking to **ROSCON** attendees as a Qualcomm **Dragonwing** Developer Relations rep.
> Grounded in the official docs at [dragonwingdocs.qualcomm.com](https://dragonwingdocs.qualcomm.com).
> Phone-friendly. Skim the talk-track, tap into a topic file when someone digs deeper.

---

## 🎯 30-second elevator pitch

> **Qualcomm Dragonwing** is Qualcomm's brand for **industrial & embedded IoT / edge-AI / robotics** silicon and dev kits.
> For robotics specifically: you get **Arm CPU + Adreno GPU + Hexagon NPU on one SoC**, running **up to 100 INT8 TOPS** of on-device AI, with a full **ROS 2 Jazzy** software stack (**QRB ROS** packages + the **QIR SDK**) that gives you **zero-copy sensor transport** and **NPU inference from a ROS node** — things stock ROS 2 can't do on its own. You can try it all in **Gazebo simulation without buying a board.**

If you remember one thing: **"Robotics-grade compute + real ROS 2 support + NPU acceleration, upstreamed and BSD-licensed."**

---

## 🗣️ Talk-track — who am I talking to → what to say → where to send them

| They are… | Lead with… | Send them to… |
|-----------|-----------|---------------|
| **ROS developer** ("does it run ROS 2?") | Yes — **ROS 2 Jazzy**, upstream **QRB ROS** packages, BSD-3, on GitHub. Zero-copy transport + NPU inference nodes. | [`github.com/qualcomm-qrb-ros`](https://github.com/qualcomm-qrb-ros) · [04-ros-robotics.md](04-ros-robotics.md) |
| **Embedded / BSP / Yocto person** ("can I build my own image?") | Yes — upstream Yocto: `meta-qcom` + `meta-ros` + `meta-qcom-robotics-sdk`, one `kas build`, RT-kernel option. | [Yocto+ROS section](04-ros-robotics.md#yocto--ros--qualcomm--building-your-own-robotics-image) |
| **AI / ML engineer** ("how do I run my model?") | **Qualcomm AI Hub** for ready-optimized models; **QAIRT** (QNN + SNPE) to bring your own PyTorch/ONNX and run on the **Hexagon HTP NPU**. | [aihub.qualcomm.com](https://aihub.qualcomm.com) · [03-ai-edge-inference.md](03-ai-edge-inference.md) |
| **Hardware / product person** ("which board?") | **RB3 Gen 2** to prototype cheap (QCS6490); **IQ-9075 EVK** for the flagship (100 TOPS, 16 cameras); **IQ-8275 / IQ-615** in between. | [02-chips-and-devices.md](02-chips-and-devices.md) |
| **"Just getting started"** | Grab a kit, flash with **Qualcomm Launcher**, or borrow a real board in **Qualcomm Device Cloud** — no hardware needed. | [05-tools-and-support.md](05-tools-and-support.md) |
| **Anyone lost in acronyms** (incl. me) | Open the decoder. | [01-acronyms.md](01-acronyms.md) |

---

## 📚 Files in this guide

| File | What's in it |
|------|--------------|
| [01-acronyms.md](01-acronyms.md) | **Acronym decoder** — the full Qualcomm/AI/robotics alphabet soup, grouped and A–Z. Your booth safety net. |
| [02-chips-and-devices.md](02-chips-and-devices.md) | The SoC/SoM & dev-kit lineup, a side-by-side spec table, and **"which board for which use case."** |
| [03-ai-edge-inference.md](03-ai-edge-inference.md) | The edge-AI story: NPU/Hexagon/TOPS, **QAIRT (QNN + SNPE)**, **AI Hub**, and the model port workflow. |
| [04-ros-robotics.md](04-ros-robotics.md) | **★ ROSCON core.** QIR SDK, the `qrb_ros_*` packages, zero-copy, NPU-from-ROS, SLAM/Nav2, simulation. |
| [05-tools-and-support.md](05-tools-and-support.md) | Software Center, Launcher, Device Cloud, VS Code extension, forums & support links. |
| [06-booth-faq.md](06-booth-faq.md) | Likely attendee questions with crisp answers + where to send them. |

---

## ⚡ Numbers worth memorizing

- **IQ-9075**: up to **100 INT8 TOPS**, octa-core Kryo Gen 6, Adreno 663, up to **36 GB LPDDR5**, **16 cameras**, Llama 2 13B ≈ **12 tok/s** on device.
- **IQ-8275**: up to **40 TOPS**, same CPU family, up to 12 GB LPDDR5 — the mid tier.
- **RB3 Gen 2**: **QCS6490** (Kryo up to 2.7 GHz, Adreno 643, Hexagon HTP) — the affordable ROS/prototyping entry point. (Docs don't state a TOPS figure — don't quote one.)
- ROS 2 flavor = **Jazzy**. All QRB ROS packages are **BSD-3-Clause**, upstream on GitHub.

> ⚠️ Accuracy note: every spec here is pulled from the official Dragonwing docs and each topic file links back to its source. If an attendee needs a guaranteed number for a datasheet/design decision, point them at the linked product page rather than quoting from memory.

---

*Built for internal DevRel use. Not an official Qualcomm publication — always defer to [dragonwingdocs.qualcomm.com](https://dragonwingdocs.qualcomm.com) and official datasheets.*
