# Multi-language base devcontainer
# Language runtimes (Python, Node, Go, Java, Ruby) are installed via Dev Container
# Features in devcontainer.json instead of here — see that file for pinned versions.
# This Dockerfile only handles C++ tooling and general build tools, since no
# dedicated Feature covers those well.
FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    build-essential \
    gdb \
    cmake \
    clang \
    clang-format \
    clang-tidy \
    git \
    curl \
    wget \
    unzip \
    zip \
    ca-certificates \
    software-properties-common \
    && rm -rf /var/lib/apt/lists/*

USER vscode
WORKDIR /workspace

CMD ["sleep", "infinity"]
