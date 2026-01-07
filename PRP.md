📋 Product Requirements Document (PRD): Keyword Finder Module

1. Executive Summary

The Keyword Finder is a specialized tool designed to mine "long-tail" keyword opportunities by leveraging Google's Autocomplete suggestions. It simulates the behavior of a user typing a query and capturing the predictions (e.g., "Coffee a...", "Coffee b..."), providing a massive list of relevant search terms often hidden from standard volume tools.

2. User User Stories

As a SEO Specialist, I want to input a seed keyword (e.g., "dog training") and get hundreds of specific questions and variations so I can find low-competition topics.

As a Content Writer, I want to filter out specific brand names (e.g., "Petco") from the results so I can focus on general informational intent.

As an Analyst, I want to export the final cleaned list to CSV to import it into my rank tracker.

3. Functional Requirements

3.1 Input Module

Seed Keyword Field: Text input for the main term.

Modifier Settings:

Alphabet Soup (A-Z): Appends letters 'a' through 'z' to the seed (e.g., "seed a", "seed b").

Numbers (0-9): Appends numbers.

Prepositions: Appends "for", "with", "without", "in", "near".

Comparisons: Appends "vs", "or", "versus", "like".

Intent/Qualifiers: Prepend/Append "best", "top", "cheap", "review", "guide".

Questions: Prepend "how to", "what is", "why", "can".

Depth Level:

Level 1: Seed + [Modifier]

Level 2: (Seed + [Modifier]) + [a-z] (Recursive - Warning: Exponential request growth).

3.2 Data Retrieval (The Engine)

The system must support two modes of data retrieval:

Option A: Unofficial Google Suggest API (Cost: Free / High Risk)

Endpoint: http://google.com/complete/search?client=chrome&q={query}

Pros: Free, extremely fast.

Cons: High risk of IP ban (429 Too Many Requests). Requires robust proxy rotation.

Implementation: Backend proxy required to avoid CORS errors.

Option B: DataForSEO Autocomplete API (Cost: Paid / Low Risk)

Task Post Endpoint: v3/serp/google/autocomplete/task_post

Action: Submits the keyword to the queue.

Task Get Endpoint: v3/serp/google/autocomplete/task_get/{task_id}

Action: Retrieves the results once the status is "Completed".

Documentation: DataForSEO Autocomplete Docs

Pros: Enterprise stability, no IP ban risk, location-specific results.

Cons: Costs money per task.

Implementation: Asynchronous queue (Task Post -> Task Get).

Recommendation: Use Option A for "Quick Preview" (limits apply) and Option B for "Full Harvest".

3.3 Keyword Cleaning & Processing

Before displaying results, the raw list must undergo:

Deduplication: Remove exact duplicates.

Sanitization: Remove non-ASCII characters if necessary.

Normalization: Convert all to lowercase for comparison.

3.4 Filtering & Manipulation

Include Filter: Only show keywords containing specific substrings (e.g., "free").

Exclude Filter: Hide keywords containing specific substrings (e.g., "near me", "reddit", "craigslist").

Word Count Filter: Min/Max number of words (e.g., Min: 3 to find long-tail).

3.5 Export

Formats: CSV, Excel (.xlsx), Clipboard copy.

Columns: Keyword, Source (e.g., "seed + a"), Character Count, Word Count.

4. User Workflow Timeline

This section details the chronological steps a user takes to complete a harvesting session.

Setup Phase (0s - 10s):

User enters seed keyword (e.g., "iphone 15 cases").

User toggles modifiers (e.g., checks "Questions" and "Comparisons", unchecks "A-Z").

User selects Data Source (Free Preview vs. DataForSEO).

Harvesting Phase (10s - 60s+):

User clicks "Start Harvesting".

System generates query list based on selected modifiers (e.g., "iphone 15 cases vs", "best iphone 15 cases").

Real-time Feedback: The results table begins populating immediately as parallel requests complete.

Status bar updates: "Processed 15/50 queries... Found 230 keywords."

Refinement Phase (Post-Harvest):

User reviews the raw list of 500+ keywords.

User types "amazon" or "ebay" in the Exclude Filter to remove e-commerce intent.

User sets Min Word Count to 4 to filter out generic short-tail terms.

Export Phase:

User clicks "Export CSV".

File downloads containing the final, filtered list of 350 keywords, ready for volume analysis.

5. Technical Specifications

5.1 "Alphabet Soup" Algorithm Logic

The system shall generate queries based on the user's selected modifiers.

seed = "camping coffee"
variations = []

# 1. Standard A-Z
alphabet = "abcdefghijklmnopqrstuvwxyz"
for letter in alphabet:
    variations.append(f"{seed} {letter}") 
    # Result: "camping coffee a", "camping coffee b"...

# 2. Comparisons
comparisons = ["vs", "versus", "or", "like", "similar to"]
for comp in comparisons:
    variations.append(f"{seed} {comp}")
    # Result: "camping coffee vs", "camping coffee or"...

# 3. Intent & Qualifiers
intents = ["best", "top", "cheap", "review", "2024"]
for intent in intents:
    variations.append(f"{intent} {seed}")
    variations.append(f"{seed} {intent}")
    # Result: "best camping coffee", "camping coffee review"...

# 4. Questions
questions = ["how to", "what is", "why", "where", "can"]
for q in questions:
    variations.append(f"{q} {seed}")


5.2 API Response Parsing

Google Suggest JSON Format:
["query", ["suggestion1", "suggestion2", ...], ...]

Parsing Logic: Extract the second element of the root array.

5.3 Performance Constraints

Concurrency: To prevent blocking, requests should be sent in parallel batches (e.g., 10 requests at a time).

Rate Limiting:

Unofficial API: Max 1 request per second per IP (requires proxy rotation for higher speeds).

DataForSEO: Dependent on account limits (usually high throughput).

6. UI/UX Wireframe Description

Header

Title: "Keyword Harvester"

Credits Balance (if using DataForSEO).

Main Control Panel (Left Sidebar)

Input: [ Enter Seed Keyword ]

Checkboxes:

[x] Append A-Z

[ ] Append 0-9

[x] Comparisons (vs, or)

[x] Intent (Best, Top)

[x] Questions (How, What)

Action Button: [ Start Harvesting ] (Changes to "Stop" during process).

Results Area (Right Panel)

Status Bar: "Harvesting: 'coffee a'... Found 45 keywords..."

Filter Bar:

[ Filter by text... ]

[ Min Words: 0 ]

[ Max Words: 10 ]

Data Table:

Columns: Keyword | Length | Source Modifier

Footer Actions:

[ Copy All ] [ Export CSV ]

7. Future Scope (V2)

SERP Data Enrichment: Fetch Search Volume and CPC for the harvested keywords (requires connecting to Volume API).

Clustering: Group the harvested keywords by intent.