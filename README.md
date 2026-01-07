# Keyword Autocomplete Tool

A powerful SEO tool for discovering long-tail keyword opportunities by leveraging Google's Autocomplete suggestions.

## Features

### Core Functionality
- **Google Autocomplete**: Free keyword suggestions from Google
- **Bulk Seed Processing**: Process multiple seed keywords simultaneously
- **Real-time Updates**: See keywords appear incrementally while scraping
- **Multi-threading**: Configurable worker threads (1-20) for faster processing
- **Smart Cancellation**: Stop harvesting anytime with immediate response
- **Retry Mechanism**: Automatic retry with exponential backoff for failed requests

### Modifiers
- **A-Z Alphabet**: Append each letter (a-z) to seed keywords
- **Numbers (0-9)**: Numeric variations
- **Prepositions**: for, with, without, in, near, at, on
- **Comparisons**: vs, or, versus, like, similar to
- **Intent Keywords**: best, top, cheap, review, guide, free
- **Questions**: how to, what is, why, where, can, does, will

### Filtering
- **Include/Exclude**: Filter by specific text
- **Word Count**: Set min/max word count
- **Duplicate Removal**: Case-insensitive duplicate filtering
- **Special Characters**: Filter non-alphanumeric keywords
- **Filter Libraries**: Create reusable word exclusion lists
- **Topic Extraction**: Auto-generate topics from harvested keywords

### Export
- CSV (full data)
- TXT (keyword list)
- Clipboard copy

## Installation

### Prerequisites
- Python 3.8+
- pip

### Setup

1. **Clone and navigate**
   ```bash
   git clone https://github.com/FassihFayyaz/keyword-autocomplete-tool.git
   cd keyword-autocomplete-tool
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure (optional)**

   Create `.env` file for proxy settings:
   ```env
   # Proxy for better performance (optional)
   GOOGLE_HTTP_PROXY=http://proxy.example.com:8080
   GOOGLE_REQUEST_DELAY=0.3
   ```

4. **Run**
   ```bash
   python app.py
   ```

5. **Open browser**
   ```
   http://localhost:5000
   ```

## Usage

### Basic Workflow

1. **Enter Seeds**: Type seed keywords (one per line)
2. **Select Modifiers**: Enable desired variations
3. **Set Workers**: Choose thread count (1-20, default 5)
4. **Start Harvesting**: Click button and watch real-time results
5. **Filter**: Apply filters to refine results
6. **Export**: CSV, TXT, or copy to clipboard

### Filter Libraries
Create reusable exclusion lists:
1. Click "Manage Libraries"
2. Create library (e.g., "Brands" with competitor names)
3. Select libraries to exclude those terms

### Inline Editing
Edit libraries directly in the UI:
1. Click "Edit" on any library
2. Modify name or words
3. Save or Cancel

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Main application |
| `/api/harvest` | POST | Start harvesting (SSE stream) |
| `/api/filter` | POST | Apply filters |
| `/api/topics` | POST | Extract topics |
| `/api/export/csv` | POST | Export CSV |
| `/api/export/txt` | POST | Export TXT |
| `/api/import` | POST | Import keywords |
| `/api/libraries` | GET | Get libraries |
| `/api/libraries` | POST | Create/update library |
| `/api/libraries/<name>` | DELETE | Delete library |

## Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `FLASK_PORT` | 5000 | Application port |
| `GOOGLE_REQUEST_DELAY` | 0.3 | Delay between requests (seconds) |
| `GOOGLE_HTTP_PROXY` | - | HTTP proxy for requests |

### Proxy Setup

**Option 1: proxies.txt**
```
142.111.48.253:7030:username:password
192.168.1.1:8080:user:pass
```

**Option 2: Environment variables**
```env
GOOGLE_HTTP_PROXY=http://proxy.example.com:8080
```

## Project Structure

```
keyword-autocomplete-tool/
├── app.py              # Flask backend
├── index.html          # Frontend SPA
├── requirements.txt    # Dependencies
├── .env.example        # Config template
├── README.md           # This file
├── ROADMAP.md          # Future plans
└── libraries.json      # Stored libraries (auto-generated)
```

## License

MIT License - see LICENSE file for details.

## Author

**Fassih Fayyaz**
