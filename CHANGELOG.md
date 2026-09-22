# Changelog

All notable changes to this devcontainer template are logged here, with timestamps,
so you can correlate a template update with any build issues that show up afterward.

## 2026-09-21 21:15 EDT
- Converted language installs (Python, Node, Go, Java, Ruby) from manual apt-get/curl
  steps in the Dockerfile to official Dev Container Features in `devcontainer.json`.
  Versions are now pinned per-feature in one place and easy to bump.
- Added `.github/dependabot.yml` so GitHub opens a PR automatically when a newer base
  image or feature version becomes available (weekly check).
- Dockerfile now only handles C++ tooling and general build essentials, since no
  dedicated Feature covers those well.

## 2026-09-21 20:55 EDT
- Added SSH passthrough mount (`~/.ssh` -> `/home/vscode/.ssh`, read-only) so
  `git push`/`git pull` over SSH work inside the container without per-project
  key setup.

## 2026-09-21 20:54 EDT
- Initial template created: Ubuntu 24.04 base image with Python, C++, Java, Go,
  Ruby, and Node installed directly in the Dockerfile; devcontainer.json with
  editor extensions and forwarded ports.
