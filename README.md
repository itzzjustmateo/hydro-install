<p align="center">
  <img width="1467" height="401" alt="Hydrodactyl Installer" src="https://github.com/user-attachments/assets/7d5138a4-acd0-43e5-932b-419c5125c0d7" />
</p>

<p align="center">
  <a href="https://github.com/itzzjustmateo/hydro-install/blob/main/LICENSE"><img src="https://img.shields.io/github/license/itzzjustmateo/hydro-install?style=for-the-badge&color=orange" alt="License"></a>
  <a href="https://github.com/itzzjustmateo/hydro-install/actions"><img src="https://img.shields.io/github/actions/workflow/status/itzzjustmateo/hydro-install/ci.yml?style=for-the-badge&color=orange" alt="CI"></a>
  <img src="https://img.shields.io/badge/shell-bash-4EAA25?style=for-the-badge&logo=gnu-bash&color=orange" alt="Shell">
</p>

A beautiful, modern, and feature-rich installer for the **Hydrodactyl** game server management panel and **Elytra** daemon. Built with an elegant flame-inspired UI and designed for ease of use.

This installer is a fork of the [Pyrodactyl Installer](https://github.com/Muspelheim-Hosting/pyrodactyl-installer), adapted for use with the [Hydrodactyl Panel](https://github.com/BlueprintFramework/hydrodactyl).

## Features

- **Beautiful Flame UI** — Orange gradient interface inspired by Muspelheim Hosting
- **Flexible Installation** — Install panel, Elytra, or both on the same machine
- **Private Repository Support** — Full support for private GitHub repositories with token validation
- **Auto-Updaters** — Optional automatic updates for both panel and Elytra
- **SSL/TLS Ready** — Let's Encrypt integration with automatic renewal and service restart hooks
- **Firewall Configuration** — Automatic UFW/FirewallD setup
- **OS Support** — Ubuntu 22.04/24.04, Debian 11/12, Rocky Linux 8/9, AlmaLinux 8/9
- **Database Management** — Automated MariaDB setup and configuration
- **Docker Integration** — Seamless Docker installation for Elytra
- **Repair Tool** — Built-in repair tool to fix common permission and service issues
- **Health Checks** — Comprehensive health checking for panel, Elytra, and system resources
- **System Requirements Check** — Automatic detection of system resources with recommendations

## Quick Start

```bash
bash <(curl -sSL https://raw.githubusercontent.com/itzzjustmateo/hydro-install/main/install.sh)
```

Or download and run:

```bash
curl -sSL https://raw.githubusercontent.com/itzzjustmateo/hydro-install/main/install.sh -o install.sh
chmod +x install.sh
sudo bash install.sh
```

## Requirements

### Minimum Requirements

| Component | Specification |
|-----------|--------------|
| **CPU** | 2 cores (x86_64 or ARM64) |
| **RAM** | 2 GB |
| **Storage** | 20 GB SSD |
| **Network** | Public IPv4 or IPv6 |
| **OS** | Ubuntu 22.04/24.04, Debian 11/12, Rocky Linux 8/9, AlmaLinux 8/9 |

### Recommended Requirements

| Component | Specification |
|-----------|--------------|
| **CPU** | 4+ cores |
| **RAM** | 4+ GB |
| **Storage** | 50+ GB SSD |
| **Network** | Both IPv4 and IPv6 |

> **Note:** The installer will display a warning if your system is below minimum requirements. Swap space is recommended for systems with limited RAM.

> **Docker Compatibility:** Elytra requires Docker to run game servers. OpenVZ, LXC, or Virtuozzo virtualization are **not supported**. KVM, VMware, or dedicated servers work best. Run `systemd-detect-virt` to check your virtualization type.

## Installation Options

<img width="848" height="504" alt="Installation menu" src="https://github.com/user-attachments/assets/9974e217-f667-4488-8a13-8745a9d2498f" />

```bash
bash <(curl -sSL https://raw.githubusercontent.com/itzzjustmateo/hydro-install/main/install.sh)
```

## Maintenance Tools

### Repair Tool (Option 7)

The built-in repair tool can fix common issues:

- **Fix Panel Permissions** — Corrects ownership and permissions for web server
- **Fix Elytra Permissions** — Sets correct permissions for Elytra directories (UID 8888)
- **Clear Laravel Caches** — Clears config, cache, view, and route caches
- **Restart All Services** — Restarts nginx, PHP-FPM, hydroq, redis, and elytra
- **Fix Database Permissions** — Re-grants privileges to hydrodactyl database user
- **Setup Swap File** — Configure swap space for systems with limited RAM (1GB, 2GB, 4GB, or custom)

### Health Check (Option 8)

Comprehensive diagnostics for your installation:

- **Panel Health** — Checks directory structure, permissions, services (nginx, PHP-FPM, Redis, MariaDB, hydroq)
- **Elytra Health** — Validates binary, configuration, data directories, Docker, and service status
- **System Resources** — Displays CPU, RAM, disk, and swap information with requirement checking

### System Requirements Monitoring

The installer automatically displays system resources on startup:

- CPU core count with minimum/recommended checking
- RAM with human-readable display and warnings for low memory
- Available disk space monitoring
- Swap configuration status and setup recommendations

## SSL Certificate Auto-Renewal

When Let's Encrypt is configured, the installer automatically sets up:

- **Automatic Renewal** — Certificates renewed twice daily (as recommended by Let's Encrypt)
- **Service Restart Hooks** — nginx and Elytra automatically restart after successful renewal
- **Renewal Logging** — All renewal activity logged to `/var/log/hydrodactyl-certbot-renewal.log`
- **Health Verification** — Dry-run testing to ensure renewal configuration is valid

## Private Repository Support

The installer fully supports private GitHub repositories:

1. Select "private repository" during setup
2. Provide a GitHub Personal Access Token
3. The token is validated for repository access
4. Token is securely stored for auto-updaters

### Creating a GitHub Token

1. Go to https://github.com/settings/tokens
2. Click "Generate new token (classic)"
3. Select the `repo` scope
4. Generate and copy the token
5. Paste when prompted by the installer

## Custom Repositories

You can install from custom forks or private builds:

### Default Repositories

- **Panel**: `BlueprintFramework/hydrodactyl`
- **Elytra**: `pyrohost/elytra`

### Using Custom Repositories

During installation, select "Use custom repository" and provide:

- Repository in `owner/repo` format
- Whether it's public or private
- GitHub token (if private)

### Requirements for Custom Repositories

- Repository must have published releases
- Release must contain the expected assets:
  - Panel: `panel.tar.gz`
  - Elytra: `elytra_linux_amd64` or `elytra_linux_arm64`

### Uninstall Options

- **Panel only**: Removes panel files, database (optional), web server config
- **Elytra only**: Removes binary, configuration, Docker containers
- **Both**: Complete removal of all components
- **Auto-updaters only**: Removes update scripts and timers

## Directory Structure

```
/var/www/hydrodactyl/         # Panel installation
/etc/elytra/                 # Elytra configuration
/etc/hydrodactyl/             # Panel configuration
/var/lib/elytra/volumes      # Game server data (containers)
/var/lib/elytra/archives     # Server archives
/var/lib/elytra/backups      # Server backups
/var/log/hydrodactyl-*.log    # Installation/update logs
/var/backups/hydrodactyl/     # Panel backups
/var/backups/elytra/         # Elytra backups
```

## Troubleshooting

### Installation Issues

**Error: "No releases found in repository"**

- Ensure your repository has published releases
- For private repos, verify your token has `repo` access

**Error: "Token cannot access repository"**

- Verify the token has not expired
- Check the repository exists and is accessible
- For private repos, ensure token has `repo` scope

**Error: "Unsupported OS"**

- Check your OS is in the supported list
- Ensure you're using a supported version

### Post-Installation Issues

**Panel not accessible**

```bash
# Use the built-in Repair Tool (Option 7)
sudo bash <(curl -sSL https://raw.githubusercontent.com/itzzjustmateo/hydro-install/main/install.sh)

# Or manually check services:
systemctl status nginx
systemctl status hydroq
journalctl -u hydroq -f
```

**Elytra not connecting**

```bash
# Check Elytra health via Health Check (Option 8)
sudo bash <(curl -sSL https://raw.githubusercontent.com/itzzjustmateo/hydro-install/main/install.sh)

# Or manually check:
systemctl status elytra
journalctl -u elytra -f
cat /etc/elytra/config.yml
```

**Database connection errors**

```bash
systemctl status mariadb
mysql -u root -p -e "SHOW DATABASES;"
```

**Low memory / OOM errors**

```bash
# Check if swap is configured
free -h

# Use Repair Tool (Option 7) to set up swap if needed
# Or manually create swap:
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo "/swapfile none swap sw 0 0" | sudo tee -a /etc/fstab
```

**Queue worker not processing jobs**

```bash
# Check queue worker status
systemctl status hydroq
journalctl -u hydroq -f

# Check for failed jobs
cd /var/www/hydrodactyl
php artisan queue:failed
php artisan queue:retry all  # Retry failed jobs
```

### Firewall Issues

If you skipped firewall configuration during install:

**UFW (Ubuntu/Debian)**

```bash
ufw allow 80,443/tcp
ufw allow 8080/tcp
ufw allow 2022/tcp
ufw allow 25500:25600/tcp
ufw allow 25500:25600/udp
```

**FirewallD (Rocky/AlmaLinux)**

```bash
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
firewall-cmd --permanent --add-port=8080/tcp
firewall-cmd --permanent --add-port=2022/tcp
firewall-cmd --permanent --add-port=25565-25665/tcp
firewall-cmd --permanent --add-port=25565-25665/udp
firewall-cmd --permanent --add-port=27015-28025/tcp
firewall-cmd --permanent --add-port=27015-28025/udp
firewall-cmd --permanent --add-port=7777-8000/tcp
firewall-cmd --permanent --add-port=7777-8000/udp
firewall-cmd --permanent --add-port=28015-28025/tcp
firewall-cmd --permanent --add-port=28015-28025/udp
firewall-cmd --permanent --add-port=2456-2466/tcp
firewall-cmd --permanent --add-port=2456-2466/udp
firewall-cmd --permanent --add-port=30120-30130/tcp
firewall-cmd --permanent --add-port=30120-30130/udp
firewall-cmd --reload
```

## Logs

All installation and update operations are logged:

- **Installation**: `/var/log/hydrodactyl-installer.log`
- **Panel Updates**: `/var/log/hydrodactyl-panel-auto-update.log`
- **Elytra Updates**: `/var/log/hydrodactyl-elytra-auto-update.log`
- **SSL Renewal**: `/var/log/hydrodactyl-certbot-renewal.log`
- **Health Check Failures**: `/etc/hydrodactyl/update-health-check-failure.log` (Panel) or `/etc/elytra/update-health-check-failure.log` (Elytra)

## Game Server Ports

The installer automatically opens these specific port ranges for popular games:

| Game/Category | Port Range | Notes |
|--------------|------------|-------|
| **Minecraft** | 25565-25665 | Java & Bedrock editions |
| **Source Engine** | 27015-27150 | CS:GO, TF2, Garry's Mod, Left 4 Dead |
| **Unreal Engine** | 7777-8000 | ARK, Satisfactory (multiple ports per server) |
| **Rust** | 28015-28025 | Game + RCON ports |
| **Valheim** | 2456-2466 | Game + Query ports |
| **FiveM/GTA** | 30120-30130 | GTA V roleplay servers |
| **General Range** | 27015-28025 | Additional ports for other games |

### Multi-Port Requirements

Some games require multiple consecutive ports per server instance:

- **ARK**: 4 ports (game, query, RCON, steam)
- **Satisfactory**: 3 ports (game, query, beacon)
- **ARMA 3**: 3 ports (game, steam, RCON)
- **Rust**: 3 ports (game, RCON, app)
- **Valheim**: 3 ports (game, query, steam)

With all port ranges combined (approximately 2,000+ ports), you can host:

- 400+ single-port game servers
- 200+ multi-port game servers
- Mixed environment of various game types

## Architecture

```
┌─────────────────────────────────────┐
│          Hydrodactyl Panel          │
│   ┌─────────────────────────────┐   │
│   │      Nginx (Web Server)     │   │
│   │    PHP 8.3-FPM + Laravel    │   │
│   └─────────────────────────────┘   │
│   ┌─────────────────────────────┐   │
│   │     MariaDB (Database)      │   │
│   └─────────────────────────────┘   │
│   ┌─────────────────────────────┐   │
│   │   Redis (Queue/Cache)       │   │
│   └─────────────────────────────┘   │
└─────────────────────────────────────┘
                   │
                   │ HTTP/HTTPS
                   ▼
┌─────────────────────────────────────┐
│           Elytra Daemon             │
│   ┌─────────────────────────────┐   │
│   │     HTTP API (Port 8080)    │   │
│   └─────────────────────────────┘   │
│   ┌─────────────────────────────┐   │
│   │   Docker (Game Servers)     │   │
│   └─────────────────────────────┘   │
│   ┌─────────────────────────────┐   │
│   │    SFTP (Port 2022)         │   │
│   └─────────────────────────────┘   │
│   ┌─────────────────────────────┐   │
│   │  Game Ports (27015-28025)   │   │
│   └─────────────────────────────┘   │
└─────────────────────────────────────┘
```

## Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on how to contribute, branch naming, commit conventions, and the pull request process.

Before submitting changes, ensure your scripts pass syntax validation:

```bash
bash -n install.sh lib/*.sh installers/*.sh ui/*.sh
```

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

## Credits

- [Hydrodactyl Panel](https://github.com/BlueprintFramework/hydrodactyl) — The game server management panel (based on Pyrodactyl)
- [Pyrodactyl](https://github.com/pyrodactyl-oss/pyrodactyl) — The original panel software
- [Elytra](https://github.com/pyrohost/elytra) — The daemon software
- [Pyrodactyl Installer](https://github.com/Muspelheim-Hosting/pyrodactyl-installer) — The upstream installer that this project is forked from
- [Pterodactyl Installer](https://github.com/pterodactyl-installer/pterodactyl-installer) — Original inspiration

---

<p align="center">
  <b>Brought to you by <a href="https://muspelheim.host">Muspelheim Hosting</a></b>
</p>
