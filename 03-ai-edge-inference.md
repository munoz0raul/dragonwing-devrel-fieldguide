# 03 · AI & Edge Inference

> The edge-AI story for a technical attendee: **where inference runs**, **how a model gets there**, and the **two paths** (ready-made vs. bring-your-own).
> Sourced from the AI Developer Workflow and AI Hub docs — links inline.

---

## The one-paragraph version

> Dragonwing SoCs have a **Hexagon DSP with a Tensor Processor (HTP)** — that's the **NPU** where quantized models run fastest (INT8/INT16). You get models onto it two ways: grab a **pre-optimized model from Qualcomm AI Hub**, or **bring your own** PyTorch/ONNX model and convert+quantize it with the **QAIRT SDK** (which contains **QNN** and **SNPE**). At runtime you target **CPU, GPU, or HTP** — HTP for max performance-per-watt.

---

## Where inference can run (the runtimes/backends)

| Backend | What it is | When to use |
|---------|-----------|-------------|
| **CPU (Kryo)** | Arm cores | Fallback, debugging, tiny models |
| **GPU (Adreno)** | via OpenCL | FP16/FP32 vision workloads |
| **HTP (Hexagon Tensor Processor)** | the **NPU** | **Default for production** — best perf/watt, INT8/INT16 |

**Booth line:** *"The NPU is the HTP inside the Hexagon DSP. That's where you want your quantized model — it's the whole reason to pick this silicon for edge AI."*

---

## The software stack — QAIRT (QNN + SNPE)

**QAIRT = Qualcomm AI Runtime SDK** — the all-in-one SDK to port ML models to Qualcomm accelerators. It contains two runtimes:

| | **QNN** (AI Engine Direct) | **SNPE** (Neural Processing Engine) |
|---|---|---|
| Full name | Qualcomm Neural Network / AI Engine Direct | Snapdragon Neural Processing Engine |
| Level | Lower-level, newer, graph-oriented | Higher-level, C/C++/Java APIs |
| Model format | QNN model libs / context binaries | **DLC** (Deep Learning Container) |
| In ROS | the **"QNN delegate"** used by `qrb_ros_nn_inference` | — |
| Run tool | — | `snpe-net-run` |

Both **convert and quantize** models trained in **PyTorch / TensorFlow / ONNX / LiteRT**, then run them on **CPU, GPU, or HTP**.

📎 [QAIRT overview](https://dragonwingdocs.qualcomm.com/Key-Documents/AI-Developer-Workflow/topic/qairt) · [Convert & quantize (port models)](https://dragonwingdocs.qualcomm.com/Key-Documents/AI-Developer-Workflow/topic/port-models) · [Run models](https://dragonwingdocs.qualcomm.com/Key-Documents/AI-Developer-Workflow/topic/run-models)

---

## Two paths to a running model

### Path A — Qualcomm AI Hub (fastest; recommend first)
A library of **pre-optimized models** plus a cloud service that **compiles, profiles, and runs inference on real devices** from a device farm.

**Bring your own model to AI Hub:**
1. Start from a pretrained **PyTorch or ONNX** model.
2. Submit a **compile job** via Python API, selecting your **device/chipset** + **target runtime**.
3. AI Hub optimizes for that device; optionally **profile** or **run inference** on a provisioned real device.

Example — **RB3 Gen 2** target via AI Hub:

| Chipset | Runtime | CPU | GPU | HTP |
|---------|---------|-----|-----|-----|
| RB3 Gen 2 | **LiteRT** | INT8, FP16, FP32 | FP16, FP32 | **INT8, INT16** |

**Booth line:** *"Don't hand-port anything to start — go to AI Hub, pick a model or upload yours, choose your board, and it compiles + benchmarks on a real device in the cloud."*

📎 [AI Hub workflow](https://dragonwingdocs.qualcomm.com/Key-Documents/AI-Developer-Workflow/topic/ai-hub) · [aihub.qualcomm.com](https://aihub.qualcomm.com)

### Path B — Bring your own model with QAIRT (full control)
1. **Convert** PyTorch/TF/ONNX/LiteRT → QNN or SNPE (DLC) format.
2. **Quantize** to INT8/INT16 (with a calibration input list) for the HTP.
3. **Run** on target via `snpe-net-run` (SNPE) or the QNN runtime — selecting CPU/GPU/HTP.

📎 [Port models](https://dragonwingdocs.qualcomm.com/Key-Documents/AI-Developer-Workflow/topic/port-models)

---

## How this shows up in robotics (the ROSCON connection)

The AI stack plugs straight into ROS 2 — this is the important bridge for your audience:

- **`qrb_ros_nn_inference`** — a generic ROS 2 node that loads a model and runs it on the **HTP NPU via the QNN delegate**. Stock TFLite/ONNX ROS nodes only reach CPU/GPU; there's **no community equivalent** for the NPU.
- **`qrb_ros_samples`** — ready pipelines: object detection, segmentation, pose (HRNet), **depth estimation**, face/hand detection, ResNet-101 classification.

See [04-ros-robotics.md](04-ros-robotics.md) for the full package tour.

**Booth line:** *"The reason to run AI on this in ROS isn't just the chip — it's that we give you a ROS node that actually reaches the NPU. That's the missing piece in stock ROS 2."*

---

## GenAI / LLMs on device

- IQ-9075 runs **Llama 2 13B at ~12 tokens/sec** locally (dual HTP, up to 36 GB LPDDR5).
- There are **LLM/VLM services** and audio-analytics APIs in the Ubuntu AI-workflows docs (OpenAPI specs published).

📎 [AI Developer Workflow hub](https://dragonwingdocs.qualcomm.com/Key-Documents/AI-Developer-Workflow/topic/port-models)

---

## Quick answers you'll get asked
- *"What frameworks?"* → PyTorch, TensorFlow, ONNX, LiteRT in; QNN/SNPE(DLC) on device.
- *"What precision on the NPU?"* → INT8 / INT16 (FP16/FP32 on GPU).
- *"Do I have to quantize?"* → For best HTP performance, yes; AI Hub can do it for you.
- *"Where do I even start?"* → **AI Hub** → pick board → compile → profile on a real device.
