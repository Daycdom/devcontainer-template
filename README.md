# Dev Container Template

A base [Dev Container](https://containers.dev/) setup for spinning up a consistent, reproducible development environment in Docker via Cursor (or VS Code). Covers Python, C++, Java, Go, Ruby, and Node (which handles JS/TS/HTML/CSS tooling).

See [CHANGELOG.md](./CHANGELOG.md) for a timestamped history of updates to this template — useful for correlating a version bump with a build breaking afterward.

## What's included

- **Base image:** Ubuntu 24.04 (`mcr.microsoft.com/devcontainers/base:ubuntu-24.04`)
- **Languages/runtimes:** installed via official, versioned [Dev Container Features](https://containers.dev/features) declared in `devcontainer.json` — Python, Node, Go, Java, Ruby. Each has a pinned version in one place, making updates a one-line change.
- **C++ tooling:** build-essential, gdb, cmake, clang — installed directly in the Dockerfile, since there's no dedicated Feature for these
- **Editor extensions:** auto-installed per language, plus ESLint, Prettier, and Live Server for web work
- **SSH passthrough:** your WSL/host `~/.ssh` folder is mounted read-only into the container, so `git push`/`git pull` over SSH work immediately with no per-project key setup
- **Forwarded ports:** 3000, 5000, 8000, 8080 (common dev server defaults — edit per project as needed)
- **Dependabot:** `.github/dependabot.yml` watches the base image and Features weekly and opens a PR automatically when newer versions are available

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

Dependabot will open PRs automatically when a newer base image or language version is available — review and merge those as they come in. For manual changes (adding a tool, changing an extension), edit the files directly and log the change with a timestamp in `CHANGELOG.md`.

Changes made here won't retroactively affect projects that already copied the template — each project's `.devcontainer` is a snapshot at the time it was copied. Consider tagging releases (`git tag v1.1.0`) once the template is stable, so you know exactly which version a given project started from.

## Requirements

- Docker Desktop, running with WSL2 integration enabled
- Cursor (or VS Code) with the **Dev Containers** extension
- An SSH key set up on your WSL host and added to GitHub, for the SSH passthrough to work
