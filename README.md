# Universal Website Scraper MVP

A production-ready MVP for scraping websites with static HTML parsing and JavaScript rendering fallback.

## Features

- **Static HTML Scraping**: Fast initial fetch using httpx + BeautifulSoup
- **JavaScript Rendering**: Playwright fallback for dynamic content
- **Section Extraction**: Intelligent section detection and parsing
- **Interactions**: Click flows, scrolling, and pagination support
- **Noise Filtering**: Removes cookie banners, modals, and popups
- **JSON API**: RESTful API with exact response shape
- **Web Interface**: Simple, functional frontend for testing

## Setup Instructions

### Prerequisites

- Python 3.10 or higher
- Bash shell (for run.sh)

### Quick Start

1. Make run.sh executable:
   ```bash
   chmod +x run.sh
   ```

2. Run the application:
   ```bash
   ./run.sh
   ```

The script will:
- Create a virtual environment (if needed)
- Install all dependencies
- Install Playwright browsers
- Start the server on http://localhost:8000

### Manual Setup (Alternative)

If you prefer manual setup:

```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
playwright install chromium
python -m uvicorn app.main:app --host 0.0.0.0 --port 8000
```

## Usage

### Web Interface

1. Open http://localhost:8000 in your browser
2. Enter a URL in the input box
3. Click "Scrape"
4. View sections in the accordion interface
5. Download JSON result

### API Endpoints

#### Health Check
```bash
GET /healthz
```

Response:
```json
{"status": "ok"}
```

#### Scrape Website
```bash
POST /scrape
Content-Type: application/json

{
  "url": "https://example.com"
}
```

See `design_notes.md` for response structure details.

## Test URLs

The following URLs were used for testing:

1. **https://example.com** - Simple static site
2. **https://quotes.toscrape.com** - Static content with pagination
3. **https://scrapethissite.com/pages/** - Various scraping challenges

## Known Limitations

- **Playwright Browser Installation**: First run requires downloading Chromium (~150MB)
- **Timeout Handling**: Some slow-loading sites may timeout (30s default)
- **JavaScript Heavy Sites**: Very complex SPAs may require additional wait strategies
- **Rate Limiting**: No built-in rate limiting (be respectful to target sites)
- **Authentication**: Does not handle login-protected pages
- **CAPTCHA**: Cannot bypass CAPTCHA or bot detection

## Project Structure

```
.
├── app/
│   ├── main.py              # FastAPI application
│   ├── scraper/
│   │   ├── static.py        # Static HTML fetching
│   │   ├── js.py            # Playwright rendering
│   │   ├── sections.py      # Section extraction
│   │   ├── interactions.py  # Click/scroll detection
│   │   └── utils.py         # URL utilities
│   ├── templates/
│   │   └── index.html       # Frontend template
│   └── static/              # Static assets
├── run.sh                   # Run script
├── requirements.txt         # Python dependencies
├── README.md               # This file
├── design_notes.md         # Design decisions
└── capabilities.json       # Feature capabilities
```

## Technology Stack

- **Backend**: FastAPI, Python 3.10+
- **Scraping**: httpx, BeautifulSoup4, Playwright
- **Frontend**: Jinja2 templates
- **Server**: Uvicorn

## License

This project is part of the Lyftr AI Full-Stack Assignment.

