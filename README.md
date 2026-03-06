# XariServers

Infrastructure inventory for all Xari / joche.ojeda@bitframeworks.com servers.

> ⚠️ Credentials are stored in Bitwarden vault (`sonofanton.jocheojeda.com`) under the **Contabo Xari** folder. This doc covers topology, roles, and access patterns only.

---

## Contabo Account — joche.ojeda@bitframeworks.com (INT-53776)

Portal: https://my.contabo.com

| Name | IP | Instance ID | Region | OS | Specs | Role |
|---|---|---|---|---|---|---|
| **xari-keycloak** | 66.94.114.62 | 202711131 | US-west | Ubuntu 24.04 | Cloud VPS 20 SSD | Keycloak 26 + Caddy reverse proxy |
| **joche-remote-dev** | 207.244.253.16 | 200652507 | US-central | Windows Server | VPS S SSD | Joche Remote Dev (Windows) |
| **xari-windows-prod** | 209.126.3.38 | 200372957 | US-central | Windows Server | VPS S SSD | Windows PRODUCTION (formatted 04-11-2025) |
| **xari-windows-test** | 167.86.85.62 | 200282730 | EU | Windows Server | VPS S SSD | Windows PRUEBAS 2 (formatted 24-02-2025) |
| **old-websites** | 80.241.215.103 | 200277619 | EU | Ubuntu | VPS S SSD | ⚠️ OLD — DO NOT USE IN PRODUCTION (needs format) |
| **rustdesk** | 209.126.10.250 | 200367739 | US-central | Ubuntu | VPS S SSD | RustDesk relay/ID server |
| **websites** | 154.53.49.85 | 200688966 | US-east | Ubuntu | VPS M SSD | NEW websites server (formatted 3/2/2025) |
| **vpn-virginia** | 89.117.53.109 | 201580619 | EU | Ubuntu | VPS S SSD | PiVPN Virginia (OpenVPN) |
| **vmi2540775** | 209.126.86.123 | 202540775 | US-central | — | VPS 4 Cores Storage | _(unassigned / unknown role)_ |
| **openclaw-xari** | 31.220.79.196 | 203105444 | EU | Ubuntu | Cloud VPS 50 SSD | OpenClaw agent |

---

## Other Providers

| Name | IP | Provider | OS | Role |
|---|---|---|---|---|
| **windows-old** | 5.189.173.9 | Contabo | Windows Server 2016 | Old Windows server |
| **vmi154** | 154.12.245.107 | Contabo | Ubuntu | Cloud VPS 20 SSD — Seattle (unassigned) |

---

## Server Details

### xari-keycloak — 66.94.114.62

**Role:** Keycloak 26 + Caddy reverse proxy. US-west.

- **SSH:** `ssh root@66.94.114.62` | credentials → Bitwarden
- Docker containers: `keycloak` (port 8080), `caddy` (80/443)
- PostgreSQL 16 on port 5432

**Services:**
| Port | Service | Description |
|---|---|---|
| 80/443 | Caddy | Reverse proxy / TLS |
| 8080 | Keycloak 26 | Auth server |
| 5432 | PostgreSQL 16 | DB for Keycloak |

**Databases:**
| Database | Owner |
|---|---|
| `keycloak` | keycloak |

**Credentials → Bitwarden (Contabo Xari):**
- Root SSH password
- Keycloak DB password

---

### joche-remote-dev — 207.244.253.16

**Role:** Windows development server for Joche. US-central.

- **RDP:** Administrator / password → Bitwarden
- **SQL Server:** `sa` / password → Bitwarden

**Credentials → Bitwarden (Contabo Xari):**
- Windows Administrator password
- SQL Server `sa` password

---

### xari-windows-prod — 209.126.3.38

**Role:** Windows PRODUCTION server (formatted 04-11-2025). US-central.

- **RDP:** Administrator / password → Bitwarden
- **SQL Server:** `sa` / password → Bitwarden
- Hosts: `insurance.xari.net` (via 167.86.85.62)

**Credentials → Bitwarden (Contabo Xari):**
- Windows Administrator password
- SQL Server `sa` password

---

### xari-windows-test — 167.86.85.62

**Role:** Windows PRUEBAS 2 (formatted 24-02-2025). EU.

- **RDP:** Administrator / password → Bitwarden
- **SQL Server:** `sa` / password → Bitwarden
- Domain: `insurance.xari.net`

**Credentials → Bitwarden (Contabo Xari):**
- Windows Administrator password
- SQL Server `sa` password

---

### old-websites — 80.241.215.103

**Role:** ⚠️ OLD Ubuntu website server — DO NOT USE IN PRODUCTION. Needs to be formatted.

- **SSH:** `ssh root@80.241.215.103`
- **Webmin:** https://80.241.215.103:10000/
- Virtualmin with many hosted sites (see list below)

**Hosted virtual hosts (to be migrated to `websites`):**
`aistorybuildersonline`, `analyzer`, `archivo`, `bitframeworks`, `blazoripfs`, `brevitas`,
`devexpressdashboard`, `docs`, `javier`, `jocheojeda`, `kc`, `nc2repairs`, `newxafersjobs`,
`omnileague`, `onlyplants`, `photoset.io`, `signalr`, `sivar`, `sivartoken`, `syncframework`,
`system`, `tinker`, `tonmd`, `url`, `wordpress`, `worldtour`, `wrpavers`, `xafers`, `xafersjobs`,
`xafersnet`, `xaferstraining`, `xafmarin`, `xamarin-ios-apps`, `xari`

**Credentials → Bitwarden (Contabo Xari):**
- Root SSH password
- Webmin credentials

