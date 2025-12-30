# 🖥️ Desktop Workstation OS

[![build-image](https://github.com/danielvollbro/workstation-desktop/actions/workflows/build.yml/badge.svg)](https://github.com/danielvollbro/workstation-desktop/actions/workflows/build.yml)
[![BlueBuild](https://img.shields.io/badge/Built%20with-BlueBuild-blue?logo=github)](https://blue-build.org/)
[![Fedora](https://img.shields.io/badge/Based%20on-Aurora%20(Fedora)-blue)](https://getaurora.dev/)

> **`workstation-desktop`** — An immutable OS for physical endpoints and thin clients.

## 📖 About
This repository defines the operating system image for my **physical hardware** (Laptops, Mini-PCs). While these machines are capable of standalone work, their primary role in this architecture is to act as **Thin Clients** connecting to the centralized `workstation-headless` compute node.

**Key Characteristics:**
* **Hardware Support:** Optimized for physical GPUs (Intel/AMD/Nvidia), Wi-Fi, and power management.
* **Hybrid Workflow:** Can run local workloads when needed, but defaults to offloading heavy tasks to the cloud host.
* **Client Focus:** Pre-configured for low-latency streaming and remote access.

## 🏗 The Workstation Ecosystem

| Repository | Role | Description |
| :--- | :--- | :--- |
| `workstation-headless` | Compute Host | The powerful backend VM doing the heavy lifting. |
| **`workstation-desktop`** | **Thin Client** | **This repo.** Lightweight OS for physical endpoints connecting to the host. |
| `workstation-dotfiles` | Config | Unified configuration (Chezmoi) for both environments. |

## ⚙️ Tech Stack & Features

* **Base OS:** [Aurora DX](https://getaurora.dev/) (Fedora Silverblue/Atomic).
* **Streaming Client:** [Moonlight](https://moonlight-stream.org/) (Pre-installed and optimized for hardware decoding).
* **Local Tools:** Browsers, Communication apps, and basic dev tools for "offline" work.
* **VPN:** WireGuard/Tailscale pre-baked for secure connectivity to the host.

## 🚀 Usage
This OS is designed to be "flash and forget".

1.  **Install:** Flash the ISO to a USB stick and install on physical hardware.
2.  **Rebase:** Connect to the OCI registry to receive updates.
    ```bash
    rpm-ostree rebase ostree-unverified-registry:ghcr.io/danielvollbro/workstation-desktop:latest
    ```
3.  **Config:** Apply the unified dotfiles.
    ```bash
    chezmoi init --apply danielvollbro/workstation-dotfiles
    ```
4.  **Connect:** Launch Moonlight and connect to `workstation-headless`.

## 📂 Repository Structure

```text
├── recipe.yml           # Defines packages (Drivers, Moonlight, VPN).
├── files/               # Hardware specific configs (e.g. power saving).
├── .github/workflows/   # CI/CD pipelines.
└── README.md
```

---

<div align="center">
<sub>Built with ❤️ and YAML by Daniel Vollbro.</sub>
</div>
