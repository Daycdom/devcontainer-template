# Dev Container Template

A base [Dev Container](https://containers.dev/) setup for spinning up a consistent, reproducible development environment in Docker via Cursor (or VS Code). Covers Python, C++, Java, Go, Ruby, and Node (which handles JS/TS/HTML/CSS tooling).

See [CHANGELOG.md](./CHANGELOG.md) for a timestamped history of updates to this template — useful for correlating a version bump with a build breaking afterward.

## What's included

- **Base image:** Microsoft's prebuilt `mcr.microsoft.com/devcontainers/universal:2` image, which already bundles Python, C++, Java, Go, Ruby, Node, and their common package managers (pip, Maven/Gradle, npm, Bundler)
- **`.devcontainer/post-create.sh`:** a script that runs automatically once the container is created — see "What the setup script does" below
- **Editor extensions:** auto-installed per language, plus ESLint, Prettier, and Live Server for web work
- **SSH passthrough:** your host's `~/.ssh` folder is mounted read-only into the container, so the *same* SSH key you already use on your machine works immediately inside every container — no separate key per project
- **Forwarded ports:** 3000, 5000, 8000, 8080 (common dev server defaults — edit per project as needed)

This image intentionally does **not** include frameworks or libraries (React, Django, Spring, etc.) — those are installed per-project via each language's own package manager, keeping the base image generic and each project's dependencies version-locked to its own manifest file.

## What the setup script does

`post-create.sh` runs automatically the moment a container finishes building. It:

1. Fixes ownership/permissions on the mounted SSH keys (bind mounts often bring over permissions SSH won't accept)
2. Pre-trusts GitHub's host key via `ssh-keyscan`, so the first `git push`/`pull` doesn't pause with a "continue connecting?" prompt
3. Lists which SSH key(s) it found, so a failed mount is obvious immediately rather than surfacing as a confusing error later
4. Runs a live `ssh -T git@github.com` test and prints the result
5. Prints the installed version of every language and package manager, as a sanity check that the environment built correctly

## Using this template in a new project

1. Copy the whole `.devcontainer/` folder (both `devcontainer.json` and `post-create.sh`) into your new project's root:
   ```bash
   mkdir -p ~/source/<your-project-name>/.devcontainer
   cp -r ~/source/devcontainer-template/.devcontainer/. ~/source/<your-project-name>/.devcontainer/
   ```
   Replace `<your-project-name>` with your project's actual folder name.
2. Add your project's manifest file at the project root (`package.json`, `requirements.txt`, `go.mod`, `Gemfile`, `pom.xml`, etc.) — either write it yourself or let a scaffold tool generate it once you're inside the container.
3. Update `postCreateCommand` in that project's `devcontainer.json` if the project needs an extra install step beyond what `post-create.sh` already does, e.g. appending `&& npm install` or `&& pip install -r requirements.txt`.
4. Adjust `forwardPorts` if the project needs a port not already listed.
5. Open the project in Cursor and run **"Dev Containers: Reopen in Container"** (`Ctrl+Shift+P`).
6. Check the container-creation log (or the integrated terminal) to confirm `post-create.sh` ran successfully — SSH auth should report success and every language version should print.

## Updating the template

For manual changes (adding a tool, changing an extension), edit the files directly and log the change with a timestamp in `CHANGELOG.md`.

Changes made here won't retroactively affect projects that already copied the template — each project's `.devcontainer` is a snapshot at the time it was copied. Consider tagging releases (`git tag v1.1.0`) once the template is stable, so you know exactly which version a given project started from.

## Requirements

- Docker Desktop, running with WSL2 integration enabled
- Cursor (or VS Code) with the **Dev Containers** extension
- An SSH key set up on your host machine and added to GitHub — generated once, reused automatically by every container via the SSH passthrough mount
