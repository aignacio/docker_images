# GitHub Actions for Docker Builds

This directory contains a GitHub Actions workflow to automatically build and push all Docker images to Docker Hub.

## Workflow

### `docker-build.yml`

**🚀 Automatic Dockerfile Detection & Parallel Builds**

The workflow automatically:
- **🔍 Discovers all Dockerfile.* files** in the repository
- **⚡ Builds all images in parallel** for maximum efficiency
- **🏗️ Supports both AMD64 and ARM64** architectures
- **🔄 Continues building** even if some images fail

**Key Features:**
- **Zero configuration** - Just add a `Dockerfile.*` and it's automatically built
- **Parallel execution** - All images build simultaneously
- **Fault tolerance** - One failed build doesn't stop others
- **Smart descriptions** - Automatic description generation based on image name
- **Build summary** - Comprehensive build report

## How It Works

### 1. **Discovery Phase**
The workflow first scans the repository for all `Dockerfile.*` files:
```bash
find . -name "Dockerfile.*" -type f
```

### 2. **Matrix Generation**
Creates a dynamic build matrix with:
- Dockerfile name
- Image name (sanitized)
- Description (auto-generated)

### 3. **Parallel Builds**
Each Dockerfile gets its own parallel build job with:
- Multi-architecture support (AMD64 + ARM64)
- Docker Hub authentication
- Caching for faster builds
- Proper metadata and labels

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

### 4. Add New Dockerfiles

**No configuration needed!** Just add a new `Dockerfile.*` to your repository:

```bash
# Add a new Dockerfile
echo "FROM ubuntu:latest" > Dockerfile.myapp
echo "RUN echo 'Hello World'" >> Dockerfile.myapp

# Push to trigger automatic build
git add Dockerfile.myapp
git commit -m "Add myapp Dockerfile"
git push
```

The workflow will automatically:
- Detect the new `Dockerfile.myapp`
- Create image name `myapp`
- Generate description "myapp Development Environment"
- Build for both AMD64 and ARM64
- Push to Docker Hub

## Trigger Builds

The workflow automatically triggers on:
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

- **🔍 Automatic discovery**: No manual configuration needed
- **⚡ Parallel builds**: All images build simultaneously
- **🔄 Fault tolerance**: Failed builds don't stop others
- **💾 Caching**: GitHub Actions cache for faster builds
- **🐳 QEMU emulation**: Enables ARM64 builds on AMD64 runners
- **🔧 BuildKit**: Advanced Docker build features
- **📊 Build summary**: Comprehensive build report

## Example Usage

After setup, your images will be available as:
```bash
# Pull the latest rtldev image
docker pull aignacio/rtldev:latest

# Pull a specific version
docker pull aignacio/rtldev:v1.0.0

# Pull for specific architecture
docker pull --platform linux/arm64 aignacio/rtldev:latest

# Pull any image (automatically discovered)
docker pull aignacio/myapp:latest  # If you added Dockerfile.myapp
```

## Adding New Images

### Method 1: Just Add Dockerfile
```bash
# Create a new Dockerfile
cat > Dockerfile.myservice << EOF
FROM ubuntu:latest
RUN apt-get update && apt-get install -y mypackage
CMD ["myservice"]
EOF

# Commit and push
git add Dockerfile.myservice
git commit -m "Add myservice Docker image"
git push
```

### Method 2: Custom Description (Optional)
If you want a custom description, you can modify the workflow's case statement in the "Create matrix" step.

## Build Matrix

The workflow uses dynamic matrix generation:
- **Automatic discovery** of all Dockerfile.* files
- **Parallel execution** of all builds
- **Independent failures** - one failure doesn't affect others
- **Comprehensive reporting** with build summary

## Troubleshooting

### Common Issues

1. **Build fails for one image**: Check the specific build logs, other images will continue
2. **Authentication errors**: Verify Docker Hub secrets are set correctly
3. **Architecture issues**: Ensure Dockerfile supports multi-arch builds
4. **Cache issues**: Builds will work without cache, just slower

### Debug Mode

To debug the discovery process, check the "Find Dockerfiles" step output in the workflow logs. 