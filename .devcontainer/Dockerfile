# Ubuntu 24.04 dev image for aQuantinum.
# Multi-arch: builds as amd64 on WSL and arm64 on Apple Silicon. Never hardcode an arch.
FROM mcr.microsoft.com/devcontainers/cpp:ubuntu-24.04

# Keep this list in sync with the README / scripts/setup.sh (the Pi installs the same).
RUN apt-get update \
 && export DEBIAN_FRONTEND=noninteractive \
 && apt-get install -y --no-install-recommends \
      build-essential \
      cmake \
      ninja-build \
      pkg-config \
      git \
      gdb \
      clangd \
      libfftw3-dev \
      python3-dev \
      python3-venv \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*