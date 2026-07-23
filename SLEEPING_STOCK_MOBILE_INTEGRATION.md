# Sleeping Stock Mobile Integration

## Setup
1. Backend: create a virtual environment, install `backend/requirements.txt`, copy `backend/.env.example` to `.env`, configure MongoDB and secrets, then run `uvicorn server:socket_app --host 0.0.0.0 --port 8000` from `backend`.
2. Frontend: copy `frontend/.env`, set `REACT_APP_BACKEND_URL`, run `npm ci`, then `npm run build`.
3. MongoDB indexes are created during backend startup by `ensure_mobile_indexes`.

## Web management
Open **Sleeping Stock Mobile** from the existing sidebar. The final route is `/sleeping-stock-mobile`; `/nmts-mobile` redirects to it. Always select an exact Branch before creating a pairing code. A normal User is automatically locked to the assigned Branch.

## Mobile API
Production mobile endpoints are under `/api/mobile/v2`: users, pairing, devices, session validation, push-token registration, configuration/version, request notifications, accept/skip/part response, verification/history, and single/multiple stock search.

## Pairing
Create a mobile user, retain the one-time temporary password securely, generate a pairing code, and complete pairing within ten minutes. The code is consumed atomically. The device receives a random session token; only its SHA-256 hash is stored. Mobile APIs derive Brand/Dealer/Branch from that device session.

## APK/version release
Store approved APKs outside the public frontend folder. Add a `mobile_app_versions` record through the Master Admin API with semantic `version_name`, increasing integer `version_code`, filename/path, release notes, minimum version and mandatory-update flag. Serve downloads only through an authenticated reverse-proxy/backend route in production.

## Production notes
Configure HTTPS, strict CORS, a strong `SECRET_KEY`, MongoDB authentication, FCM credentials, rate limiting at the reverse proxy, log rotation, backups, and an Android release keystore kept outside source control. Never commit the keystore or production `.env`.
