# 04 · ROS & Robotics — ★ ROSCON core

> **This is the file to know cold at ROSCON.** What Qualcomm + ROS gives a roboticist, package by package, and how to try each — including **without buying a board**.
> Sourced from the QRB ROS overview and QIR SDK docs — links inline.

---

## The pitch in three sentences

> **QRB ROS** is Qualcomm's upstream collection of **ROS 2 Jazzy** packages for robotics — all **BSD-3-Clause**, all on GitHub. They give you three things stock ROS 2 can't do on Qualcomm silicon by itself: **run inference on the Hexagon HTP NPU from a ROS node**, **share camera/point-cloud buffers zero-copy via DMA-buf**, and **packaged accelerator-correct pipelines** (detection, depth, SLAM, Nav2, pick-and-place). And you can **evaluate the whole thing in Gazebo simulation without any hardware**.

**Target:** Ubuntu on Qualcomm IoT platforms, **ROS 2 Jazzy**, on **IQ-9075 EVK** and **IQ-8 (Beta) EVK**. Packages ship via the Qualcomm IoT PPAs (`ppa:ubuntu-qcom-iot/qcom-ppa` and `.../qirp`). For **Qualcomm Linux**, the equivalent is the **QIRP SDK**.

---

## How this differs from stock ROS 2 (the three real differentiators)

1. **Hexagon HTP NPU access.** Stock TFLite/ONNX ROS nodes run on CPU or OpenCL GPU only. Reaching the **HTP NPU** needs the Qualcomm **QNN delegate** — **no community equivalent exists.**
2. **DMA-buf camera sharing.** Stock `image_transport` + `sensor_msgs::Image` serialize and **memcpy** every frame between nodes. `qrb_ros_transport` passes a **DMA-buf file descriptor** instead — the frame the camera ISP wrote stays put until the next hardware consumer reads it. **True zero-copy.**
3. **Packaged accelerator-correct pipelines.** `qrb_ros_samples` wires camera ingest + QNN inference + pre/post-processing into launch files, so you don't hand-build the plumbing.

**Booth line:** *"Three things you can't get from stock ROS 2 here: the NPU from a ROS node, real zero-copy sensor transport, and pipelines that are already wired correctly for the accelerators."*

---

## The package map (GitHub org: [`qualcomm-qrb-ros`](https://github.com/qualcomm-qrb-ros))

