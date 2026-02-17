# telegram2teldrive — User Manual (Start to End)

This guide walks you through everything from setup to running imports, for both PostgreSQL/Teldrive mode and MongoDB mode.

---

## 1) What this tool does

`telegram2teldrive.py` connects to your Telegram account, scans documents in selected channels, and stores metadata in your chosen backend:

- **PostgreSQL mode (`--db-driver postgres`)**: inserts into Teldrive tables (`files`, `channels`, etc.).
- **MongoDB mode (`--db-driver mongodb`)**: stores metadata in MongoDB collections.

---

## 2) Requirements

- Python 3.11+ recommended
- Telegram API credentials
  - `api-id`
  - `api-hash`
  - your Telegram phone number
- One backend:
  - PostgreSQL (for Teldrive integration), or
  - MongoDB (for metadata storage in your own project)

---

## 3) Get Telegram API credentials

1. Open your Teldrive `config.toml` (or your Telegram app config source).
2. Copy:

```toml
[tg]
app-id = "<Telegram API ID>"
app-hash = "<Telegram API hash>"
```

3. Keep your phone number in international format, e.g. `+15551234567`.

---

## 4) Install from scratch

### Linux/macOS

```bash
git clone https://github.com/iwconfig/telegram2teldrive
cd telegram2teldrive
python3 -m venv pyvenv
source pyvenv/bin/activate
pip install -r requirements.txt
```

### Windows (PowerShell)

```powershell
git clone https://github.com/iwconfig/telegram2teldrive
cd telegram2teldrive
python -m venv pyvenv
.\pyvenv\Scripts\Activate.ps1
pip install -r requirements.txt
```

---

## 5) Choose your backend mode

## A) PostgreSQL / Teldrive mode

Use this when you want imported metadata to appear inside Teldrive.

Required DB values:
- DB name
- DB user
- DB password
- DB host
- DB port

Example CLI:

```bash
python3 telegram2teldrive.py \
  --db-driver postgres \
  --db-name teldrive \
  --db-user myuser \
  --db-password mypass \
  --db-host 127.0.0.1 \
  --db-port 5432
```

## B) MongoDB mode

Use this when your own project stores metadata in MongoDB (not Teldrive tables).

Required Mongo values:
- Mongo URI (for example `mongodb://localhost:27017`)
- Mongo DB name

Optional:
- files collection (default `telegram_files`)
- channels collection (default `telegram_channels`)

Example CLI:

```bash
python3 telegram2teldrive.py \
  --db-driver mongodb \
  --mongo-uri "mongodb://localhost:27017" \
  --mongo-db "telegram2teldrive" \
  --mongo-files-collection "telegram_files" \
  --mongo-channels-collection "telegram_channels"
```

---

## 6) Configure with a TOML file (recommended)

Create `telegram2teldrive.toml` in the project directory:

```toml
[telegram]
api-id = "<Telegram API ID>"
api-hash = "<Telegram API hash>"
phone-number = "+15551234567"
# channels = "all" # optional

[database]
driver = "mongodb" # "postgres" or "mongodb"

# Used in postgres mode:
name = "<db name>"
user = "<db user>"
password = "<db password>"
host = "localhost"
port = "5432"

[mongodb]
uri = "mongodb://localhost:27017"
db = "telegram2teldrive"
files_collection = "telegram_files"
channels_collection = "telegram_channels"

[teldrive]
folder_name = "Imported"
```

Run with default config filename:

```bash
python3 telegram2teldrive.py
```

Run with a specific config path:

```bash
python3 telegram2teldrive.py --config /path/to/telegram2teldrive.toml
```

Or via env var:

```bash
export CONFIG_FILE=/path/to/telegram2teldrive.toml
python3 telegram2teldrive.py
```

---

## 7) First run authentication flow

On first run, Telethon prompts for login verification:

1. Enter your phone number (if not passed by config/CLI).
2. Enter the OTP code sent by Telegram.
3. If enabled, enter 2FA password.

Session is stored in:

- `./telegram2teldrive.session`

Next runs usually won’t ask again unless the session expires or is removed.

---

## 8) Channel selection

If `--channels` is not provided, the script shows an interactive menu.

Supported inputs:

- `0`, `a`, `all`, or empty enter → all channels
- `1` → single channel
- `1,4,5` → multiple channels
- `1-3` → range
- `1,4,5-8` → mixed

Non-interactive channel selection:

```bash
python3 telegram2teldrive.py --channels all
python3 telegram2teldrive.py --channels 12345,98765
```

---

## 9) What gets stored

For each Telegram document message, the tool stores metadata like:

- file name
- file size
- mime type
- category (`image`, `video`, `audio`, `document`, `archive`, `other`)
- Telegram message ID
- channel ID / channel name
- timestamp fields

Duplicate detection is based on Telegram message ID + channel/user context, so reruns generally skip already-imported items.

---

## 10) Example end-to-end runs

### Example 1: MongoDB full run

```bash
python3 telegram2teldrive.py \
  --api-id 123456 \
  --api-hash "abcd1234" \
  --phone-number "+15551234567" \
  --db-driver mongodb \
  --mongo-uri "mongodb://localhost:27017" \
  --mongo-db "myproject" \
  --mongo-files-collection "tg_files" \
  --mongo-channels-collection "tg_channels" \
  --channels all
```

### Example 2: PostgreSQL/Teldrive full run

```bash
python3 telegram2teldrive.py \
  --api-id 123456 \
  --api-hash "abcd1234" \
  --phone-number "+15551234567" \
  --db-driver postgres \
  --db-name teldrive \
  --db-user postgres \
  --db-password secret \
  --db-host 127.0.0.1 \
  --db-port 5432 \
  --folder-name Imported \
  --channels all
```

---

## 11) Troubleshooting

## `ModuleNotFoundError: tomllib`

- You are likely on Python < 3.11.
- Fix: use Python 3.11+.

## `MongoDB support requires 'pymongo'`

- Install deps in your venv:

```bash
pip install -r requirements.txt
```

## Cannot connect to MongoDB

- Verify URI, DB name, network/firewall, and auth options.
- Test connection separately with `mongosh`.

## Cannot connect to PostgreSQL

- Verify host/port/user/password/db name.
- If DB is in Docker, expose `5432` and check container health.

## Telegram login keeps asking again

- Ensure `telegram2teldrive.session` is writable/persistent.
- Don’t delete session file between runs.

---

## 12) Safety and best practices

- Backup your DB before running imports.
- Start with one small channel as a test.
- Keep credentials in config/env, not shell history.
- Use least-privilege DB users when possible.

---

## 13) Quick command reference

Show help:

```bash
python3 telegram2teldrive.py --help
```

Run with config file:

```bash
python3 telegram2teldrive.py --config ./telegram2teldrive.toml
```

Force Mongo mode:

```bash
python3 telegram2teldrive.py --db-driver mongodb --mongo-uri "mongodb://localhost:27017" --mongo-db mydb
```

Force Postgres mode:

```bash
python3 telegram2teldrive.py --db-driver postgres --db-name teldrive --db-user user --db-password pass
```

---

If you want, I can also provide a **sample production config** with redacted placeholders specifically for your MongoDB deployment (Atlas, local Docker, or self-hosted replica set).
