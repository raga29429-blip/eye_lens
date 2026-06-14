# Eluno AI OMS - Backend

Python FastAPI backend for the Eluno AI Order Management System.

## Prerequisites

- Python 3.11+
- pip

## Setup

1. Create virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Create `.env` file:
```env
DATABASE_URL=sqlite:///./eluno_oms.db
GEMINI_API_KEY=your_gemini_api_key
ENVIRONMENT=development
```

## Development

Run development server:
```bash
python main.py
```

Access at: `http://localhost:8000`

API Documentation: `http://localhost:8000/docs`

## Database

Uses SQLite for development, PostgreSQL for production.

Initialize database:
```bash
python seed_data.py
```

## API Endpoints

- `GET /api/inventory` - Get all inventory
- `POST /api/inventory` - Create inventory item
- `GET /api/orders` - Get all orders
- `POST /api/orders` - Create order
- `PUT /api/orders/:id/stage` - Update order stage
- `GET /api/alerts` - Get all alerts
- `GET /api/dashboard/metrics` - Get dashboard metrics
- `GET /api/model-metrics` - Get ML model metrics
- `POST /api/model/retrain` - Retrain ML model
- `POST /api/recommendations` - Get AI recommendations

## Project Structure

```
backend/
├── routers/              # API route handlers
│   ├── inventory.py
│   ├── orders.py
│   ├── alerts.py
│   ├── metrics.py
│   ├── ml_model.py
│   └── recommendations.py
├── services/             # Business logic
│   ├── inventory_manager.py
│   ├── order_lifecycle_manager.py
│   ├── prediction_engine.py
│   ├── alert_manager.py
│   ├── dashboard_service.py
│   └── gemini_integration.py
├── main.py              # Application entry point
├── database.py          # Database configuration
├── models.py            # SQLAlchemy models
├── schemas.py           # Pydantic schemas
├── seed_data.py         # Database seeding
└── requirements.txt     # Python dependencies
```

## Environment Variables

- `DATABASE_URL`: Database connection string
- `GEMINI_API_KEY`: Google Gemini API key for AI recommendations
- `ENVIRONMENT`: development/production
- `PORT`: Server port (default: 8000)

Optional (Email alerts):
- `SMTP_HOST`, `SMTP_PORT`, `SMTP_USERNAME`, `SMTP_PASSWORD`

Optional (WhatsApp alerts):
- `TWILIO_ACCOUNT_SID`, `TWILIO_AUTH_TOKEN`, `TWILIO_WHATSAPP_FROM`

## Tech Stack

- FastAPI
- SQLAlchemy
- PostgreSQL/SQLite
- Scikit-learn (ML)
- Google Generative AI
- Twilio (WhatsApp)
- Uvicorn (ASGI server)
