# yolo-nas-docker-env
A Docker environment optimized for training and running YOLO-NAS models with SuperGradients and PyTorch (CUDA 12) support. Includes essential fixes for model downloads, checkpoint handling, and Jupyter Notebook integration.

# YOLO-NAS Docker Environment

This repository provides a **pre-configured Docker environment** for training and running **YOLO-NAS** models using SuperGradients and PyTorch with CUDA support.

## 🚀 Features
- **Based on NVIDIA PyTorch (CUDA 12)**: Uses `nvcr.io/nvidia/pytorch:23.10-py3` as the base image.
- **Fixes for SuperGradients**:
  - Corrects **broken model download URLs**.
  - Fixes **checkpoint filename parsing**.
- **Ensures GPU compatibility** by enforcing a CUDA-enabled PyTorch installation.
- **Pre-installed dependencies** including `super_gradients`, `torch`, `torchvision`, `torchaudio`, `opencv-python-headless`, and more.
- **Jupyter Notebook pre-configured** (No token authentication required).

## 🛠 Installation & Usage

### 1️⃣ Clone this repository
```bash
git clone https://github.com/your-username/yolo-nas-docker-env.git
cd yolo-nas-docker-env

