# Eluno AI Order Management System

An intelligent fulfillment platform for eyewear production with predictive machine learning capabilities.

## 🎯 Overview

The Eluno AI OMS optimizes eyewear production by integrating rule-based inventory management with predictive machine learning to proactively identify SLA breaches before they occur.

## 📁 Project Structure

```
eye_lens/
├── backend/              # Python FastAPI backend
│   ├── routers/         # API endpoints
│   ├── services/        # Business logic
│   ├── main.py          # Entry point
│   ├── requirements.txt # Python dependencies
│   └── README.md        # Backend documentation
├── frontend/            # React TypeScript frontend
│   ├── src/            # Source code
│   ├── package.json    # Node dependencies
│   └── README.md       # Frontend documentation
├── docs/               # Documentation
│   ├── DEPLOYMENT.md   # Multi-platform deployment guide
│   ├── RAILWAY_SETUP.md # Railway-specific guide
│   └── RENDER_SETUP.md  # Render-specific guide
└── README.md           # This file
```

## ✨ Features

- **Inventory Management**: Track lens types, prescriptions, and stock levels
- **Order Lifecycle Tracking**: Monitor orders through all production stages
- **ML-Based Breach Prediction**: Predict SLA violations before they occur
- **Alert System**: Automated notifications for high-risk orders
- **AI Recommendations**: Get intelligent remediation suggestions from Google Gemini
- **Real-time Dashboard**: Monitor KPIs and order status

## 🚀 Quick Start

### Backend Setup

```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
python main.py
```

Backend runs on: `http://localhost:8000`

### Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

Frontend runs on: `http://localhost:3000`

See individual README files in `backend/` and `frontend/` for detailed instructions.

## 🛠️ Tech Stack

**Backend:**
- Python 3.11
- FastAPI
- SQLAlchemy
- PostgreSQL/SQLite
- Scikit-learn
- Google Gemini AI

**Frontend:**
- React 19
- TypeScript
- Vite
- Tailwind CSS

## 📦 Deployment

Multiple deployment options available:

- **Railway**: All-in-one platform (recommended for beginners)
- **Render**: Free tier with PostgreSQL
- **Vercel + Render**: Frontend on Vercel, Backend on Render
- **Docker**: Self-hosted with Docker Compose

See `docs/DEPLOYMENT.md` for complete deployment guides.

## 📊 ML Model

The system uses a trained Random Forest model for TAT breach prediction:
- Model file: `order_breach_model (1).pkl`
- Features: Order stage, lens type, stock status, prescription complexity
- Predicts breach probability (0-100%)
- Risk classification: Low (<30%), Medium (30-70%), High (>70%)

## 🔐 Environment Variables

**Backend (.env):**
```env
DATABASE_URL=sqlite:///./eluno_oms.db
GEMINI_API_KEY=your_api_key
ENVIRONMENT=development
```

**Frontend (.env):**
```env
VITE_API_URL=http://localhost:8000/api
```

## 📚 Documentation

- **Backend API**: `http://localhost:8000/docs` (when running)
- **Deployment Guides**: See `docs/` folder
- **Component Docs**: See individual README files

## 🧪 Testing

Backend API integration tests:
```bash
python test_api_integration.py
```

## 📝 License

MIT

## 🤝 Contributing

This is a project for eyewear fulfillment optimization. For questions or contributions, please open an issue.

---

**Status**: Production Ready ✅

**Live Demo**: [Your deployed URL]

**Repository**: https://github.com/raga29429-blip/eye_lens
