# Use NVIDIA PyTorch base image with CUDA 12 support
FROM nvcr.io/nvidia/pytorch:23.10-py3

# Set environment variable to prevent interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Set working directory
WORKDIR /workspace

# Install dependencies (Fixes OpenCV's libGL.so.1 error)
RUN apt-get update && apt-get install -y \
    python3-pip \
    tzdata \
    iputils-ping \
    wget \
    curl \
    nano \
    libgl1 \
    libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

# Ensure OpenCV is installed correctly
RUN pip install --upgrade pip && \
    pip uninstall -y opencv-python opencv-python-headless opencv-contrib-python && \
    rm -rf /usr/local/lib/python3.10/dist-packages/cv2* && \
    pip install --no-cache-dir opencv-python-headless==4.7.0.72

# Install YOLO-NAS dependencies
RUN pip install --upgrade super_gradients torch torchvision torchaudio jupyter notebook ujson pycocotools

# 🔹 Fix 1: Patch SuperGradients - Fix broken model URLs
RUN sed -i 's|sghub.deci.ai|sg-hub-nv.s3.amazonaws.com|g' /usr/local/lib/python3.10/dist-packages/super_gradients/training/pretrained_models.py

# 🔹 Fix 2: Fix filename parsing in checkpoint_utils.py
RUN sed -i 's|url.split("https://sghub.deci.ai/models/")|url.split("https://sg-hub-nv.s3.amazonaws.com/models/")|g' /usr/local/lib/python3.10/dist-packages/super_gradients/training/utils/checkpoint_utils.py

# 🔹 Fix 3: Force CUDA-enabled PyTorch installation (ensures GPU compatibility)
RUN pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# 🔹 Fix 4: Ensure Jupyter Notebook runs without token authentication
RUN mkdir -p /root/.jupyter && echo 'c.NotebookApp.token = ""' >> /root/.jupyter/jupyter_notebook_config.py

# 🔹 Fix 5: Set default shell to bash and enable interactive mode
SHELL ["/bin/bash", "-c"]

# Expose Jupyter Notebook port
EXPOSE 8888

# Set entrypoint to start Jupyter Notebook by default
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]

