# lamleunghomepc3

Server information for the `lamleunghomepc3` device.

## Identity

| Item | Value |
|---|---|
| Hostname | `lamleunghomepc3` |
| LAN IP | `192.168.0.39/24` (interface `wlan0`) |
| Board | CM311-1a-YST (Amlogic, `linuxfamily`: amlogic) |
| OS | Armbian 26.11.3 (Debian 12 bookworm) |
| Kernel | `6.12.117-ophub` |
| Architecture | aarch64 |
| Timezone | Asia/Shanghai (CST, +0800), clock synchronized |
| Uptime | ~4 hours 47 minutes (at time of capture) |

## Hardware

| Item | Value |
|---|---|
| CPU | 4x ARM Cortex-A53 (max 1.9 GHz) |
| Memory | 3.6 GiB total |
| Storage | `/dev/mmcblk2` 116.5 GiB (eMMC) |
| `/boot` | 511 MiB (`mmcblk2p1`) |
| `/` | 115.9 GiB, 2.2 GiB used, 112 GiB free (2%) — `mmcblk2p2` |
| Temperature | ~50 °C |

## Network / Services

| Item | Value |
|---|---|
| SSH | `0.0.0.0:22` and `[::]:22` — OpenSSH 9.2p1 (Debian-2+deb12u10) |
| rpcbind | `0.0.0.0:111` |
| systemd-resolved | `127.0.0.53:53`, `127.0.0.54:53` |
| LLMNR | `0.0.0.0:5355` |

## Accounts

| User | UID | Shell | Notes |
|---|---|---|---|
| `lamleunghome` | 1000 | `/usr/bin/bash` | groups: tty, disk, dialout, `sudo`, audio, video, plugdev, games, users, systemd-journal, input, render, i2c, netdev, bluetooth, gpio, spi, docker |

## SSH Access Policy

- `PermitRootLogin prohibit-password` — root may log in by SSH **key only**, password auth for root is refused.
  - Enforced via `/etc/ssh/sshd_config.d/20-root-no-password.conf`.
- `PasswordAuthentication yes` — non-root users may still use password auth.
- `PubkeyAuthentication yes`.
- Passwordless login for `lamleunghome` is configured with an installed ed25519 key.

## Access

```bash
# Non-root (recommended)
ssh lamleunghome@192.168.0.39

# Root (key only, password refused)
ssh -i <key> root@192.168.0.39
```

## Notes

- Docker is **not** installed on this host.
- Root password login was previously allowed and has been disabled; revert with:
  ```bash
  sudo rm /etc/ssh/sshd_config.d/20-root-no-password.conf && sudo systemctl reload ssh
  ```
