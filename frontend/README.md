# Eluno AI OMS - Frontend

React + TypeScript + Vite frontend for the Eluno AI Order Management System.

## Prerequisites

- Node.js 16+
- npm or yarn

## Setup

1. Install dependencies:
```bash
npm install
```

2. Create `.env` file:
```env
VITE_API_URL=http://localhost:8000/api
```

## Development

Run development server:
```bash
npm run dev
```

Access at: `http://localhost:3000`

## Build for Production

```bash
npm run build
```

Output in `dist/` folder.

## Features

- **Orders Management**: Create and track orders through all stages
- **Inventory Dashboard**: Monitor lens stock levels
- **Predictions**: View ML-based breach predictions
- **Alerts**: Real-time notifications for at-risk orders
- **AI Recommendations**: Get intelligent remediation suggestions

## Project Structure

```
frontend/
├── src/
│   ├── components/       # React components
│   │   ├── OrdersTab.tsx
│   │   ├── InventoryTab.tsx
│   │   ├── PredictionsTab.tsx
│   │   ├── AlertsTab.tsx
│   │   ├── Header.tsx
│   │   └── Sidebar.tsx
│   ├── config/          # Configuration
│   │   └── api.ts       # API endpoints
│   ├── App.tsx          # Main app component
│   ├── main.tsx         # Entry point
│   ├── types.ts         # TypeScript types
│   └── index.css        # Global styles
├── index.html           # HTML template
├── package.json         # Dependencies
├── tsconfig.json        # TypeScript config
└── vite.config.ts       # Vite config
```

## Environment Variables

- `VITE_API_URL`: Backend API URL (default: http://localhost:8000/api)

## Tech Stack

- React 19
- TypeScript
- Vite
- Tailwind CSS
- Lucide Icons
- Motion (animations)
