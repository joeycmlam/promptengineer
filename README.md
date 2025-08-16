# promptengineer

A modern AI prompt engineering tool.

## Project Overview
This project is designed to help users create, test, and manage prompts for AI models efficiently.

## Features
- Prompt templates
- Versioning
- Testing and evaluation
- Extensible for multiple AI providers

## Tech Stack
- Python 3.11+
- FastAPI (for API/backend)
- Jinja2 (for templating)
- SQLite (default DB, can be swapped)
- Optional: React (for frontend, not included in initial scaffold)

## Getting Started

### 1. Clone the repository
```
git clone <repo-url>
cd promptengineer
```

### 2. Create a virtual environment
```
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies
```
pip install -r requirements.txt
```

### 4. Run the API server
```
uvicorn app.main:app --reload
```

## Folder Structure
- `app/` - Main FastAPI application
- `tests/` - Unit and integration tests
- `.github/` - Copilot and GitHub workflow instructions

## License
MIT
