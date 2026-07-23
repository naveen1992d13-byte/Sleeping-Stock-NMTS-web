# Gmail App Password setup

1. Use (or create) a Gmail account for sending, e.g. `sleepingstock@gmail.com`.
2. Turn on 2-Step Verification: https://myaccount.google.com/security → "2-Step Verification".
   An App Password cannot be created until this is on.
3. Go to https://myaccount.google.com/apppasswords (or Security → "2-Step Verification" →
   "App passwords" if the direct link doesn't work for your account).
4. Choose app "Mail", device "Other (Custom name)" → enter e.g. `Sleeping Stock NMTS`.
5. Google shows a 16-character password (four groups of four). Copy it — it's shown once.
6. In your `.env` file:
   ```
   GMAIL_SMTP_HOST=smtp.gmail.com
   GMAIL_SMTP_PORT=587
   GMAIL_SMTP_USERNAME=sleepingstock@gmail.com
   GMAIL_SMTP_APP_PASSWORD=xxxxxxxxxxxxxxxx   # the 16-character App Password, no spaces
   GMAIL_SENDER_NAME=Sleeping Stock - NMTS
   ```
   (If your deployment already uses `SMTP_EMAIL` / `SMTP_PASSWORD` / `SMTP_HOST` / `SMTP_PORT` /
   `SMTP_FROM_NAME` instead, those work too — `notifications.py` checks the `GMAIL_SMTP_*` names
   first and falls back to these automatically.)
7. Restart the backend. Do **not** commit the real `.env` file.
8. Never use your normal Gmail account password here — only an App Password. If sending fails
   with an authentication error, regenerate the App Password and update `.env`.
