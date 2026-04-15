# VTU Internship Diary Generator (IS&E Optimized)

A browser-based tool to extract VTU internship diary entries and generate a clean, structured, and print-ready PDF tailored for IS&E department evaluation standards.

Repository: [https://github.com/R-Pradhyumna/VTU-Diary-IS-E.git](https://github.com/R-Pradhyumna/VTU-Diary-IS-E.git)

---

## Overview

Maintaining a VTU internship diary manually involves repeatedly opening each entry, copying content, and formatting it for submission. This project automates the entire workflow end-to-end.

The system:

1. Extracts diary entries directly from the VTU portal
2. Cleans and structures the data
3. Generates a professionally formatted diary PDF aligned with IS&E expectations

The entire workflow runs inside the browser with no installation or external dependencies required.

---

## Features

### Data Extraction

- Fetches all diary entries from the VTU portal
- Handles pagination automatically
- Extracts:
  - Date
  - Hours
  - Work Summary
  - Learnings

### Data Processing

- Removes unnecessary whitespace and formatting
- Retains only the first two meaningful lines per field during extraction
- Sorts entries chronologically
- Requires skill enrichment (skills must be added before generating the diary)

### PDF Generation (IS&E Optimized)

- One diary entry per page (IS&E-compliant format)
- Clear structured sections:
  - Skills
  - Description
  - Learnings/Outcomes

- Bullet formatting for improved readability
- Justified paragraphs for professional presentation
- Signature sections included
- Stable A4 layout using browser print engine

### Lightweight and Dependency-Free

- Runs entirely in the browser
- No Node.js, Puppeteer, or external libraries required
- Works on any modern browser (Chrome recommended)

---

## Project Structure

```
.
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── fetchData.js
├── index.html
├── LICENSE.md
├── README.md
├── SECURITY.md
└── viewer.html
```

---

## How It Works

### Step 1: Data Extraction

The script in `fetchData.js` calls the VTU API:

[https://vtuapi.internyet.in/api/v1/student/internship-diaries](https://vtuapi.internyet.in/api/v1/student/internship-diaries)

Workflow:

1. Fetch paginated data
2. Extract required fields
3. Normalize content (retain first two meaningful lines)
4. Sort entries by date
5. Download `refined_diary.json`

---

### Step 2: Add Skills to JSON (Required)

The extracted JSON does not include skills by default.

Before generating the diary:

- Each entry must include a `skills` field
- Skills should be 1–2 relevant technical keywords per entry

You can do this manually or using AI tools (e.g., ChatGPT).

**Tip:**

- Paste the entire JSON into ChatGPT
- Ask:
  "Add 1–2 technical skills per entry and return full JSON"

Example:

```json
{
  "date": "2026-02-02",
  "hours": 6,
  "skills": "Problem Analysis, Technical Assessment",
  "work_summary": "...",
  "learnings": "..."
}
```

Save the updated file as:

```
diary_with_skills.json
```

---

### Step 3: Generate Diary

- Open `index.html`
- Upload `diary_with_skills.json`
- Click "Generate Diary"

---

### Step 4: Save as PDF

- Open print dialog (Ctrl + P)
- Destination → Save as PDF
- Pages → All
- Layout → Portrait

**Important:**

- Disable "Headers and Footers"

This removes unwanted browser metadata from the final document.

---

## Design Decisions

### Structured Academic Formatting (IS&E Focus)

Instead of compressing multiple entries per page, this system adopts a one-entry-per-page approach to align with IS&E evaluation standards.

Each entry is structured into:

- Skills (bullet points)
- Description (justified paragraph)
- Learnings/Outcomes (bullet points)

This improves:

- Readability
- Clarity of technical content
- Evaluation efficiency

---

### Content Normalization

Handling inconsistent content length is a core challenge in document generation.

This system:

- Reduces content to meaningful lines during extraction
- Preserves semantic clarity instead of truncating visually
- Avoids broken sentences or clipped content

---

### Stable Pagination Strategy

Instead of dynamic layouts:

- Uses one entry per page
- Applies controlled page breaks
- Prevents layout overflow into signature sections

This ensures consistent, predictable output.

---

### Dependency-Free Architecture

The system relies entirely on:

- Native browser APIs
- `window.print()` for PDF generation

Benefits:

- No installation required
- Cross-platform compatibility
- Minimal maintenance overhead

---

### Separation of Concerns

- `fetchData.js` → Data extraction and normalization
- `index.html` → Upload interface
- `viewer.html` → Rendering and formatting

This improves modularity and maintainability.

---

## Limitations

- Requires active VTU login session
- Dependent on VTU API structure
- Browser print rendering may vary slightly

---

## Security

- No data is transmitted externally
- All processing happens locally in the browser
- Do not share session cookies or sensitive data

---

## License

See: [LICENSE.md](./LICENSE.md)

---

## Contributing

See: [CONTRIBUTING.md](./CONTRIBUTING.md)

---

## Code of Conduct

See: [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)

---

## Security Policy

See: [SECURITY.md](./SECURITY.md)

---

## Future Improvements

- AI-based skill generation
- Grammar and content refinement
- Duplicate entry detection
- Page numbering
- Department-specific templates (CSE, AIML, etc.)
- Hosted web version
