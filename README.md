[![Build and Push Docker Images](https://github.com/aignacio/docker_images/actions/workflows/docker-build.yml/badge.svg)](https://github.com/aignacio/docker_images/actions/workflows/docker-build.yml)

# Docker Images

Docker images for hardware design, RTL development, and embedded systems. All images support AMD64 and ARM64 architectures.

## Available Images

### rtldev
```bash
docker pull aignacio/rtldev:latest
```
Complete RTL development environment including:
- Verilator v5.026
- Slang (SystemVerilog compiler)
- SV2V (SystemVerilog to Verilog converter)
- Verible (SystemVerilog linter)
- Icarus Verilog
- Nox

### chisel
```bash
docker pull aignacio/chisel:latest
```
Chisel hardware design environment:
- Chisel (Scala-based HDL)
- Scala
- SBT

### yosys
```bash
docker pull aignacio/yosys:latest
```
Open-source synthesis suite:
- Yosys (RTL synthesis framework)
- ABC (synthesis and verification)
- SMT-Solver

### synlig
```bash
docker pull aignacio/synlig:latest
```
SystemVerilog synthesis toolchain:
- Synlig
- Yosys-based synthesis flow

### mpsocsw
```bash
docker pull aignacio/mpsocsw:latest
```
Zynq UltraScale+ MPSoC development:
- Xilinx tools for MPSoC
- ARM64 cross-compilation toolchain
- Embedded Linux development tools

### nox
```bash
docker pull aignacio/nox:latest
```
Python task automation:
- Nox
- Python 3
- Testing and development tools

### axidma
```bash
docker pull aignacio/axidma:latest
```
AXI DMA development environment:
- Xilinx AXI DMA IP
- HLS tools
- Vivado

### icarus
```bash
docker pull aignacio/icarus:latest
```
Verilog simulation:
- Icarus Verilog
- GTKWave
- Basic Verilog toolchain

### gh_runner
```bash
docker pull aignacio/gh_runner:latest
```
Self-hosted GitHub Actions runner:
- GitHub Actions runner
- CI/CD tools

## Architecture Support

All images support:
- Linux AMD64
- Linux ARM64

## Quick Start

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

## Image Tags

- `latest` - Most recent stable version
- `v1.0.0` - Specific version tags
- `v1.0` - Major.minor version
- `main-abc123` - Branch-specific builds

## Automated Builds

GitHub Actions automatically builds and pushes images to Docker Hub on every push to main. Parallel builds run for all images with multi-architecture support.

### Required Secrets

To enable automated builds:

1. `DOCKERHUB_USERNAME` - Your Docker Hub username
2. `DOCKERHUB_TOKEN` - Docker Hub access token

Create a token at [Docker Hub Account Settings](https://hub.docker.com/settings/security)

## Development

### Prerequisites
- Docker with BuildKit enabled

### Building Locally
```bash
git clone https://github.com/aignacio/docker_images.git
cd docker_images

# Build all images
for dockerfile in Dockerfile.*; do
  name=$(basename $dockerfile Dockerfile.)
  docker build -f $dockerfile -t aignacio/$name:local .
done
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add your Dockerfile
4. Update `.github/workflows/docker-build.yml`
5. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) for details.

## Contact

- Issues: [GitHub Issues](https://github.com/aignacio/docker_images/issues)
- Email: anderson@aignacio.com