---

### rustdesk — 209.126.10.250

**Role:** RustDesk self-hosted ID + relay server. US-central.

- **SSH:** `ssh root@209.126.10.250`
- **Webmin:** https://209.126.10.250:10000/
- Docker-based RustDesk deployment

**RustDesk connection info:**
| Field | Value |
|---|---|
| ID Server | 209.126.10.250 |
| Relay Server | 209.126.10.250 |
| RustDesk Client ID | 375481814 |

**Credentials → Bitwarden (Contabo → RustDesk Server):**
- Root SSH password
- RustDesk client password
- Desktop user: `rduser`

---

### websites — 154.53.49.85

**Role:** NEW Ubuntu websites server (formatted 3/2/2025). US-east. Primary hosting for all Xari domains.

- **SSH:** `ssh -p 2222 root@154.53.49.85` ⚠️ port 2222
- **Virtualmin:** https://vmi688966.contaboserver.net:10000/

**Active websites:**
| Domain | Status | Notes |
|---|---|---|
| jocheojeda.com | ✅ Working | |
| nc2repairs.com | ✅ Working | |
| xari.io | ✅ Working | |
| xafmarin.com | ✅ Working | |
| bitframeworks.com | ⚠️ Migration issues | |
| wrpavers.com | ✅ Working | |
| docs.xari.io | ⚠️ No content yet | |
| xafers.training | ⚠️ Migration issues | |
| devexpressdashboard.com | ✅ Working | |

**Databases (MariaDB):**
| Database | User | Used by |
|---|---|---|
| `wrpavers` | `wrpavers` | wrpavers.com WordPress |
| `docs` | `docs` | docs.xari.io WordPress |

**Credentials → Bitwarden (Contabo Xari):**
- Root SSH password
- MariaDB root password
- Virtualmin admin: `jocheojeda` / password
- WordPress `wrpavers` credentials
- WordPress `docs.xari.io` credentials
- WordPress `devexpressdashboard.com` credentials
- Virtualmin `bitframeworks` user credentials
- Virtualmin `devexpressdashboard` user credentials

---

### vpn-virginia — 89.117.53.109

**Role:** PiVPN Virginia — OpenVPN server. EU.

- **SSH:** `ssh root@89.117.53.109`
- OpenVPN (`pivpn`)

**Active VPN clients:**
| Client | Status | Expiry |
|---|---|---|
| vmi1580619 (server) | Valid | Mar 2034 |
| jmiphone15 | Valid | Oct 2029 |
| jochemacair | Valid | Oct 2029 |
| mangohomespb | Revoked | — |
| mangorouterspb | Valid | Oct 2029 |
| mango-arizona | Valid | Oct 2029 |
| mango-san-salvador | Valid | Oct 2029 |
| squirrel | Valid | Mar 2027 |
| msi | Valid | Mar 2027 |
| amor | Valid | Mar 2027 |
| netgear_nighthawk | Valid | Dec 2029 |
| ivan_cell | Valid | Mar 2027 |
| lera_cell | Valid | Mar 2027 |
| dan_cell | Valid | Mar 2027 |
| mikha_cell | Valid | Mar 2027 |
| alina_cell | Valid | Mar 2027 |

**Commands:**
```bash
# Add new client
pivpn add
# Add client for router (no password)
pivpn add nopass
# QR code
pivpn -qr
```

**Credentials → Bitwarden (Contabo Xari):**
- Root SSH password

---

### windows-old — 5.189.173.9

**Role:** Old Windows Server 2016 Datacenter.

- **RDP:** Administrator / password → Bitwarden
- **VNC:** 173.212.243.86:63090 / password → Bitwarden
- OS: Windows Server 2016 Datacenter Edition (64-bit)

**Credentials → Bitwarden (Contabo Xari):**
- Administrator password
- VNC password

---

### vmi154 — 154.12.245.107

**Role:** Unassigned. Seattle, US-west. Contabo Cloud VPS 20 SSD.

- **VNC:** 66.94.127.64:63222 / password → Bitwarden
- SSH credentials: set during order process

---

## Tools & Internal Services

| Tool | URL | Notes |
|---|---|---|
| URL Shortener | http://url.xafers.info/ | |
| Source / Gitea | https://source.xafers.info/ | |
| Analyzer | http://analyzer.xafers.training/ | |

---

## Credentials Reference

All credentials stored in **Bitwarden** → vault at `sonofanton.jocheojeda.com` → **Contabo Xari** folder.

| Bitwarden Item | What it contains |
|---|---|
| `Contabo API - joche.ojeda (xari)` | INT-53776, client secret, API password |
| `Server - vmi688966 (154.53.49.85)` | Root pw, MariaDB root, Virtualmin, WordPress creds |
| `Server - vmi277619 (80.241.215.103)` | Root pw, Webmin (old websites — do not use) |
| `Server - vmi282730 (167.86.85.62)` | Windows Administrator pw, SQL Server sa pw |
| `Server - vmi372957 (209.126.3.38)` | Windows Administrator pw, SQL Server sa pw |
| `Server - vmi652507 (207.244.253.16)` | Windows Administrator pw, SQL Server sa pw |
| `Server - vmi367739 (209.126.10.250)` | Root pw, RustDesk client ID + password |
| `Server - vmi1580619 (89.117.53.109)` | Root pw (OpenVPN server) |
| `Server - vmi2711131 (66.94.114.62)` | Root pw, Keycloak DB password |
| `Server - vmi3105444 (31.220.79.196)` | Root pw (OpenClaw) |
| `RustDesk Server - 209.126.10.250` | RustDesk ID, password, relay config |
