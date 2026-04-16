# homelab

A devcontainer-based development environment for homelab work. Tools and shell configuration are managed declaratively using mise and provisioned automatically when the container starts.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) or [Podman](https://podman.io/getting-started/installation)
- [DevPod](https://devpod.sh/) or [VS Code](https://code.visualstudio.com/) with the [Remote Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension

## Getting Started

Clone the repository:

```bash
git clone https://github.com/nelsong/homelab.git
cd homelab
```

### Using DevPod

```bash
devpod up .
```

### Using VS Code

1. Open the repository in VS Code.
2. When prompted, select **Reopen in Container**. Alternatively, open the command palette and run **Dev Containers: Reopen in Container**.

The container will build, install all declared tools, and configure the shell automatically.

## What's Included

### Tools (via mise)

The following tools are declared in `mise.toml` and installed during container setup:

| Tool | Version |
|------|---------|
| Neovim | 0.12.1 |
| Node.js | 24 |
| fzf | latest |
| ripgrep | latest |
| eza | 0.23.4 |

### Additional Software

- [chezmoi](https://www.chezmoi.io/) for dotfile management
- [zap](https://github.com/zap-zsh/zap) as the zsh plugin manager
- zsh with autosuggestions and syntax highlighting plugins
- zsh is set as the default shell

## Configuration

| File | Purpose |
|------|---------|
| `mise.toml` | Declares tool versions managed by mise |
| `.devcontainer/devcontainer.json` | Devcontainer settings, mounts, and post-create hooks |
| `.devcontainer/Dockerfile` | Base image, system packages, mise binary, and shell activation |
| `.devcontainer/scripts/setup` | Post-create script that installs mise tools and configures zap |

## Host Home Mount

The host `$HOME` directory is bind-mounted into the container at `/workspace/home`. This allows access to host files (SSH keys, dotfiles, etc.) from within the container without copying them.

## Customization

To add or change tools, edit `mise.toml` and rebuild the container. For example, to add Go:

```toml
[tools]
go = "1.23"
```

Then rebuild the devcontainer to pick up the changes.
