# DPSA — Web Scraping Vacancies Using Python

Automated scraper for South African government job vacancy circulars published by the [Department of Public Service and Administration (DPSA)](https://www.dpsa.gov.za/newsroom/psvc/).

Each circular contains PDF links for 15+ national departments and 7 provincial administrations. This tool extracts those links automatically and saves them to a structured CSV file.
date of extraction :19 Mar 2023
---

## What It Does

- Fetches a DPSA vacancy circular page
- Extracts all department PDF vacancy links
- Deduplicates results and filters to PDFs only
- Saves output to CSV for analysis
- *(Optional)* Bulk scrapes all historical circulars listed in the sidebar

---

## Repository Structure

```
dpsa-web-scraping-vacancies/
│
├── Web_Scraper_Circulars_Original.ipynb    # Original exploratory notebook
├── Web_Scraper_Circulars_Refactored.ipynb  # Refactored, production-ready notebook
├── requirements.txt                         # Python dependencies
├── .gitignore                               # Files excluded from version control
└── README.md                               # This file
```

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/dpsa-web-scraping-vacancies.git
cd dpsa-web-scraping-vacancies
```

### 2. Create a virtual environment (recommended)

```bash
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Launch Jupyter

```bash
jupyter notebook
```

Open `Web_Scraper_Circulars_Refactored.ipynb` to get started.

---

## Usage

### Scrape a single circular

Set the `CIRCULAR_URL` in the configuration cell to the circular you want, then run all cells. A CSV file named `circular_08_2026_links.csv` (or similar) will be saved in the working directory.

```python
CIRCULAR_URL = "https://www.dpsa.gov.za/newsroom/psvc/circular-08-of-2026/"
```

### Scrape all circulars

Run Section 4 of the refactored notebook. It reads the sidebar to discover all listed circular URLs and collects every PDF link into a single file: `all_circulars_links.csv`.

---

## Output Format

| Column | Description |
|--------|-------------|
| `title` | Department name (e.g. `Agriculture`, `Gauteng`) |
| `url` | Absolute URL to the department's PDF vacancy document |
| `circular` | *(Bulk mode only)* Source circular identifier |

---

## Original vs. Refactored

| Issue | Original | Refactored |
|-------|----------|------------|
| Runtime bug (`urljoin`) | ❌ Crashes | ✅ Fixed |
| Duplicate results | ❌ ~44 links | ✅ ~22 clean links |
| Error handling | ❌ None | ✅ try/except with timeout |
| PDF filtering | ❌ Includes non-PDFs | ✅ `.pdf` filter applied |
| Output saved | ❌ Prints to stdout | ✅ Saved to CSV |
| Bulk scraping | ❌ Not supported | ✅ Supported |

---

## Requirements

- Python 3.9+
- See `requirements.txt` for package versions

---

## License

This project is open source and available under the [MIT License](LICENSE).

---

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

---

## Disclaimer

This tool scrapes publicly available information from a South African government website. Please use responsibly and review the [DPSA website terms of use](https://www.dpsa.gov.za/terms-of-use/) before deploying at scale.
