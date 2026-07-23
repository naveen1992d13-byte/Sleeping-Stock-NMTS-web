# Sleeping Stock — powered by NMTS (Non Moving Tracking System)

**Track Smart. Move Faster. Reduce Dead Stock.**

An automotive spare-parts inventory platform for tracking stock, flagging
non-moving ("sleeping") inventory, managing purchase/sales orders, and
running warehouse operations across brands, groups, and locations.

## Stack

- **Frontend:** React (CRA + craco), Tailwind CSS, shadcn/ui components
- **Backend:** FastAPI, MongoDB (Motor/PyMongo), Socket.IO for live notifications
- **Auth:** JWT (python-jose) with bcrypt password hashing, role-based
  permissions (master / admin / user)

## Project Structure

```
nmts/
├── backend/
│   ├── server.py          # FastAPI app (routes, models, business logic)
│   ├── requirements.txt
│   ├── tests/             # API test suite
│   └── .env               # MONGO_URL, DB_NAME, SECRET_KEY, CORS_ORIGINS
└── frontend/
    ├── src/
    │   ├── pages/          # Dashboard, Products, Orders, Users, Reports, etc.
    │   ├── components/ui/  # shadcn/ui primitives
    │   └── index.css       # Emerald/Grey theme tokens
    └── .env                # REACT_APP_BACKEND_URL
```

## Getting Started

**Backend**
```bash
cd backend
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
# edit .env with your MongoDB connection details
uvicorn server:app --reload --port 8000
```

**Frontend**
```bash
cd frontend
npm install
npm start
```

## Theme

Emerald green / grey / white / dark grey enterprise palette, defined in
`frontend/tailwind.config.js` (`emerald` and `graphite` color scales) and
`frontend/src/index.css`.

## Notes

- On first run, use `POST /api/init` (see `server.py`) to bootstrap the
  first master admin account, then change its password immediately —
  the seeded credentials are for initial setup only.