| Repo | Purpose | License |
|------|---------|---------|
| [`qrb_ros_transport`](https://github.com/qualcomm-qrb-ros/qrb_ros_transport) | **Zero-copy** ROS 2 transport types (Image, PointCloud2) via DMA-buf | BSD-3 |
| [`qrb_ros_nn_inference`](https://github.com/qualcomm-qrb-ros/qrb_ros_nn_inference) | **Generic QNN inference** ROS node → runs a model on the **HTP NPU** | BSD-3 |
| [`qrb_ros_samples`](https://github.com/qualcomm-qrb-ros/qrb_ros_samples) | AI + robotics **sample pipelines** (detection, depth, pose, Nav2, AprilTag, pick-and-place) | BSD-3 |
| [`qrb_ros_simulation`](https://github.com/qualcomm-qrb-ros/qrb_ros_simulation) | **Gazebo** sim of QRB AMRs and arms — try without hardware | BSD-3 |
| [`qrb_ros_benchmark`](https://github.com/qualcomm-qrb-ros/qrb_ros_benchmark) | `ros2_benchmark` extension to measure zero-copy wins vs. stock | BSD-3 |
| [`ROS2-DDSConfig-Optimizer`](https://github.com/qualcomm-qrb-ros/ROS2-DDSConfig-Optimizer) | **LLM-driven FastDDS QoS auto-tuner** (works on any ROS 2 setup) | BSD-3 |
| [`qrb_ros_tensor_process`](https://github.com/qualcomm-qrb-ros/qrb_ros_tensor_process) | YOLO pre/post-processing nodes | BSD-3 |
| [`qrb_ros_color_space_convert`](https://github.com/qualcomm-qrb-ros/qrb_ros_color_space_convert) | NV12 ↔ RGB8 GPU-accelerated converter | BSD-3 |
| [`qrb_ros_image_resize`](https://github.com/qualcomm-qrb-ros/qrb_ros_image_resize) | EVA-accelerated NV12 downscaler | BSD-3 |

Also upstreamed and **portable to any Linux SoC with a DMA heap** (nice "we contribute upstream" story):
- [`dmabuf_transport`](https://github.com/qualcomm-qrb-ros/dmabuf_transport) — portable REP-2007 adapted types
- [`lib_mem_dmabuf`](https://github.com/qualcomm-qrb-ros/lib_mem_dmabuf) — userspace DMA-buf helper

> `qrb_ros_transport` is built on top of both, so users don't touch them directly.

---

## "Pick your level of abstraction" (great for the *how deep do I go?* question)

| Level | What you use | Example |
|-------|--------------|---------|
| **From scratch** | QNN delegate + stock ROS 2 + an AI Hub model, wired yourself | the hand-rolled depth pipeline (NPU Workflows) |
| **Generic NPU node** | `qrb_ros_nn_inference` + your own AI Hub model | drop-in QNN inference on any topic |
| **Reference pipeline** | a `qrb_ros_samples` entry, as-is or lightly modified | `sample_depth_estimation` |

All three target the **same silicon** and **interoperate on the same ROS graph** — they compose, you don't have to choose one camp.

---

## The QIR SDK (Qualcomm Intelligent Robotics SDK)

The **QIR SDK 2.0** is the batteries-included robotics SDK. It's built on **Yocto** and stacks:

- **Qualcomm Linux Distribution** — foundational Linux + multimedia.
- **Robotics SDK layers** — the robot-specific support.
- **meta-ros layer** — OpenEmbedded layers that add ROS to the Yocto build.

It also pulls in **function SDKs**: the **IM SDK** (GStreamer-based AI/multimedia pipelines), the **Neural Processing SDK (SNPE)**, and **AI Engine Direct (QNN)**. On Qualcomm Linux this SDK is called the **QIRP SDK**.

**What you can do with it:** flash a robotics image (QDL), run demo apps, build sample ROS 2 apps, and build/customize the image with a prebuilt **eSDK**. There's a full **1.0 → 2.0 migration guide**.

📎 [QIR SDK overview](https://dragonwingdocs.qualcomm.com/SDKs/QIR-SDK-2.0/qir-sdk-overview) · [Software architecture](https://dragonwingdocs.qualcomm.com/SDKs/QIR-SDK-2.0/qir-software-architecture) · [Get started](https://dragonwingdocs.qualcomm.com/SDKs/QIR-SDK-2.0/get-started-with-qir-sdk)

---

## Samples you can name-drop

**AI vision:** object detection, object segmentation, **depth estimation**, **HRNet pose estimation**, face detection, hand detection, ResNet-101 classification.
**Robotics:** **2D LiDAR SLAM with Cartographer**, **Navigation2 (Nav2)**, **AprilTag** pipeline, pick-and-place, AMR simple motion, remote assistant.
**Platform:** Orbbec Gemini 335L depth camera, RPLIDAR (`rplidar-ros2`), system monitor (`qrb_ros_system_monitor`), OCR service, audio service (`qrb_ros_audio_service`), colorspace convert (NV12↔RGB).

Most robotics samples run **in the simulator too**, so a booth demo doesn't need the physical robot.

📎 [QIR sample applications](https://dragonwingdocs.qualcomm.com/SDKs/QIR-SDK-2.0/qir-sdk-sample-applications) · [Run robotics samples](https://dragonwingdocs.qualcomm.com/SDKs/QIR-SDK-2.0/run-robotics-sample-applications)

---

## "Try it without hardware" (your best booth CTA)

Point people at **`qrb_ros_simulation`** — pre-built **AMR and manipulator** configs in **Gazebo**. They can evaluate the transport types, NPU sample flow, Nav2 and pick-and-place entirely in sim. Pair with the **DDS optimizer** (works on any ROS 2 install, no Qualcomm HW).

**Booth line:** *"You don't need to buy a board today — clone `qrb_ros_simulation`, run the AMR in Gazebo tonight, and the same launch files move to real hardware later."*

---

## Fast answers for ROS devs
- *"Which ROS 2 distro?"* → **Jazzy.**
- *"License?"* → **BSD-3-Clause**, all of it, upstream on GitHub.
- *"How do I get the packages?"* → Ubuntu: Qualcomm IoT **PPAs**; Qualcomm Linux: **QIRP SDK**.
- *"Do I need Qualcomm HW to start?"* → No — **Gazebo sim** + the DDS optimizer run anywhere.
- *"What's actually special vs. my x86 + discrete GPU?"* → NPU-from-ROS, DMA-buf zero-copy, integrated ISP/camera, real-time cores, industrial temp — on one power-efficient module.
- *"Where's the code?"* → **[github.com/qualcomm-qrb-ros](https://github.com/qualcomm-qrb-ros)**.
