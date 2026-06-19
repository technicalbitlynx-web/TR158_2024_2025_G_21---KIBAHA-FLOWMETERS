# DAWASA Monitoring Dashboard

Real-time monitoring dashboard for Dar es Salaam Water & Sewerage Authority (DAWASA).  
Tracks flowmeters and pressure transmitters across WTP, Transmission Mains, Booster Pumping Stations, and Waste Stabilization Ponds.

**Live site:** https://technicalbitlynx-web.github.io/TR158_2024_2025_G_21---KIBAHA-FLOWMETERS/

---

## Default Login

| Field | Value |
|---|---|
| Username | `admin` |
| Password | `admin` |
| Role | Manager (full access) |

> All accounts must use a `@dawasa.go.tz` email address. Contact the system administrator to create additional accounts.

---

## Folder Structure

```
DAWASA-Dashboard/
├── index.html              # Main dashboard — single-file, self-contained
├── devices.json            # Pre-loaded device seed (auto-populates on first login)
├── assets/
│   └── images/
│       └── dawasa-logo.png # Official DAWASA logo (local copy)
├── backend/
│   └── requirements.txt    # Python dependencies for the VIDAA TV remote backend
├── .venv/                  # Python virtual environment (not committed)
├── .gitignore
├── README.md
└── PROJECT_DOCUMENT.md     # Internal retrospective (local only, not pushed)
```

---

## Running Locally

```powershell
# Activate the virtual environment
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
.\.venv\Scripts\Activate.ps1

# Serve the dashboard
python -m http.server 8080
```

Visit **http://localhost:8080**

---

## Pre-loaded Devices (Kibaha Flowmeters)

These 5 devices are seeded automatically from `devices.json` on first login — no CSV import required.

| Device | Site | Pipe Size | MQTT Topic |
|---|---|---|---|
| Kibaha RPC 48 | TM (Transmission Mains) | 48″ | `rpc/flow/48inch` |
| Kibaha RPC 36 | TM (Transmission Mains) | 36″ | `rpc/flow/36inch` |
| Kibaha Mpakani 24 | TM (Transmission Mains) | 24″ | `mpkn/flow/24inch` |
| Kibaha Mpakani 30 | TM (Transmission Mains) | 30″ | `mpkn/flow/30inch` |
| Mlandizi 16 | TM (Transmission Mains) | 16″ | `mlndz/flow/16inch` |

**MQTT Broker:** `wss://broker.emqx.io:8084/mqtt` (HTTPS) / `ws://broker.emqx.io:8083/mqtt` (local)

To add or modify devices, edit `devices.json` and push — or use the **Add Device** option in the dashboard (Manager role required).

---

## Features

- **Auto-seeded devices** — visitors see data immediately after logging in, no import needed
- **CSV Import / Export** — managers can load or download device lists (HTTPS-compatible)
- **Flowmeter Dashboard (Overview)** — live flow readings with gauge visualisation
- **Pressure Dashboard** — pressure transmitter monitoring
- **Alerts** — active alerts and historical alert log
- **Historical Data** — time-series export as CSV or PDF
- **Role-based access** — User and Manager roles (Manager can add/remove devices)
- **Dark / Light theme** — toggle in the UI
- **Responsive** — works on desktop and TV displays

---

## VIDAA TV Remote Backend

A separate Flask API (`backend/`) sends remote-control commands to a Hisense VIDAA TV over the network, allowing the dashboard to be operated from a TV remote.

```bash
# Install dependencies
pip install -r backend/requirements.txt

# Set TV_IP in backend/vidaa_remote_backend.py, then run:
python backend/vidaa_remote_backend.py
# → available at http://localhost:5000
```

---

## Deployment

The dashboard is hosted on **GitHub Pages** from the `main` branch root.

```bash
# Push changes to GitHub Pages
git push kibaha main
```

Remote `kibaha` → `https://github.com/technicalbitlynx-web/TR158_2024_2025_G_21---KIBAHA-FLOWMETERS`  
Remote `origin` → `https://github.com/technicalbitlynx-web/DAWASA_IoT_csv`
