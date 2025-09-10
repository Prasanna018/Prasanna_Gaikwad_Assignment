# React Web Scraper (Google OAuth)
# Deployed on render :- https://web-scraper-frontend-ifmy.onrender.com/
A full-stack starter that satisfies your requirements:

- **ReactJS** frontend with **OAuth 2.0 (Google)** using `@react-oauth/google`
- **Python FastAPI** backend only (no Node backend), with web scraping using `requests` + `BeautifulSoup`
- **Robots-aware** scraping helper (uses `urllib.robotparser`)
- **Responsive UI** with simple cards and a refresh button
- **Real-time refresh** of scraped data with loading state
- **Setup docs** in this README

> Demo scraper targets **https://quotes.toscrape.com** — a public site intended for educational scraping.

---

## Project Structure

```
freshers-react-scraper/
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── auth.py
│   │   ├── scraper.py
│   │   └── __init__.py
│   ├── requirements.txt
│   └── .env.example
├── frontend/
│   ├── index.html
│   ├── package.json
│   ├── vite.config.js
│   └── src/
│       ├── main.jsx
│       ├── App.jsx
│       ├── api.js
│       ├── styles.css
│       └── components/
│           ├── Login.jsx
│           └── DataView.jsx
└── README.md  (this file)
```

---

## Prerequisites

- **Python 3.10+**
- **Node.js 18+**
- A **Google OAuth Client ID** (Web) from Google Cloud Console
  - Authorized JS origin (dev): `http://localhost:5173`
  - Authorized redirect URI: not required with One Tap/Popup

---

## Backend (FastAPI)

### 1) Configure environment

Create a `.env` file in `backend/` based on `.env.example`:

### Provided working my google client id 
```
GOOGLE_CLIENT_ID=657194342637-bnjs1siqbpi1v39btii2ahu0dhhd34ao.apps.googleusercontent.com
ALLOWED_ORIGINS=http://localhost:5173
```


> Only Python is used for backend.

### 2) Install & run

```bash
cd backend
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

Backend will be on **http://localhost:8000**.

---

## Frontend (React + Vite)

### 1) Set Google Client ID

Open `frontend/src/App.jsx` and set `VITE_GOOGLE_CLIENT_ID` via env:

Create `frontend/.env`:

```
VITE_GOOGLE_CLIENT_ID=657194342637-bnjs1siqbpi1v39btii2ahu0dhhd34ao.apps.googleusercontent.com
VITE_API_BASE=http://localhost:8000
```

### 2) Install & run

```bash
cd frontend
npm install
npm run dev
```

Frontend runs on **http://localhost:5173**.

---

## What it does

1. **Login with Google:** Frontend obtains a Google **ID token** via `@react-oauth/google`.
2. **Verify on backend:** Sends ID token to `POST /api/auth/google`. FastAPI verifies it using Google libraries.
3. **Scrape data:** Frontend calls `GET /api/scrape?tag=life` (optional tag) which scrapes quotes from `quotes.toscrape.com`,
   respecting robots.txt.
4. **Display UI:** Shows quotes in responsive cards, with a **Refresh** button and **loading spinner**.

---







#




