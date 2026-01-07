# Keyword Autocomplete Tool

A powerful SEO tool for discovering long-tail keyword opportunities by leveraging Google's Autocomplete suggestions and DataForSEO API.

![Keyword Finder](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Flask](https://img.shields.io/badge/Flask-3.1.0-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

## Features

### Core Functionality
- **Dual API Support**: Choose between Google Autocomplete (free, rate-limited) or DataForSEO (paid, reliable)
- **Bulk Seed Processing**: Process multiple seed keywords simultaneously
- **Real-time Progress Tracking**: Live updates with ETA, query count, and results
- **Smart Modifiers**: Generate keyword variations using multiple strategies

### Modifiers
- **A-Z Alphabet Soup**: Appends each letter (a-z) to seed keywords
- **Numbers (0-9)**: Appends digits for numeric variations
- **Prepositions**: Adds common prepositions (for, with, without, in, near, at, on)
- **Comparisons**: Adds comparison terms (vs, or, versus, like, similar to)
- **Intent Keywords**: Adds intent qualifiers (best, top, cheap, review, guide, free)
- **Questions**: Prepends question words (how to, what is, why, where, can, does, will)

### Filtering & Analysis
- **Include/Exclude Filters**: Filter keywords by specific text
- **Word Count Filters**: Set min/max word count for long-tail discovery
- **Topic Extraction**: Auto-generate topics from harvested keywords using n-gram analysis
- **Filter Libraries**: Create reusable word libraries to exclude (e.g., brands, locations)

### Export Options
- **CSV Export**: Full data with keyword, source, character count, word count
- **TXT Export**: Simple keyword list
- **Clipboard Copy**: Quick copy for pasting into other tools
- **Import**: Import existing keyword lists (CSV, TXT, Excel)

## Installation

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)

### Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/FassihFayyaz/keyword-autocomplete-tool.git
   cd keyword-autocomplete-tool
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure environment variables**

   Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```

   Edit `.env` with your settings:
   ```env
   # DataForSEO (optional - only if using paid API)
   DATAFORSEO_API_LOGIN=your_api_login
   DATAFORSEO_API_PASSWORD=your_api_password

   # Proxy settings for Google API (optional)
   GOOGLE_REQUEST_DELAY=0.3
   ```

4. **Run the application**
   ```bash
   python app.py
   ```

5. **Open in browser**
   ```
   http://localhost:5000
   ```

## Usage

### Basic Workflow

1. **Enter Seed Keywords**
   - Type one or more seed keywords (one per line for bulk)
   - Example: `coffee maker`, `espresso machine`

2. **Select Data Source**
   - **Google Autocomplete (Free)**: Rate-limited but no cost
   - **DataForSEO (Paid)**: Requires credentials, more reliable

3. **Choose Modifiers**
   - Enable/disable modifiers based on your needs
   - More modifiers = more queries = more keywords

4. **Start Harvesting**
   - Click "Start Harvesting" to begin
   - Monitor real-time progress and results

5. **Filter Results**
   - Use include/exclude filters
   - Set word count ranges
   - Apply library filters
   - Extract topics for analysis

6. **Export**
   - Copy to clipboard
   - Export as CSV/TXT
   - Import into your SEO tools

### Advanced Features

#### Filter Libraries
Create reusable word libraries to exclude specific terms:
1. Click "Manage Libraries"
2. Create a library (e.g., "Brands" with competitor names)
3. Select libraries to exclude those keywords from results

#### Topic Extraction
1. Harvest keywords first
2. Click "Generate Topics"
3. Click topics to filter keywords containing those terms
4. Use the eye icon to hide/show specific topics

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Main application page |
| `/api/harvest` | POST | Start keyword harvesting (SSE stream) |
| `/api/filter` | POST | Apply filters to keywords |
| `/api/topics` | POST | Extract topics from keywords |
| `/api/export/csv` | POST | Export keywords as CSV |
| `/api/export/txt` | POST | Export keywords as TXT |
| `/api/import` | POST | Import keywords from file |
| `/api/libraries` | GET | Get all libraries |
| `/api/libraries` | POST | Create/update library |
| `/api/libraries/<name>` | DELETE | Delete library |

## Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `FLASK_PORT` | 5000 | Application port |
| `FLASK_DEBUG` | true | Debug mode |
| `GOOGLE_REQUEST_DELAY` | 0.3 | Delay between Google API requests (seconds) |
| `DATAFORSEO_API_LOGIN` | - | DataForSO API login |
| `DATAFORSEO_API_PASSWORD` | - | DataForSEO API password |
| `GOOGLE_HTTP_PROXY` | - | HTTP proxy for Google API |
| `GOOGLE_HTTPS_PROXY` | - | HTTPS proxy for Google API |

### Proxy Configuration

To avoid rate limiting with Google API, you can use proxies:

**Method 1: proxies.txt file** (Recommended)
```
142.111.48.253:7030:username:password
192.168.1.1:8080:user:pass
```

**Method 2: Environment variables**
```env
GOOGLE_HTTP_PROXY=http://proxy.example.com:8080
GOOGLE_HTTPS_PROXY=http://proxy.example.com:8080
```

## Project Structure

```
keyword-autocomplete-tool/
├── app.py              # Flask backend application
├── index.html          # Frontend single-page application
├── requirements.txt    # Python dependencies
├── .env.example        # Environment configuration template
├── .gitignore          # Git ignore rules
├── README.md           # This file
├── PRP.md              # Product Requirements Document
└── libraries.json      # Stored filter libraries (auto-generated)
```

## Technical Details

### KeywordHarvester Class

The core `KeywordHarvester` class handles:

- Query generation with modifiers
- API communication (Google/DataForSEO)
- Keyword cleaning and normalization
- Topic extraction using unigram analysis

### Server-Sent Events (SSE)

The application uses SSE for real-time progress updates:
- `init`: Initial query count
- `progress`: Progress updates during harvesting
- `seed_complete`: Individual seed completion
- `complete`: Final results

## Rate Limiting

### Google Autocomplete API
- **Recommended delay**: 0.3-0.5 seconds per request
- **Without proxy**: Risk of IP ban after ~100 requests
- **With proxy**: Can reduce delay to 0

### DataForSEO API
- No rate limiting concerns
- Requires paid account
- More reliable results

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License.

## Author

**Fassih Fayyaz**

## Acknowledgments

- Google Autocomplete API for the free suggestion service
- DataForSEO for the enterprise-grade API option
- Flask and the Python community for excellent tools
