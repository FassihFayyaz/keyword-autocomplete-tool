# Roadmap & Future Plans

## Priority Features

### High Priority

- [x] **Real-time Table Updates** ✅
  - Fill keyword table incrementally while scraping
  - Add results as they come in instead of waiting for completion
  - Show live keyword count updates
  - **Also implemented:** Immediate stop/cancellation functionality

- [ ] **Multi-threading / Worker Pool**
  - Add configurable number of workers for parallel processing
  - Make keyword finding as fast as possible
  - Add worker count setting in UI

- [ ] **Retry Mechanism**
  - Implement timeout detection (60 seconds per keyword)
  - Add automatic retry (up to 20 attempts) before stopping
  - Show retry status in progress UI

### Medium Priority

- [ ] **UI Improvements**
  - Fix results table height to match sidebar height
  - Improve responsive layout
  - Add loading skeleton states

- [ ] **Library Management**
  - Enable inline editing of library names
  - Enable inline editing of library words
  - Add bulk import for libraries
  - Add export for libraries

### Low Priority

- [ ] **Advanced Filtering**
  - Add duplicate keyword filtering (exact matches)
  - Add near-duplicate detection (similar keywords)
  - Add special characters filtering options
  - Add regex-based filtering

## Enhancement Ideas

### Performance

- [ ] **Caching Layer**
  - Cache results for repeated seed keywords
  - Implement TTL for cached results
  - Add cache statistics UI

- [ ] **Queue Management**
  - Pause/resume harvesting functionality
  - Save partial results for later recovery
  - Add progress persistence across sessions

### Features

- [ ] **Search Volume Integration**
  - Connect to keyword volume APIs
  - Display CPC data
  - Show keyword difficulty scores

- [ ] **SERP Data Enrichment**
  - Fetch search intent classification
  - Get featured snippet opportunities
  - Identify question-type keywords

- [ ] **Export Enhancements**
  - Add Excel (.xlsx) export
  - Add JSON export format
  - Add custom column selection

### Analytics

- [ ] **Keyword Clustering**
  - Group keywords by semantic similarity
  - Create topical clusters
  - Visual cluster representations

- [ ] **Competition Analysis**
  - Compare keywords across domains
  - Identify keyword gaps
  - Track keyword opportunities

### User Experience

- [ ] **Saved Projects**
  - Save harvesting sessions
  - Load previous sessions
  - Compare sessions side-by-side

- [ ] **Dark/Light Theme**
  - Toggle between themes
  - System theme detection
  - Custom theme colors

- [ ] **Keyboard Shortcuts**
  - Ctrl+Enter to start harvesting
  - Ctrl+E to export
  - Escape to cancel

## Technical Debt

### Code Quality

- [ ] Add type hints throughout codebase
- [ ] Add comprehensive unit tests
- [ ] Add integration tests for API endpoints
- [ ] Improve error handling and logging
- [ ] Add API rate limiting headers

### Security

- [ ] Add CSRF protection
- [ ] Implement request throttling
- [ ] Add input sanitization validation
- [ ] Secure proxy credentials storage
- [ ] Add authentication (optional)

### Documentation

- [ ] Add API documentation (Swagger/OpenAPI)
- [ ] Create contribution guidelines
- [ ] Add development setup guide
- [ ] Document proxy rotation strategy

## Bug Fixes

- [ ] Fix table scroll position on new results
- [ ] Handle empty library edge case
- [ ] Fix progress bar estimation accuracy
- [ ] Handle network errors gracefully
- [ ] Fix memory leak with large result sets

## Version History

### v1.1.0 (Planned)
- Real-time table updates
- Multi-threading support
- Retry mechanism

### v1.2.0 (Planned)
- Library editing improvements
- Advanced filtering
- UI enhancements

### v2.0.0 (Future)
- Search volume integration
- Keyword clustering
- Saved projects
- Analytics dashboard
