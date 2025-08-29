# Flask URL Shortener (MySQL)

A tiny URL shortener built with Flask + SQLAlchemy + MySQL.

## Features
- REST API to shorten a long URL
- Redirect route to the original URL
- Minimal frontend to input a link and show the short URL
- Uses MySQL for storage

## Quickstart

### 1) Create the MySQL database
```sql
CREATE DATABASE IF NOT EXISTS url_shortener CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### 2) Configure environment
Copy `.env.example` to `.env` and fill your MySQL credentials.

```bash
cp .env.example .env
# then edit .env
```

### 3) Create a virtual environment & install deps
```bash
python -m venv .venv
source .venv/bin/activate  # on Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

### 4) Run
```bash
python app.py
# App runs on http://127.0.0.1:5000
```

### 5) Use the API
```bash
curl -X POST http://127.0.0.1:5000/api/shorten \
  -H "Content-Type: application/json" \
  -d '{"url":"https://example.com/some/very/long/link"}'
```

You’ll get back:
```json
{"short_url": "http://127.0.0.1:5000/Ab12XyZ", "code": "Ab12XyZ"}
```

Open `http://127.0.0.1:5000/Ab12XyZ` to be redirected.

## Notes
- The app auto-creates the `urls` table on first request.
- For production, run behind a real server (gunicorn + nginx) and set a strong `SECRET_KEY`.
- To change the short code length, tweak `generate_code(n=7)` in `app.py`.
