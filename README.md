# 🐳 Docker Images Collection

> **A curated collection of specialized Docker images for hardware design, RTL development, and embedded systems**

```
                    ##         .
              ## ## ##        ==
           ## ## ## ## ##    ===
       /""""""""""""""""\___/ ===
  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
       \______ o           __/
         \    \         __/
          \____\_______/
```

## 🚀 Available Images

### 🔧 **RTL Development Environment**
```bash
docker pull aignacio/rtldev:latest
```
**`rtldev`** - Your complete RTL development toolkit with:
- **Verilator** v5.026 - Fast Verilog simulator
- **Slang** - Modern SystemVerilog compiler
- **SV2V** - SystemVerilog to Verilog converter
- **Verible** - SystemVerilog tools and linter
- **Icarus Verilog** - Open-source Verilog simulator
- **Nox** - Python task automation

### ⚡ **Chisel Hardware Design**
```bash
docker pull aignacio/chisel:latest
```
**`chisel`** - Hardware design with Chisel:
- **Chisel** - Constructing Hardware in a Scala Embedded Language
- **Scala** - Programming language for hardware design
- **SBT** - Build tool for Scala projects

### 🔍 **Yosys Synthesis Suite**
```bash
docker pull aignacio/yosys:latest
```
**`yosys`** - Open source synthesis suite:
- **Yosys** - Framework for Verilog RTL synthesis
- **ABC** - Sequential synthesis and verification
- **SMT-Solver** - Satisfiability modulo theories

### 🎯 **Synlig Synthesis Tool**
```bash
docker pull aignacio/synlig:latest
```
**`synlig`** - Advanced synthesis environment:
- **Synlig** - Modern synthesis toolchain
- **Optimization tools** - For RTL synthesis
- **Design analysis** - Comprehensive verification

### 🧠 **MPSoC Software Development**
```bash
docker pull aignacio/mpsocsw:latest
```
**`mpsocsw`** - Multi-Processor System-on-Chip development:
- **Xilinx tools** - For Zynq UltraScale+ MPSoC
- **Cross-compilation** - ARM64 toolchain
- **Embedded Linux** - Development environment

### 🐍 **Nox Development Environment**
```bash
docker pull aignacio/nox:latest
```
**`nox`** - Python task automation:
- **Nox** - Flexible test automation
- **Python 3** - Latest Python environment
- **Development tools** - For Python projects

### 🔌 **AXI DMA Development**
```bash
docker pull aignacio/axidma:latest
```
**`axidma`** - AXI Direct Memory Access development:
- **AXI DMA IP** - Xilinx DMA controller
- **HLS tools** - High-Level Synthesis
- **Vivado tools** - For FPGA development

### 🎮 **Icarus Verilog**
```bash
docker pull aignacio/icarus:latest
```
**`icarus`** - Lightweight Verilog simulation:
- **Icarus Verilog** - Open-source Verilog simulator
- **GTKWave** - Waveform viewer
- **Verilog tools** - Complete toolchain

### 🤖 **GitHub Runner Environment**
```bash
docker pull aignacio/gh_runner:latest
```
**`gh_runner`** - Self-hosted GitHub Actions runner:
- **GitHub Actions runner** - Self-hosted CI/CD
- **Development tools** - For automated workflows
- **Containerized CI** - Isolated build environment

## 🏗️ **Architecture Support**

All images are built for multiple architectures:
- **🐧 Linux AMD64** - Intel/AMD 64-bit processors
- **🍎 Linux ARM64** - Apple Silicon, ARM servers, Raspberry Pi

## 🚀 **Quick Start**

### Pull and Run
```bash
# Pull the latest RTL development environment
docker pull aignacio/rtldev:latest

# Run with interactive shell
docker run -it --rm aignacio/rtldev:latest

# Mount your project directory
docker run -it --rm -v $(pwd):/workspace aignacio/rtldev:latest
```

### Build Locally
```bash
# Build a specific image
docker build -f Dockerfile.rtldev -t my-rtldev .

# Build for specific architecture
docker build --platform linux/arm64 -f Dockerfile.rtldev -t my-rtldev-arm64 .
```

## 🏷️ **Image Tags**

- **`latest`** - Most recent stable version
- **`v1.0.0`** - Specific version tags
- **`v1.0`** - Major.minor version
- **`main-abc123`** - Branch-specific builds

## 🔄 **Automated Builds**

This repository uses GitHub Actions to automatically build and push all images to Docker Hub:

- **🔄 Automatic builds** on every push to main branch
- **🏷️ Version tagging** for releases
- **⚡ Parallel builds** for all images
- **🔄 Multi-arch support** (AMD64 + ARM64)

## 🛠️ **Development**

### Prerequisites
- Docker with BuildKit enabled
- GitHub Actions (for automated builds)

### Local Development
```bash
# Clone the repository
git clone https://github.com/your-username/docker_images.git
cd docker_images

# Build all images locally
for dockerfile in Dockerfile.*; do
  name=$(basename $dockerfile Dockerfile.)
  docker build -f $dockerfile -t aignacio/$name:local .
done
```

## 📝 **Contributing**

1. Fork the repository
2. Create a feature branch
3. Add your Dockerfile with proper labels
4. Update the matrix in `.github/workflows/docker-build.yml`
5. Submit a pull request

## 📄 **License**

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 **Support**

- **🐛 Issues**: [GitHub Issues](https://github.com/your-username/docker_images/issues)
- **💬 Discussions**: [GitHub Discussions](https://github.com/your-username/docker_images/discussions)
- **📧 Email**: anderson@aignacio.com

---
