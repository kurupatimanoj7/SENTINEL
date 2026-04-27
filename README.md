# SENTINEL

Anonymous tamper-evident whistleblower network demo.

SENTINEL lets a user submit a report from a web interface, receive a
cryptographic receipt, and verify later that the stored encrypted report has not
been modified. The project focuses on network anonymity, hybrid encryption,
HMAC receipts, Dijkstra relay routing, SQLite storage, and Merkle proofs.

## Scope

This version is web-interface only. Reports are entered through
`client/web/index.html`, encrypted in the browser with the Web Crypto API, then
sent to the Flask API. There is no alternate submission path in this project.

## Project Layout

```text
client/
  web/
    index.html
    verify.html
    crypto.js
server/
  app.py
  config.py
  crypto/
  routing/
  storage/
  anonymity/
  audit/
tests/
docs/
requirements.txt
```

## Setup

```bash
python -m venv .venv
.venv\Scripts\activate
python -m pip install -r requirements.txt
python server/app.py
```

Open `http://127.0.0.1:5000/` to submit a report, then use
`http://127.0.0.1:5000/verify` to verify the receipt. Organization reviewers
can use `http://127.0.0.1:5000/admin` with the admin token.

Default demo admin token:

```text
sentinel-admin-dev-token
```

## Demo Flow

1. Start the server with `python server/app.py`.
2. Submit a report from the browser.
3. Copy the 64-character `report_id`.
4. Open the admin dashboard and load reports with the admin token.
5. Open the complaint to review its decrypted content and integrity status.
6. Verify the receipt on the verification screen.
7. Modify the stored blob in SQLite for a tamper demo.
8. Verify again and observe `TAMPERED`.

## Tests

```bash
python -m pytest
```
