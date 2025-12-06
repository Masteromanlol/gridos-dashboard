# GridOS Real-Time Dashboard

🔋 **Real-time power grid monitoring dashboard with HPC cluster integration via Globus**

Connects PEGASE 9241 grid data and GNN-PINN contingency analysis model to an interactive web interface.

## 🎯 Features

- **Real-Time Data Visualization**: Plotly-powered interactive charts
- **HPC Integration**: Globus SDK for seamless data transfer from cluster
- **GNN-PINN Analysis**: Graph Neural Network + Physics-Informed Neural Network for contingency prediction
- **FastAPI Backend**: High-performance async REST API
- **Modern Frontend**: Responsive HTML/CSS/JS dashboard

## 📁 Project Structure

```
gridos-dashboard/
├── frontend/
│   └── index.html          # Web dashboard interface
├── backend/
│   ├── main.py             # FastAPI server
│   ├── requirements.txt    # Python dependencies
│   └── README.md          # Backend docs
└── README.md              # This file
```

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- Node.js (optional, for advanced frontend features)
- Globus account ([Sign up](https://www.globus.org/))

### Backend Setup

```bash
# Clone the repository
git clone https://github.com/Masteromanlol/gridos-dashboard.git
cd gridos-dashboard/backend

# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up Globus credentials
export GLOBUS_CLIENT_ID="your-client-id"
export GLOBUS_CLIENT_SECRET="your-client-secret"
export GLOBUS_ENDPOINT_ID="your-hpc-endpoint-id"

# Run the server
python main.py
```

Server will start at `http://localhost:8000`

### Frontend Access

**Option 1: Via Backend** (Recommended for local dev)
- Open browser to `http://localhost:8000`
- Backend serves frontend automatically

**Option 2: GitHub Pages** (For production)
- Frontend hosted at: `https://masteromanlol.github.io/gridos-dashboard/`
- Configure CORS in backend for cross-origin requests

## 🌐 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Serve frontend HTML |
| `/api/health` | GET | Health check |
| `/api/grid-data` | GET | Fetch latest grid data from HPC |
| `/api/analyze` | POST | Run GNN-PINN contingency analysis |
| `/api/model-status` | GET | Get model metadata |

## 🔧 Globus Setup

### 1. Register Globus Application

1. Go to [Globus Developers](https://developers.globus.org/)
2. Create a new app
3. Note your `Client ID` and `Client Secret`

### 2. Find Your HPC Endpoint

```bash
# Install Globus CLI
pip install globus-cli

# Login
globus login

# List available endpoints
globus endpoint search "your-institution"
```

### 3. Configure Environment

Create `.env` file in `backend/`:

```bash
GLOBUS_CLIENT_ID=your-client-id-here
GLOBUS_CLIENT_SECRET=your-secret-here
GLOBUS_ENDPOINT_ID=your-endpoint-uuid
```

## 📊 Data Flow

```
HPC Cluster (PEGASE 9241 Data)
    ↓ (Globus Transfer)
Backend API (FastAPI)
    ↓ (REST API)
Frontend Dashboard (HTML/JS)
    ↓ (Plotly)
Interactive Visualization
```

## 🧠 GNN-PINN Model

The backend integrates a Graph Neural Network + Physics-Informed Neural Network for power grid contingency analysis:

- **Input**: Real-time grid topology and power flow
- **Output**: Contingency predictions, risk scores, stability metrics
- **Architecture**: Custom PyTorch implementation

## 🎨 Frontend Features

- Dark theme with gradient background
- Real-time chart updates
- Refresh data button
- Run analysis trigger
- Status indicators
- Responsive design

## 🛠️ Development

### Run Tests
```bash
pytest backend/tests/
```

### Hot Reload
```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

## 📝 Configuration

### Backend Port
Edit `main.py`, line 197:
```python
uvicorn.run(app, host="0.0.0.0", port=8000)
```

### CORS Origins
For production, edit `main.py`, line 35:
```python
allow_origins=["https://your-frontend-domain.com"]
```

## 🚨 Troubleshooting

**Issue**: `ModuleNotFoundError: No module named 'fastapi'`
- **Solution**: Activate venv and run `pip install -r requirements.txt`

**Issue**: `Globus authentication failed`
- **Solution**: Check your `GLOBUS_CLIENT_ID` and `GLOBUS_CLIENT_SECRET` environment variables

**Issue**: `CORS error in browser`
- **Solution**: Add your frontend URL to `allow_origins` in `main.py`

## 📦 Dependencies

### Backend
- FastAPI 0.104.1
- Uvicorn 0.24.0  
- PyTorch 2.1.0
- Globus SDK 3.34.0
- NumPy, Pandas

### Frontend
- Plotly.js (CDN)
- Axios (CDN)

## 🎓 Research Context

This dashboard is part of ongoing research at the University of Colorado Boulder on applying Graph Neural Networks and Physics-Informed Neural Networks to power grid contingency analysis.

## 📄 License

MIT License - See LICENSE file for details

## 🤝 Contributing

Pull requests welcome! For major changes, please open an issue first.

## 📞 Contact

- **Repository**: [github.com/Masteromanlol/gridos-dashboard](https://github.com/Masteromanlol/gridos-dashboard)
- **Issues**: [Report a bug](https://github.com/Masteromanlol/gridos-dashboard/issues)

---

**Built with** ⚡ by [Roman Pouw](https://github.com/Masteromanlol) | University of Colorado Boulder
