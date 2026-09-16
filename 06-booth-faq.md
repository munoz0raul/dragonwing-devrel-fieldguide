# 06 · Booth FAQ

> Rapid-fire answers for the questions you'll actually get at a ROSCON booth. Keep it short, then hand off a link.

---

### "What is Dragonwing?"
Qualcomm's brand for **industrial & embedded IoT / edge-AI / robotics** silicon and dev kits. One recipe across the line: **Kryo CPU + Adreno GPU + Hexagon NPU + real-time cores** on a single SoC. → [02](02-chips-and-devices.md)

### "Does it run ROS 2?"
Yes — **ROS 2 Jazzy**, with Qualcomm's upstream **QRB ROS** packages (BSD-3-Clause) on GitHub, plus the **QIR/QIRP SDK**. → [04](04-ros-robotics.md) · [github.com/qualcomm-qrb-ros](https://github.com/qualcomm-qrb-ros)

### "Why not just use my x86 box with a GPU?"
On Dragonwing you get, on one power-efficient module: **NPU inference from a ROS node** (no community equivalent), **DMA-buf zero-copy** sensor transport, integrated **ISP/multi-camera**, **real-time control cores**, and **industrial temperature** range. → [04](04-ros-robotics.md)

### "How much AI performance?"
**IQ-9075: up to 100 INT8 TOPS** (runs Llama 2 13B ~12 tok/s on-device). **IQ-8275: up to 40 TOPS.** RB3 Gen 2 is the affordable entry. → [02](02-chips-and-devices.md)

### "What's the NPU actually called?"
The **HTP** — Hexagon Tensor Processor — inside the **Hexagon DSP**. Fastest at INT8/INT16. → [03](03-ai-edge-inference.md)

### "How do I run my own model?"
Two paths: **AI Hub** (pick/upload a model, it compiles + profiles on a real device) or **QAIRT** (QNN/SNPE) to convert+quantize yourself. Frameworks in: **PyTorch, TensorFlow, ONNX, LiteRT.** → [03](03-ai-edge-inference.md) · [aihub.qualcomm.com](https://aihub.qualcomm.com)

### "How do I run a model *from ROS*?"
`qrb_ros_nn_inference` — a generic ROS 2 node that runs your model on the **HTP NPU via the QNN delegate**. → [04](04-ros-robotics.md)

### "What's the zero-copy thing?"
`qrb_ros_transport` passes a **DMA-buf file descriptor** between nodes instead of memcpy-ing every camera frame/point cloud. Big latency + CPU win. → [04](04-ros-robotics.md)

### "Which board should I buy?"
- Cheapest ROS on-ramp → **RB3 Gen 2** (QCS6490)
- Flagship robot, 16 cameras, on-device GenAI → **IQ-9075 EVK**
- Rugged deployed industrial unit → **IQ-8275** (or **IQ-615** entry)
- Next-gen edge controller → **IQ-X** series
→ [02](02-chips-and-devices.md)

### "Can I try it without buying hardware?"
Two ways: **`qrb_ros_simulation`** (Gazebo — AMRs & arms, run tonight) or **Qualcomm Device Cloud** (SSH into a real board in the cloud). → [04](04-ros-robotics.md) · [05](05-tools-and-support.md)

### "Which OS should I use?"
Prototyping/ROS → **Ubuntu** (QRB ROS via PPAs). Shipping a product → **Qualcomm Linux** (QIRP SDK). Also **Windows** for IoT. → [05](05-tools-and-support.md)

### "How do I flash it?"
Easiest: **Qualcomm Launcher** (GUI). Under the hood: **EDL** mode + **QDL** tool. → [05](05-tools-and-support.md)

### "Can I build a custom Yocto image with ROS baked in?"
Yes — it's the production path. Upstream **Yocto/OpenEmbedded** via **KAS**: `meta-qcom` (BSP) + `meta-ros` + Qualcomm's **`meta-qcom-robotics-sdk`** layer (tag `qli-2.0`), which adds **ROS 2 Jazzy**, the `qrb_ros` packages, **Nav2/MoveIt/Cartographer**, and a **real-time kernel** option. One `kas build` line → a flashable `qcom-robotics-image`. → [04](04-ros-robotics.md)

### "What's the license? Is it open?"
All **QRB ROS** packages are **BSD-3-Clause**, upstream on GitHub. The stack builds on **Yocto / OpenEmbedded / meta-ros**. → [04](04-ros-robotics.md)

### "ROS 2 Jazzy — supported on all boards?"
QRB ROS currently targets **IQ-9075 EVK** and **IQ-8 (Beta) EVK** on Ubuntu; QIRP SDK covers Qualcomm Linux. Confirm a specific board on the docs. → [04](04-ros-robotics.md)

### "Do you have SLAM / navigation samples?"
Yes — **Cartographer** (2D LiDAR SLAM), **Nav2**, **AprilTag**, pick-and-place, AMR motion — most run in **simulation** too. → [04](04-ros-robotics.md)

### "What sensors are supported out of the box?"
Samples for **Orbbec Gemini 335L** depth camera and **RPLIDAR** (`rplidar-ros2`), plus system-monitor, audio, and OCR services. → [04](04-ros-robotics.md)

### "Where do I get help / report a docs bug?"
Docs: [dragonwingdocs.qualcomm.com](https://dragonwingdocs.qualcomm.com) · Forum: [mysupport.qualcomm.com](https://mysupport.qualcomm.com) · Support: [qualcomm.com/support](https://www.qualcomm.com/support). Docs even expose an **MCP server** so AI assistants can read them. → [05](05-tools-and-support.md)

---

### 🆘 If I get a question I can't answer
1. "Great question — let me get you the exact answer rather than guess."
2. Grab their contact / point them at [mysupport.qualcomm.com](https://mysupport.qualcomm.com).
3. Note it — recurring questions are gold for the docs/DevRel team (and the `submit_feedback` MCP tool).
