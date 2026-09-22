# Multi-language base devcontainer
# Covers: Python, C++, Java, Go, Ruby, Node (JS/TS/HTML/CSS tooling)
FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

ARG DEBIAN_FRONTEND=noninteractive

# --- Core build tools + C++ ---
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

# --- Python ---
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-venv \
    && rm -rf /var/lib/apt/lists/*
RUN pip3 install --break-system-packages --upgrade pip

# --- Java ---
RUN apt-get update && apt-get install -y \
    openjdk-21-jdk \
    maven \
    gradle \
    && rm -rf /var/lib/apt/lists/*

# --- Go ---
ARG GO_VERSION=1.23.4
RUN curl -fsSL https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz -o /tmp/go.tar.gz \
    && tar -C /usr/local -xzf /tmp/go.tar.gz \
    && rm /tmp/go.tar.gz
ENV PATH="/usr/local/go/bin:${PATH}"

# --- Ruby ---
RUN apt-get update && apt-get install -y \
    ruby-full \
    && rm -rf /var/lib/apt/lists/*
RUN gem install bundler

# --- Node (covers JS/TS/HTML/CSS tooling: npm, live-server, prettier, etc.) ---
ARG NODE_VERSION=20
RUN curl -fsSL https://deb.nodesource.com/setup_${NODE_VERSION}.x | bash - \
    && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists/*
RUN npm install -g npm@latest

# Non-root user (the base image ships a "vscode" user already)
USER vscode
WORKDIR /workspace

CMD ["sleep", "infinity"]
