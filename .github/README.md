# GitHub Actions for Docker Builds

This directory contains a GitHub Actions workflow to automatically build and push all Docker images to Docker Hub.

## Workflow

### `docker-build.yml`
Builds and pushes all Docker images individually for both AMD64 and ARM64 architectures.

**Supported Images:**
- `rtldev` - RTL Development Environment with Verilator, Slang, SV2V, and Verible
- `chisel` - Chisel Hardware Design Language Environment
- `yosys` - Yosys Open SYnthesis Suite
- `synlig` - Synlig Synthesis Tool Environment
- `mpsocsw` - MPSoC Software Development Environment
- `nox` - Nox Development Environment
- `axidma` - AXI DMA Development Environment
- `icarus` - Icarus Verilog Environment
- `gh_runner` - GitHub Runner Environment

## Setup Instructions

### 1. Create Docker Hub Access Token

1. Go to [Docker Hub](https://hub.docker.com/)
2. Log in to your account
3. Go to **Account Settings** → **Security** → **New Access Token**
4. Create a token with **Read & Write** permissions
5. Copy the token (you'll need it for the next step)

### 2. Add GitHub Secrets

In your GitHub repository, go to **Settings** → **Secrets and variables** → **Actions** and add:

- `DOCKERHUB_USERNAME`: Your Docker Hub username (e.g., `aignacio`)
- `DOCKERHUB_TOKEN`: The access token you created in step 1

### 3. Configure Image Names

Edit the workflow file to match your Docker Hub username:

```yaml
env:
  REGISTRY: docker.io
  DOCKERHUB_USERNAME: your-dockerhub-username  # Change this
```

### 4. Trigger Builds

The workflow will automatically trigger on:
- **Push to main/master branch**: Builds and pushes all images with branch name tag
- **Push with version tag** (e.g., `v1.0.0`): Builds and pushes all images with version tags
- **Pull requests**: Builds all images but doesn't push (for testing)
- **Manual trigger**: Use the "workflow_dispatch" option in GitHub Actions

## Image Tags

The workflow automatically generates tags for each image:
- `latest` (for main branch)
- `v1.0.0` (for version tags)
- `v1.0` (major.minor for version tags)
- `main-abc123` (branch-commit for other pushes)

## Multi-Architecture Support

The workflow builds for both architectures:
- `linux/amd64` (Intel/AMD 64-bit)
- `linux/arm64` (ARM 64-bit, Apple Silicon, etc.)

## Build Features

- **Parallel builds**: All images are built simultaneously
- **Caching**: GitHub Actions cache for faster builds
- **QEMU emulation**: Enables ARM64 builds on AMD64 runners
- **BuildKit**: Advanced Docker build features
- **Provenance disabled**: Faster builds without SBOM generation

## Example Usage

After setup, your images will be available as:
```bash
# Pull the latest rtldev image
docker pull aignacio/rtldev:latest

# Pull a specific version
docker pull aignacio/rtldev:v1.0.0

# Pull for specific architecture
docker pull --platform linux/arm64 aignacio/rtldev:latest

# Pull other images
docker pull aignacio/chisel:latest
docker pull aignacio/yosys:latest
docker pull aignacio/synlig:latest
# ... and so on for all images
```

## Build Matrix

The workflow uses GitHub Actions matrix strategy to build all images in parallel:
- Each Dockerfile gets its own build job
- All jobs run simultaneously for maximum efficiency
- If one image fails, others continue building
- Each image gets proper metadata and labels 