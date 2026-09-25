# [APMap]

## Introduction

This is the repository for the APMap in the department of Computer Science and Information Engineering, National Taiwan University

## Developers

邱紀寰、魏勻希

## Repository Layout
```
├── manage.py
├── requirements.txt
├── .env
│
├── config/                  # Django project 總設定
│   ├── __init__.py
│   ├── settings.py          # 需在此設定 Celery 與 JWT 參數
│   ├── urls.py              
│   ├── asgi.py
│   └── wsgi.py
│
├── auth_api/                #處理 LDAP 登入與 JWT 核發
│   ├── __init__.py
│   ├── services.py          
│   ├── views.py             # 提供 /api/login 端點
│   └── urls.py
│
├── iperf_api/               # iperf 測速 API
│   ├── __init__.py
│   ├── services.py          
│   ├── serializers.py
│   ├── views.py
│   └── urls.py
│
└── heatmap/                 # 給前端 Leaflet 用的熱力圖 JSON
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── serializers.py
    ├── tests.py
    ├── upload_measure_points.py
    ├── vsz_client.py
    ├── views.py
    └── urls.py
```

### Files on Host Machine (Not in Repository)

> 若有任何「必須存於伺服器實體路徑、但沒有進 Git 的檔案」請在這邊列一個表格

## Quick Start

### 1. Prerequisites

- python 3
- Node.js / npm
- the repository vanchiu5288/nasa3-

### 2. Backend Setup

Create and activate a Python virtual environment:
```
python -m pip install -r requirements.txt
python -m pip install django-cors-headers
```

Start the Django server:
- For basic local development:
```
python manage.py runserver
```
The backend will be available at: [http://127.0.0.1:8000/](http://127.0.0.1:8000/)

> If the project requires VSZ credentials or the oneDirector tunnel, follow the instructions in [02 Setup](/docs/02-setup.md) before starting Django.

### 3. Frontend Setup

If Node,js and npm are not installed, install them using NVM:
```
sudo apt update
sudo apt upgrade -y
sudo apt-get install -y curl
```

Install NVM:
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
```

Restart the terminal, then install Node.js:
```
nvm install --lts
```

Check the installation:
```
node --version
npm --version
```

Install frontend dependencies:
- Enter the frontend directory (only have to do this once):
```
cd frontend
npm install
```
- Start the Vite development server:
```
npm run dev
```
- The frontend will normally be available at: [http://localhost:5173/](http://localhost:5173)

### 4. Leaflet

The project uses Leaflet for map-related functionality. Install the required packages if they are not already listed in `package.json`:
```
npm install leaflet react-leaflet
```

### 5. Database

The project uses Django migrations to initialize and update the database. 
Create/update the local SQLite database (`db.sqlite3`):
```
python manage.py makemigrations
python manage.py migrate
```

#### Django Admin

To create an administration account:
```
python manage.py createsuperuser
```

Then start Django:
```
python manage.py runserver
```

Open:
[http://127.0.0.1:8000/admin](http://127.0.0.1:8000/admin)

### 6. Running the Full Application

Indevelopment, run the backend and frontend separately.

#### Terminal 1 - Backend
```
source .venv/bin/activate
(venv) python manage.py runserver
```

#### Terminal 2 - Frontend
```
cd frontend
npm run dev
```

Then open:
[http://localhost:5173](http://localhost:5173)

### 7. CSIE Workstation

The project is deployed/developed on the CSIE workstation environment. Use the CSIE VPN (recommended) or use the CSIE workstation as a jump host to access the server. 
```
wifi1 IP: 172.16.127.110
```

For SSH key setup, GitHub Deploy Keys, VSZ authentication, environment variables, and the oneDirector SSH tunnel, see [02 Setup](/docs/02-setup.md)

## Documentation Index

- [01 System Design](/docs/01-architecture.md)
- [02 Setup](/docs/02-setup.md)
- [03 APIs & Database Schema](/docs/03-api-and-db.md)
- [04 Integration Guide](/docs/04-migration.md)
