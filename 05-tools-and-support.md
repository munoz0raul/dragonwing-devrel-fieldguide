# 05 · Tools & Support

> The tools that get an attendee from "I have a board (or don't)" to "I'm running code," plus where to send them for help.
> Sourced from the Tools section of the docs — links inline.

---

## The developer tool belt

| Tool | What it does | Send them here |
|------|--------------|----------------|
| **Qualcomm Software Center (QSC)** | Desktop app to browse & manage Qualcomm **tools, SDKs, and chip software** from one place. The starting point. | [QSC overview](https://dragonwingdocs.qualcomm.com/Tools/Qualcomm-Software-Center/overview) |
| **Qualcomm Launcher** | **GUI to download, flash, and configure** an OS onto a dev kit — pick kit → pick OS → flash → set password/Wi-Fi. Easiest flashing path. | [Launcher overview](https://dragonwingdocs.qualcomm.com/Tools/Qualcomm-Launcher/overview) |
| **Qualcomm Device Cloud (QDC)** | **Real devices in the cloud** — start a session, SSH in, run preinstalled GStreamer AI samples, set up RTSP. **No hardware needed.** | [Device Cloud overview](https://dragonwingdocs.qualcomm.com/Tools/Qualcomm-Device-Cloud/overview) |
| **Qualcomm VS Code Extension (QVSCE)** | IDE for dev kits **inside VS Code** — manage/flash devices, SSH, download & **profile AI models**, sample projects, build/deploy/run from the status bar. Has a **built-in MCP server**. | [QVSCE intro](https://dragonwingdocs.qualcomm.com/Tools/QVSCE/introduction) |
| **SoM Development Tools** | Tools for working with the System-on-Module hardware. | [SoM tools](https://dragonwingdocs.qualcomm.com/Tools/SoM-Development-Tools/overview) |

📎 [All tools overview](https://dragonwingdocs.qualcomm.com/Tools/discover-tools)

---

## The three OS paths (know which to recommend)

| OS | Best for | Notes |
|----|----------|-------|
| **Qualcomm Linux (QLI)** | Production, embedded, deep system engineering | Yocto-based; the QIRP SDK path for robotics |
| **Ubuntu** | Rapid prototyping, dev-friendly, AI/ML | **QRB ROS** packages via Qualcomm IoT PPAs; **ROS 2 Jazzy** |
| **Windows** | Scalable IoT solutions | — |

**Booth rule of thumb:** *ROS developer prototyping →* **Ubuntu**. *Shipping an industrial product →* **Qualcomm Linux**.

---

## Flashing, quickly (when someone's stuck at the booth)

1. **Easiest:** **Qualcomm Launcher** — GUI, pick kit + OS, flash, configure Wi-Fi/password.
2. **Under the hood:** board enters **EDL** (Emergency Download) mode → flashed with **QDL** (Qualcomm Device Loader). USB shows as vendor ID `05c6:9008`.
3. **Watch for:** USB driver conflicts (Launcher has a troubleshooting page); on Windows, **WSL USB forwarding** via `usbipd`.

📎 [Flash the OS](https://dragonwingdocs.qualcomm.com/Tools/Qualcomm-Launcher/flash-os) · [USB driver conflicts](https://dragonwingdocs.qualcomm.com/Tools/Qualcomm-Launcher/troubleshooting/usb-driver-conflict)

---

## Where to send people for help

| Need | Link |
|------|------|
| **Main docs** | [dragonwingdocs.qualcomm.com](https://dragonwingdocs.qualcomm.com) |
| **Robotics code (QRB ROS)** | [github.com/qualcomm-qrb-ros](https://github.com/qualcomm-qrb-ros) |
| **Optimized AI models** | [aihub.qualcomm.com](https://aihub.qualcomm.com) |
| **Multimedia SDK docs** | [imsdkdocs.qualcomm.com](https://imsdkdocs.qualcomm.com) |
| **Developer portal** | [qualcomm.com/developer](https://www.qualcomm.com/developer) |
| **Support** | [qualcomm.com/support](https://www.qualcomm.com/support) |
| **Community forum** | [mysupport.qualcomm.com](https://mysupport.qualcomm.com) |

---

## The docs have an MCP server (nice devrel flex)

The documentation site exposes a **Model Context Protocol (MCP) server** at
`https://dragonwingdocs.qualcomm.com/mcp` — so a developer's AI assistant (Claude, Cursor, the QVSCE built-in server, etc.) can **search and read the docs directly**. Great "we built for AI-native workflows" talking point.

📎 [QVSCE integrated MCP server](https://dragonwingdocs.qualcomm.com/Tools/QVSCE/ai/mcp-server)

**Found a docs bug?** The MCP server also has a `submit_feedback` tool — report incorrect/outdated pages straight to the docs team.
