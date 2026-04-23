# kasm-hackbox

> Hack-the-Box ready Docker Image for KASM Workspaces, based on Ubuntu Focal maintained by KASM Tech.

## What's inside

| Tool | Purpose |
|------|---------|
| **Starship** | Cross-shell prompt (xcad dotfiles config) |
| **Hack Nerd Font v3** | Terminal font with glyphs/icons |
| **eza** | Modern `ls` replacement with icons |
| **zoxide** | Smarter `cd` with frecency ranking |
| **direnv** | Per-directory environment variables |
| **fzf** | Fuzzy finder |
| **bat** | `cat` with syntax highlighting |
| **ripgrep** | Fast grep |
| **fd** | Fast `find` alternative |
| **nmap / netcat / dnsutils / whois** | Network recon tools |
| **OpenVPN** | VPN client for HTB connections |
| **Terminator** | Tiling terminal with xcad color theme |
| **Warp theme** | xcad2k-dark theme for Warp terminal |
| **Numix Dark** | XFCE dark GTK + icon theme |

## Shell aliases loaded in bash

```bash
alias ls="eza --icons --group-directories-first"
alias ll="eza --icons --group-directories-first -l"
alias la="eza --icons --group-directories-first -la"
alias cat="batcat"
alias fd="fdfind"
```

## Terminal Colors — xcad theme

| Role | Hex |
|------|-----|
| Background | `#1A1A1A` |
| Foreground | `#F1F1F1` |
| Black | `#121212` |
| Red | `#A52AFF` |
| Green | `#7129FF` |
| Yellow | `#3D2AFF` |
| Blue | `#2B4FFF` |
| Magenta | `#2883FF` |
| Cyan | `#28B9FF` |
| White | `#F1F1F1` |
| Bright Black | `#666666` |
| Bright Red | `#BA5AFF` |
| Bright Green | `#905AFF` |
| Bright Yellow | `#685AFF` |
| Bright Blue | `#5C78FF` |
| Bright Magenta | `#5EA2FF` |
| Bright Cyan | `#5AC8FF` |
| Bright White | `#FFFFFF` |

## Run locally

```bash
docker run --rm -it --shm-size=512m -p 6901:6901 -e VNC_PW=password xcad2k/hackbox
```

Connect to `https://localhost:6901` — username `kasm_user`, password `password`.

## Use in Kasmweb

Paste this into **Docker Run Config Override (JSON)** to allow VPN tunneling:

```json
{"cap_add":["NET_ADMIN"],"devices":["dev/net/tun","/dev/net/tun"],"sysctls":{"net.ipv6.conf.all.disable_ipv6":"0"}}
```

## OpenVPN to Hack The Box

```bash
openvpn --config <your-config-file>
```
