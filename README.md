<<<<<<< HEAD
This is a simple repo for a container template to use for development environments.
=======
# Dev Container Template

A base [Dev Container](https://containers.dev/) setup for spinning up a consistent, reproducible development environment in Docker via Cursor (or VS Code). Covers Python, C++, Java, Go, Ruby, and Node (which handles JS/TS/HTML/CSS tooling).

## What's included

- **Base image:** Ubuntu 24.04 (`mcr.microsoft.com/devcontainers/base:ubuntu-24.04`)
- **Languages/runtimes:** Python 3 + pip, C++ (build-essential, gdb, cmake, clang), Java 21 (Maven + Gradle), Go, Ruby (+ Bundler), Node.js 20 (+ npm)
- **Editor extensions:** auto-installed per language, plus ESLint, Prettier, and Live Server for web work
- **SSH passthrough:** your WSL/host `~/.ssh` folder is mounted read-only into the container, so `git push`/`git pull` over SSH work immediately with no per-project key setup
- **Forwarded ports:** 3000, 5000, 8000, 8080 (common dev server defaults — edit per project as needed)

This image intentionally does **not** include frameworks or libraries (React, Django, Spring, etc.) — those are installed per-project via each language's own package manager, keeping the base image generic and each project's dependencies version-locked to its own manifest file.

## Using this template in a new project

1. Copy the `.devcontainer/` folder into your new project's root:
   ```bash
   cp -r .devcontainer /path/to/your-project/
   ```
2. Add your project's manifest file at the project root (`package.json`, `requirements.txt`, `go.mod`, `Gemfile`, `pom.xml`, etc.) — either write it yourself or let a scaffold tool generate it once you're inside the container.
3. Update `postCreateCommand` in that project's `devcontainer.json` to install from the manifest, e.g.:
   - Node: `"npm install"`
   - Python: `"pip install -r requirements.txt"`
   - Go: `"go mod download"`
   - Ruby: `"bundle install"`
   - Java: `"mvn install"` or `"gradle build"`
4. Adjust `forwardPorts` if the project needs a port not already listed.
5. Open the project in Cursor and run **"Dev Containers: Reopen in Container"** (`Ctrl+Shift+P`).

## Updating the template

Changes made here won't retroactively affect projects that already copied it — each project's `.devcontainer` is a snapshot. Update this repo when you want the *next* new project to start from an improved baseline (e.g. bumping a language version or adding a tool).

## Requirements

- Docker Desktop, running with WSL2 integration enabled
- Cursor (or VS Code) with the **Dev Containers** extension
- An SSH key set up on your WSL host and added to GitHub, for the SSH passthrough to work
>>>>>>> 376352b (Update README with template usage instructions)
