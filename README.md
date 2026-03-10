# Issue Tracker API

A simple REST API for tracking issues built with FastAPI. This application provides CRUD operations for managing issues with support for status tracking and priority levels.

## Features

- **CRUD Operations**: Create, read, update, and delete issues
- **Status Management**: Track issues through open, in_progress, and closed states
- **Priority Levels**: Assign low, medium, or high priority to issues
- **Request Timing**: Built-in middleware to monitor API response times
- **CORS Support**: Configured for cross-origin requests
- **JSON Storage**: Simple file-based data persistence

## Tech Stack

- **Framework**: FastAPI
- **Data Validation**: Pydantic
- **Storage**: JSON file-based storage
- **Server**: Uvicorn

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd fastapi-issue-tracker2
```

2. Create a virtual environment:
```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Usage

### Running the Server

Start the development server:
```bash
uvicorn main:app --reload
```

The API will be available at `http://localhost:8000`

### API Documentation

Once the server is running, access the interactive documentation:
- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/issues/` | Get all issues |
| POST | `/api/v1/issues/` | Create a new issue |
| GET | `/api/v1/issues/{issue_id}` | Get a specific issue |
| PUT | `/api/v1/issues/{issue_id}` | Update an issue |
| DELETE | `/api/v1/issues/{issue_id}` | Delete an issue |

### Request/Response Examples

**Create Issue:**
```bash
curl -X POST "http://localhost:8000/api/v1/issues/" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Fix authentication bug",
    "description": "Users cannot login with valid credentials",
    "priority": "high"
  }'
```

**Update Issue:**
```bash
curl -X PUT "http://localhost:8000/api/v1/issues/{issue_id}" \
  -H "Content-Type: application/json" \
  -d '{
    "status": "in_progress"
  }'
```

## Data Models

### Issue Schema

| Field | Type | Description |
|-------|------|-------------|
| id | string | Unique identifier (UUID) |
| title | string | Issue title (3-100 characters) |
| description | string | Detailed description (5-1000 characters) |
| priority | enum | low, medium, high |
| status | enum | open, in_progress, closed |

### Priority Levels
- `low`: Low priority issue
- `medium`: Medium priority issue (default)
- `high`: High priority issue

### Status States
- `open`: Issue is open and awaiting work
- `in_progress`: Issue is currently being worked on
- `closed`: Issue has been resolved

## Project Structure

```
.
├── app/
│   ├── routes/
│   │   └── issues.py       # Issue API endpoints
│   ├── middleware/
│   │   └── timer.py        # Request timing middleware
│   ├── schemas.py          # Pydantic models
│   └── storage.py          # JSON file storage utilities
├── data/                   # Data storage directory
├── main.py                 # Application entry point
├── requirements.txt        # Python dependencies
└── README.md              # This file
```

## Configuration

- Data is stored in `data/issues.json`
- CORS is configured to allow all origins (suitable for development)
- Request processing time is added to response headers as `X-Process-Time`

## Development

The application uses:
- **FastAPI** for the web framework
- **Pydantic** for data validation and serialization
- **Uvicorn** as the ASGI server
- File-based JSON storage for simplicity

## License

[Add your license here]
