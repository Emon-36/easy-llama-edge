# 🚀 Easy Llama Edge: LLM Deployment for 1GB RAM Devices

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform: Linux/ARM](https://img.shields.io/badge/Platform-Linux%2FARM-blue)](https://armbian.com)
[![Main Engine: llama.cpp](https://img.shields.io/badge/Main%20Engine-llama.cpp-green)](https://github.com/ggerganov/llama.cpp)

An optimized environment and automated pipeline to run Large Language Models (LLMs) on ultra-low-end hardware, specifically **$25 Android TV Boxes** (Allwinner H313/H616) with only **1GB RAM**.

---

## 🎖 Credits & Attributions
- **Original Engine:** This project is built upon the revolutionary [llama.cpp](https://github.com/ggerganov/llama.cpp) developed by **Georgi Gerganov**. 
- **Edge Optimization:** Environment tuning, Clang-based compilation, Swap management, and automation scripts developed by **Md. Shahariar Khan Emon**.

---

## 🛠 Features & The "1GB RAM" Optimization
Running modern LLMs on 1GB RAM is a challenge. This repository solves it through:
- **Clang Compiler:** Using `clang` instead of `gcc` for better ARMv8 binary efficiency.
- **Virtual Memory:** Automated 4GB Swap configuration to prevent OOM (Out of Memory) crashes.
- **Quantization:** Support for GGUF (INT4/INT8) to reduce model footprint.
- **Custom Shell Scripts:** Ready-to-use runners for **Llama 3.2 (1B)** and **Qwen 2.5 (0.5B)**.

---

## 🏗 System Architecture



The pipeline ensures that the CPU can handle the weights even when the physical RAM is exhausted by utilizing optimized swap space.

---

## ⚙️ Automated Setup (One-Click)

I have created a comprehensive bash script to handle everything from installation to compilation.

### 1. Run the Setup Script
Simply run this command to prepare your system:
```bash
chmod +x run_llama3.2.sh
chmod +x run_qwen2.5.sh
./run_llama3.2.sh
./run_qwen2.5.sh



##2. Manual Setup Instructions
If you prefer to run things manually:

###A. Install Toolchains
```bash
sudo apt update && sudo apt install -y build-essential clang git cmake

###B.Configure Swapfile(Mandatory)
```bash
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

###Build With Clang
```bash
mkdir build && cd build
cmake .. -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++
cmake --build . --config Release -j$(nproc)
cd ..


##Model Execution

Place your .gguf model files in the model/ directory, then use the following scripts:

For Qwen 2.5 (0.5B): ./run_qwen2.5.sh (High speed)

For Llama 3.2 (1B): ./run_llama3.2.sh (High accuracy)



##Performance Matrix
Device,RAM,Model,Quant,Tokens/Sec
TV Box (H313),1GB,Qwen 2.5 0.5B,Q4_K_M,4.2 - 5.5
TV Box (H313),1GB,Llama 3.2 1B,Q4_K_M,1.8 - 2.5


##Contact and Colab
Feel free to reach out for collaborations in Edge AI, Embedded Systems, or Power Electronics.

Lead Engineer: Md. Shahariar Khan Emon
Email: emon23702036@gmail.com
