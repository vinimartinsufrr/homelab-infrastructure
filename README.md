# 🖥️ homelab-infrastructure

Personal homelab running on a dedicated Ubuntu Server machine, hosting a full stack of self-managed services organized into Docker Compose stacks. Built and maintained as a hands-on environment for Linux administration, networking, and infrastructure monitoring.

---

## 🔧 Hardware

| Component | Spec |
|---|---|
| **CPU** | AMD Ryzen 5 5600G |
| **RAM** | 8GB DDR4 |
| **Boot** | 256GB SSD |
| **Storage** | 2x 1TB HDD |
| **OS** | Ubuntu Server 24.04 LTS |

---

## 🐳 Docker Stacks

### 🎬 Media (`stacks/media/`)

Self-hosted media server with automated content management.

| Container | Purpose |
|---|---|
| **Jellyfin** | Media server and player |
| **Sonarr** | TV series collection manager |
| **Radarr** | Movie collection manager |
| **Prowlarr** | Indexer aggregator for Sonarr/Radarr |
| **Bazarr** | Automatic subtitle downloader |
| **qBittorrent** | Download client |

### 📊 Monitoring (`stacks/monitoring/`)

Full observability stack for the homelab infrastructure.

| Container | Purpose |
|---|---|
| **Prometheus** | Metrics collection and storage (15-day retention) |
| **Grafana** | Dashboards for CPU, memory, disk, network and containers |
| **node-exporter** | System-level metrics exporter |
| **cAdvisor** | Per-container resource metrics |
| **Uptime Kuma** | Service uptime monitoring with status page |

### ☁️ Nextcloud (`stacks/nextcloud/`)

Private cloud storage with MariaDB backend.

| Container | Purpose |
|---|---|
| **Nextcloud** | File sync, sharing and collaboration |
| **MariaDB** | Database backend |

### 🌐 Pi-hole (`stacks/pihole/`)

| Container | Purpose |
|---|---|
| **Pi-hole** | Network-wide DNS resolver and ad/tracker blocker |

---

## ⚙️ System Services (systemd)

| Service | Description |
|---|---|
| **minecraft.service** | Java Edition Minecraft server managed via screen |
| **smbd / nmbd** | Samba file sharing for local network devices |
| **tailscaled** | WireGuard-based VPN mesh for secure remote access |
| **ssh** | Remote administration — key-only authentication |
| **ufw** | Firewall with restrictive inbound rules |
| **rsyslog** | System logging |
| **unattended-upgrades** | Automatic security updates |
| **lm-sensors** | Hardware temperature monitoring |

---

## 🌐 Networking

- **DNS:** Pi-hole as the local DNS resolver for all network devices
- **VPN:** Tailscale (WireGuard-based) mesh — full SSH access from any device, anywhere
- **Remote power:** Smart plugs with restore-on-power-loss for remote startup via Tailscale
- **File sharing:** Samba shares accessible to all local network devices

---

## 📁 Repository Structure

```
homelab-infrastructure/
├── README.md
├── .gitignore
├── stacks/
│   ├── media/
│   │   └── docker-compose.yml
│   ├── monitoring/
│   │   ├── docker-compose.yml
│   │   └── prometheus.yml
│   ├── nextcloud/
│   │   ├── docker-compose.yml
│   │   └── .env.example
│   └── pihole/
│       ├── docker-compose.yml
│       └── .env.example
└── systemd/
    └── minecraft.service
```

---

## 🔒 Security Notes

- SSH key-only authentication — password login disabled
- UFW firewall active with restrictive inbound rules
- Unattended security upgrades enabled
- Sensitive values (passwords, tokens) removed from all compose files — see `.env.example` in each stack
- Tailscale VPN for all remote access

---

*All services self-hosted. No third-party cloud dependencies for personal data.*
