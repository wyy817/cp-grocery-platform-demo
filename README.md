# CP Group Fresh-Food Platform: Strategy Dashboard + Consumer App (Demo)

A full-stack demo platform for a fresh-food e-commerce market-entry case study on CP Group in China. It has two sides:

- **Strategy Dashboard** (login required): competitor analysis, market opportunities, market growth trends, customer personas and inventory, for strategy analysts and managers.
- **Consumer App** (public, English UI): product catalogue, farm-to-shelf traceability lookup and a simple cart / checkout flow.

Data comes from one curated spreadsheet (`backend/CP_Glide_Data_Master.xlsx`: competitors, products, traceability, market data, opportunities, personas). It was built as a demo, so this is a prototype rather than a production system.

## Tech stack

| Layer | Stack |
|---|---|
| Frontend | Vue 3, Vite, Vue Router, Pinia, Element Plus, ECharts (vue-echarts), Axios |
| Backend | FastAPI, pandas / openpyxl (spreadsheet data), JWT auth (python-jose, passlib) |
| Deployment configs | Vercel (frontend), Railway (backend) |

## Roles

Role-based access (`ADMIN`, `ANALYST`, `CONSUMER`) is enforced with JWT. Demo accounts for local use: `admin / admin123`, `analyst / analyst123`, `consumer / consumer123`.

## API

| Endpoint | Auth |
|---|---|
| `POST /api/v1/auth/login` | none |
| `GET /api/v1/competitors`, `/products`, `/products/{id}/traceability`, `/market-data`, `/opportunities`, `/personas` | none (demo) |
| `GET /api/v1/inventory` | analyst or above |
| `GET /api/v1/health` | none |

## Run locally

```bash
# backend
cd backend
pip install -r requirements.txt
uvicorn main:app --reload --port 8000

# frontend (new terminal)
cd frontend
npm install
npm run dev        # proxies /api to http://localhost:8000
```

Environment variables:

- `JWT_SECRET` (backend): set a random value outside local demos
- `VITE_API_BASE_URL` (frontend build): URL of the deployed backend

## Docs

`docs/SRS.md` is the original requirements specification draft. It was written before implementation and lists Spring Boot as the backend; the implementation here uses FastAPI.
