# DAWASA Monitoring Dashboard

Real-time monitoring dashboard for Dar es Salaam Water & Sewerage Authority (DAWASA).
Tracks flowmeters and pressure transmitters across WTP, Transmission Mains, Booster Pumping Stations, and Waste Stabilization Ponds.

---

## Folder Structure

```
DAWASA-Dashboard/
├── index.html              # Main dashboard (single-file, self-contained)
├── assets/
│   └── images/
│       └── dawasa-logo.png # Official DAWASA logo
├── backend/
│   ├── vidaa_remote_backend.py   # Flask API for VIDAA TV remote control
│   └── requirements.txt          # Python dependencies for the backend
├── .venv/                  # Python virtual environment (not committed)
├── .gitignore
└── README.md
```

---

## Quick Start — Dashboard (no server required)

Open `index.html` directly in a browser, **or** serve it locally for full feature support:

```bash
# From the project root
python -m http.server 8080
```

Then visit: **http://localhost:8080**

---

## Quick Start — TV Remote Backend

The backend sends remote-control commands to a Hisense VIDAA TV over the network.

```bash
# 1. Activate the virtual environment (Windows PowerShell)
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
.\.venv\Scripts\Activate.ps1

# 2. Install dependencies
pip install -r backend/requirements.txt

# 3. Set your TV IP in backend/vidaa_remote_backend.py (TV_IP variable)

# 4. Run the backend
python backend/vidaa_remote_backend.py
```

The backend will be available at `http://localhost:5000`.

---

## Features

- **CSV Import/Export** — load device data from CSV files
- **Flowmeter Dashboard** — live flow readings with gauge visualisation
- **Pressure Dashboard** — pressure transmitter monitoring
- **Alerts** — active alerts and historical alert log
- **Historical Data** — time-series export (CSV / PDF)
- **Role-based access** — standard user and manager roles
- **Dark / Light theme** — toggle in the UI
- **Responsive** — works on desktop and TV displays

---

## Credentials

Access is restricted to `@dawasa.go.tz` email addresses.
Contact your system administrator for account creation.
