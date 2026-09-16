# 01 · Acronym Decoder

> Your booth safety net. Two ways in: **[grouped by topic](#grouped-by-topic)** (for "what's the AI stuff called again?") and **[straight A–Z](#az-master-list)** (for "what does XYZ mean?").
> Combines the working Qualcomm/AI/robotics glossary with terms pulled from the Dragonwing docs.

---

## Grouped by topic

### 🤖 Robotics & ROS (ROSCON-critical)
| Term | Meaning |
|------|---------|
| **ROS / ROS 2** | Robot Operating System — the middleware everyone at ROSCON uses. Dragonwing targets **ROS 2 Jazzy**. |
| **QIR** | Qualcomm Intelligent Robotics (SDK) — Qualcomm's robotics SDK on top of Yocto + ROS. |
| **QIRP** | Qualcomm Intelligent Robotics Product (SDK) — the QIR SDK name used on Qualcomm Linux. |
| **QRB / QRB ROS** | Qualcomm Robotics Brand — the upstream `qrb_ros_*` ROS 2 package family on GitHub. |
| **AMR** | Autonomous Mobile Robot. |
| **SLAM** | Simultaneous Localization and Mapping. |
| **Nav2** | ROS 2 Navigation stack. |
| **DDS** | Data Distribution Service — the ROS 2 comms layer (e.g. FastDDS). |
| **QoS** | Quality of Service — DDS tuning knobs (reliability, history, etc.). |
| **DMA-buf** | DMA Buffer — kernel mechanism for sharing buffers without copying; basis of zero-copy transport. |
| **REP** | ROS Enhancement Proposal (e.g. REP 2007 for type adaptation). |
| **eSDK** | extensible SDK — a Yocto-derived SDK you can build images with. |
| **AprilTag** | Fiducial marker system used for robot localization/pick-and-place. |
| **EVA** | Qualcomm's computer-vision hardware engine (used for accelerated image resize). |

### 🧠 AI / Compute
| Term | Meaning |
|------|---------|
| **NPU** | Neural Processing Unit — the AI accelerator. |
| **HTP** | Hexagon Tensor Processor — the NPU inside the Hexagon DSP; the INT8/INT16 inference engine. |
| **HVX** | Hexagon Vector eXtensions. |
| **HMX** | Hexagon Matrix eXtensions. |
| **TOPS** | Tera Operations Per Second — AI throughput (usually quoted at INT8). |
| **QAIRT** | Qualcomm AI Runtime (SDK) — the all-in-one SDK to port/run models; contains SNPE + QNN. |
| **QNN** | Qualcomm Neural Network / AI Engine Direct — low-level runtime & the ROS "QNN delegate." |
| **SNPE** | Snapdragon Neural Processing Engine — older/high-level neural runtime (C/C++/Java APIs). |
| **AI Hub** | Qualcomm AI Hub — library of pre-optimized models + cloud compile/profile on real devices. |
| **DLC** | Deep Learning Container — SNPE's compiled model format. |
| **LiteRT** | Lite Runtime (formerly TFLite) — runtime supported for RB3 Gen 2 via AI Hub. |
| **ONNX** | Open Neural Network Exchange — model interchange format. |
| **AIMET** | AI Model Efficiency Toolkit — quantization/compression. |
| **INT8 / INT16 / FP16 / FP32** | Numeric precisions; NPU is fastest at INT8/INT16. |
| **LLM / VLM** | Large Language Model / Vision-Language Model. |
| **GenAI** | Generative AI. |
| **TTFT / TPS** | Time To First Token / Tokens Per Second — LLM latency & throughput metrics. |

### 🔩 Silicon & hardware
| Term | Meaning |
|------|---------|
| **SoC** | System on Chip — the main processor (e.g. IQ-9075, QCS6490). |
| **SoM** | System on Module — the SoC + memory + PMICs on a module (e.g. IQ-9075M). |
| **EVK** | Evaluation Kit — the dev board (e.g. IQ-9075 EVK). |
| **QCS** | Qualcomm Communication/Compute SoC (e.g. QCS6490, QCS5430). |
| **Kryo** | Qualcomm's Arm-based CPU brand. |
| **Adreno** | Qualcomm's GPU brand. |
| **Hexagon** | Qualcomm's DSP brand (hosts the HTP NPU). |
| **RTSS** | Real-Time SubSystem — dedicated real-time cores for low-latency control. |
| **PMIC** | Power Management IC. |
| **LPDDR5 / LPDDR4X** | Low-Power DDR SDRAM generations. |
| **ECC** | Error-Correcting Code (memory). |
| **UFS** | Universal Flash Storage. |
| **eMMC** | embedded MultiMediaCard (flash). |
| **ISP** | Image Signal Processor. |
| **VPU** | Video Processing Unit (encode/decode). |
| **TPM** | Trusted Platform Module. |
| **IMU** | Inertial Measurement Unit. |
| **CAN / CAN-FD** | Controller Area Network (Flexible Data-rate) — industrial/vehicle bus. |

### 🔌 Connectivity & I/O
| Term | Meaning |
|------|---------|
| **PCIe** | Peripheral Component Interconnect Express. |
| **MIPI CSI / DSI** | Camera Serial Interface / Display Serial Interface. |
| **C-PHY / D-PHY** | MIPI physical layers for cameras. |
| **GbE / SGMII** | Gigabit Ethernet / Serial Gigabit Media-Independent Interface. |
| **UART** | Universal Asynchronous Receiver-Transmitter (serial console). |
| **I2C / I3C / SPI / I2S** | Common low-speed peripheral buses (I2S = audio). |
| **QUP** | Qualcomm Universal Peripheral (configurable serial engine). |
| **GPIO** | General Purpose Input/Output. |
| **USB / ADB** | Universal Serial Bus / Android Debug Bridge. |
| **RTSP** | Real-Time Streaming Protocol (video streaming). |

### 🛠️ Tools, OS & platform
| Term | Meaning |
|------|---------|
| **QLI** | Qualcomm Linux (Image) — production embedded Linux distro. |
| **Yocto** | The embedded-Linux build system QLI/QIR are built on. |
| **meta-ros / OpenEmbedded** | Yocto layers that add ROS support. |
| **QSC** | Qualcomm Software Center — desktop app to get tools/SDKs/chip software. |
| **QVSCE** | Qualcomm VS Code Extension — IDE integration for dev kits. |
| **QDC** | Qualcomm Device Cloud — real remote devices for sessions/testing. |
| **QDL** | Qualcomm Device Loader — command-line flashing tool. |
| **EDL** | Emergency Download (mode) — the state a board enters to be flashed. |
| **QFIL** | Qualcomm Flash Image Loader. |
| **QSH** | Qualcomm Sensing Hub (low-power sensor processing). |
| **QuRT** | Qualcomm Real-Time OS running on the Hexagon DSP. |
| **BSP** | Board Support Package. |
| **OTA / FOTA** | Over-The-Air (Firmware) update. |
| **SDK / API / CLI** | Software Development Kit / Application Programming Interface / Command-Line Interface. |
| **WSL** | Windows Subsystem for Linux (needed for some Windows flashing flows). |

### 🏢 Org / process
| Term | Meaning |
|------|---------|
| **DevRel** | Developer Relations — you! |
| **QTI / QCT** | Qualcomm Technologies Inc. / Qualcomm CDMA Technologies. |
| **PR / RFC / LKML** | Pull Request / Request for Comments / Linux Kernel Mailing List. |
| **GA / RC / POC** | General Availability / Release Candidate / Proof of Concept. |
| **BSD-3-Clause** | The permissive open-source license used by all QRB ROS packages. |

---

## A–Z master list

**A** — Adreno (GPU) · AI Hub · AIMET (AI Model Efficiency Toolkit) · AMR (Autonomous Mobile Robot) · API (Application Programming Interface) · AprilTag
**B** — BSD-3-Clause · BSP (Board Support Package)
**C** — CAN/CAN-FD (Controller Area Network) · CLI (Command-Line Interface) · CSI (Camera Serial Interface) · C-PHY
**D** — DDS (Data Distribution Service) · DevRel (Developer Relations) · DLC (Deep Learning Container) · DMA-buf (DMA Buffer) · DSI (Display Serial Interface) · DSP (Digital Signal Processor)
**E** — ECC (Error-Correcting Code) · EDL (Emergency Download mode) · eMMC · eSDK (extensible SDK) · EVA (vision engine) · EVK (Evaluation Kit)
**F** — FOTA (Firmware Over-The-Air) · FP16/FP32 (floating-point precision)
**G** — GA (General Availability) · GbE (Gigabit Ethernet) · GenAI (Generative AI) · GPIO · GPU (Graphics Processing Unit)
**H** — HTP (Hexagon Tensor Processor) · Hexagon (DSP brand) · HMX (Hexagon Matrix eXtensions) · HVX (Hexagon Vector eXtensions)
**I** — I2C · I2S (audio) · I3C · IMU (Inertial Measurement Unit) · INT8/INT16 · ISP (Image Signal Processor)
**K** — Kryo (CPU brand)
**L** — LiteRT (Lite Runtime, ex-TFLite) · LKML · LLM (Large Language Model) · LPDDR4X/LPDDR5 (Low-Power DDR)
**M** — meta-ros · MIPI (Mobile Industry Processor Interface)
**N** — Nav2 (ROS 2 Navigation) · NPU (Neural Processing Unit)
**O** — ONNX (Open Neural Network Exchange) · OpenEmbedded · OTA (Over-The-Air)
**P** — PCIe · PMIC (Power Management IC) · POC (Proof of Concept) · PR (Pull Request)
**Q** — QAIRT (Qualcomm AI Runtime) · QCS (Qualcomm Compute/Comms SoC) · QDC (Qualcomm Device Cloud) · QDL (Qualcomm Device Loader) · QFIL (Qualcomm Flash Image Loader) · QIR (Qualcomm Intelligent Robotics) · QIRP (…Product SDK) · QLI (Qualcomm Linux) · QNN (Qualcomm Neural Network / AI Engine Direct) · QoS (Quality of Service) · QRB (Qualcomm Robotics Brand) · QSC (Qualcomm Software Center) · QSH (Qualcomm Sensing Hub) · QTI/QCT (Qualcomm Technologies/CDMA) · QUP (Qualcomm Universal Peripheral) · QuRT (Qualcomm Real-Time OS) · QVSCE (Qualcomm VS Code Extension)
**R** — RC (Release Candidate) · REP (ROS Enhancement Proposal) · RFC · ROS/ROS 2 (Robot Operating System) · RTSP (Real-Time Streaming Protocol) · RTSS (Real-Time SubSystem)
**S** — SDK · SGMII · SLAM (Simultaneous Localization and Mapping) · SNPE (Snapdragon Neural Processing Engine) · SoC (System on Chip) · SoM (System on Module) · SPI
**T** — TFLite (now LiteRT) · TOPS (Tera Operations Per Second) · TPM (Trusted Platform Module) · TPS (Tokens Per Second) · TTFT (Time To First Token)
**U** — UART · UFS (Universal Flash Storage) · USB
**V** — VLM (Vision-Language Model) · VPU (Video Processing Unit)
**W** — WSL (Windows Subsystem for Linux)
**Y** — Yocto (embedded-Linux build system)

---
📎 **Source:** term definitions verified against [dragonwingdocs.qualcomm.com](https://dragonwingdocs.qualcomm.com) device, AI-workflow, and QRB ROS pages. See [02](02-chips-and-devices.md)–[04](04-ros-robotics.md) for where each is used in context.
