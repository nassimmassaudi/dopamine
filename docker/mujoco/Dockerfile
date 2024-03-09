# Specify the base image
ARG base_image=dopamine/core
FROM ${base_image}

# Install system dependencies
RUN apt-get update && apt-get install -y \
    curl \
    libosmesa6-dev \
    libgl1-mesa-glx \
    libglfw3 \
    libglew-dev \
    patchelf \
    gcc \
    python3.8-dev \
    unzip \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /root

# Create .mujoco directory and copy the MuJoCo license key
RUN mkdir .mujoco
COPY mjkey.txt .mujoco/mjkey.txt

# Download and install MuJoCo
RUN curl -O https://www.roboti.us/download/mujoco200_linux.zip && \
    unzip mujoco200_linux.zip && \
    rm mujoco200_linux.zip && \
    mv mujoco200_linux .mujoco/mujoco200

# Add LD_LIBRARY_PATH environment variable
ENV LD_LIBRARY_PATH /root/.mujoco/mujoco200/bin:${LD_LIBRARY_PATH}

# Install mujoco_py
RUN pip install mujoco_py

# Reset working directory
WORKDIR /
