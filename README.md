# Expedia Travel Experience: Text Extraction and Planning Analysis

A comprehensive data science project that extracts and analyzes Expedia attraction listings and customer reviews for New York City to help travelers make informed travel-planning decisions.

## Table of Contents

- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Configuration](#configuration)
- [Usage](#usage)
  - [Running the Analysis](#running-the-analysis)
  - [Live Web Scraping](#live-web-scraping)
  - [Working with Saved Data](#working-with-saved-data)
- [Data Extraction Pipeline](#data-extraction-pipeline)
- [Analysis Workflow](#analysis-workflow)
- [Output & Insights](#output--insights)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

This project demonstrates a complete data science workflow for transforming unstructured web content into analytical insights. It specifically:

1. **Extracts attraction data** from Expedia's New York attractions search results
2. **Collects customer reviews** from individual attraction pages
3. **Cleans and structures** the raw data into CSV datasets
4. **Performs exploratory analysis** to identify patterns, pricing trends, and customer sentiment
5. **Generates travel recommendations** based on multi-criteria analysis

The project is implemented as a Jupyter notebook that combines web scraping (Selenium), data processing (Pandas), and exploratory analysis into a reproducible workflow.

---

## Problem Statement

A traveler planning a short trip to New York faces overwhelming choices: many highly-rated attractions exist, but understanding the full picture—combining quality ratings, price, popularity, cancellation policies, and actual customer feedback—is challenging.

**Key Questions This Project Answers:**

1. How can attraction and review text be automatically extracted from Expedia pages into structured datasets?
2. What patterns emerge in pricing, ratings, and review volume across attractions?
3. Which attractions are most expensive, and would a $10,000 budget cover the top premium options?
4. Among premium attractions, which has the strongest customer engagement signal?
5. What full-day trip experiences are available in the attraction catalog?
6. What themes and sentiments appear across customer reviews?
7. How can this analysis inform a practical, high-value trip itinerary?

---

## Features

- **Automated Web Scraping**: Selenium-based extraction of attraction details from Expedia
- **XPath-Based Parsing**: Robust extraction of multiple data fields from dynamic web pages
- **Data Cleaning Pipeline**: Transforms raw extracted data into clean, analyzable datasets
- **Reproducibility**: Includes saved data snapshots (CSV files) to ensure analysis reproducibility without repeated web requests
- **Exploratory Data Analysis**: Statistical analysis of ratings, prices, and review volume
- **Sentiment & Theme Analysis**: Extract themes from customer review text
- **Budget Analysis**: Identify best-value attractions within budget constraints
- **Flexible Architecture**: Can run from live web data or pre-saved snapshots

---

## Technology Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Data Processing** | Python 3, Pandas | Data cleaning, transformation, analysis |
| **Web Scraping** | Selenium WebDriver | Browser-based HTML extraction |
| **Notebook** | Jupyter Notebook | Interactive analysis and documentation |
| **Data Storage** | CSV | Structured data serialization |
| **Browser Control** | ChromeDriver | Headless Chrome automation |

---

## Project Structure

```
Expedia-Travel-Plan/
├── Project.ipynb                    # Main Jupyter notebook with complete analysis
├── README.md                        # This file
├── LICENSE                          # GNU General Public License v3
├── attractions_raw.csv              # Raw extracted attraction data (75 attractions)
├── attractions.csv                  # Cleaned attraction data
├── reviews.csv                      # Customer reviews and feedback
└── .gitattributes                   # Git configuration
```

### Data Files Description

| File | Rows | Purpose |
|------|------|---------|
| `attractions_raw.csv` | 75 | Raw scraped attraction data with URLs and field values |
| `attractions.csv` | 75 | Cleaned attractions with normalized prices, ratings, and text |
| `reviews.csv` | 500+ | Customer review records linked to attractions |

### Key Data Fields

**Attractions Dataset:**
- `Attraction_name`: Title of the attraction or experience
- `Company`: Tour operator or attraction provider
- `Rating`: Average customer rating (0-10 scale)
- `Reviews`: Count of customer reviews
- `Ticket_price`: USD price per ticket
- `Free_cancellation`: Cancellation policy indicator
- `Overview`: Short description of the attraction
- `Location`: Physical address or area
- `Meeting_point`: Where tour participants gather
- `Attraction_page`: URL to the original Expedia listing

**Reviews Dataset:**
- `Attraction_page`: Link to the reviewed attraction
- `Customer_name`: Reviewer's name
- `Review_scores`: Rating (e.g., "9.5/10")
- `Review_date`: When the review was posted
- `Country`: Reviewer's country
- `Review_text`: Full review text

---

## Prerequisites

### System Requirements
- **Python**: 3.8 or higher
- **Operating System**: Windows, macOS, or Linux
- **Memory**: 2GB minimum (for Jupyter and data processing)
- **Internet Connection**: Required for live web scraping (optional if using saved data)

### Software Requirements
- Jupyter Notebook or JupyterLab
- Google Chrome browser (for Selenium web driver)
- pip (Python package manager)

---

## Installation & Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/Chakrapani2122/Expedia-Travel-Plan.git
cd Expedia-Travel-Plan
```

### Step 2: Create a Virtual Environment (Recommended)

```bash
# On macOS/Linux
python3 -m venv venv
source venv/bin/activate

# On Windows
python -m venv venv
venv\Scripts\activate
```

### Step 3: Install Required Dependencies

```bash
pip install --upgrade pip
pip install pandas jupyter selenium webdriver-manager
```

**Detailed Dependency Information:**

| Package | Version | Purpose |
|---------|---------|---------|
| `pandas` | 1.3+ | Data manipulation and analysis |
| `jupyter` | 1.0+ | Interactive notebook environment |
| `selenium` | 4.0+ | Web browser automation |
| `webdriver-manager` | 3.8+ | Automatic ChromeDriver management |

### Step 4: Launch Jupyter

```bash
jupyter notebook
```

The notebook interface opens in your default browser. Navigate to `Project.ipynb` and open it.

### Step 5: Install ChromeDriver (if running live scraper)

The `webdriver-manager` package handles ChromeDriver installation automatically. If issues occur, manually download ChromeDriver:

1. Visit [ChromeDriver Downloads](https://chromedriver.chromium.org/)
2. Download the version matching your Chrome browser
3. Add the ChromeDriver to your system PATH

---

## Configuration

### Main Configuration Parameters

The notebook includes a configuration section (Section 2) with the following adjustable parameters:

```python
# Run live web scraper (True) or use saved CSV snapshots (False)
RUN_LIVE_SCRAPER = False

# Expedia search URL for New York attractions (October 28-29, 2025)
SEARCH_URL = "https://www.expedia.com/things-to-do/search?..."

# File paths for data storage
ATTRACTIONS_RAW_PATH = "attractions_raw.csv"
ATTRACTIONS_CLEAN_PATH = "attractions.csv"
REVIEWS_PATH = "reviews.csv"

# Budget constraint for trip planning analysis
BUDGET = 10000  # USD
```

### Configuration Options

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `RUN_LIVE_SCRAPER` | Boolean | `False` | Whether to scrape live from Expedia or use saved CSV files |
| `SEARCH_URL` | String | (Expedia URL) | Base search URL for attraction listings |
| `ATTRACTIONS_RAW_PATH` | String | `attractions_raw.csv` | Path to save/load raw attraction data |
| `ATTRACTIONS_CLEAN_PATH` | String | `attractions.csv` | Path to save/load cleaned attraction data |
| `REVIEWS_PATH` | String | `reviews.csv` | Path to save/load customer reviews |
| `BUDGET` | Integer | `10000` | Maximum budget (in USD) for trip planning analysis |

### Environment Variables

While the project doesn't require environment variables, you can extend it by setting:

```bash
# (Optional) Set Chrome options for headless browsing
export CHROME_HEADLESS=true
```

---

## Usage

### Running the Analysis

#### Option 1: Using Saved Data (Recommended for Quick Analysis)

This is the default behavior. No internet scraping is required:

```bash
jupyter notebook Project.ipynb
```

Then run all cells from top to bottom. The notebook uses the pre-saved CSV files, so the entire analysis completes in 5-10 minutes without web requests.

#### Option 2: Live Web Scraping

To collect fresh data from Expedia:

1. Open `Project.ipynb` in Jupyter
2. In Section 2 (Project Configuration), change:
   ```python
   RUN_LIVE_SCRAPER = True
   ```
3. Run the notebook cells sequentially
4. The scraper will:
   - Open Expedia's attraction search page
   - Extract attraction links
   - Visit each attraction page and extract details
   - Save new `attractions_raw.csv` and `reviews.csv` files

**Note**: Live scraping takes 30+ minutes due to page load times and may be blocked by Expedia's rate limiting.

### Example Workflow

1. **Launch Jupyter**:
   ```bash
   jupyter notebook
   ```

2. **Open `Project.ipynb`**

3. **Run Section by Section**:
   - Section 1: Load libraries and set up environment
   - Section 2: Configure parameters (set `RUN_LIVE_SCRAPER = False` to use saved data)
   - Section 3: Extract attraction links
   - Section 4: Extract attraction details and reviews
   - Section 5: Clean and normalize the data
   - Section 6: Exploratory data analysis
   - Section 7: Budget and value analysis
   - Section 8: Review theme analysis
   - Section 9: Generate recommendations

4. **Examine outputs**: Charts, tables, and insights are displayed inline

### Working with Saved Data

The project includes pre-extracted data snapshots:

```python
# Load attractions data
attractions = pd.read_csv("attractions.csv", index_col=0)

# Load reviews
reviews = pd.read_csv("reviews.csv", index_col=0)

# Display summary
print(f"Total attractions: {len(attractions)}")
print(f"Average rating: {attractions['Rating'].mean():.1f}")
print(f"Price range: ${attractions['Ticket_price'].min():.0f} - ${attractions['Ticket_price'].max():.0f}")
```

---

## Data Extraction Pipeline

### Stage 1: Collect Attraction Links

The scraper navigates to Expedia's New York attractions search page (filtered for highly-rated options) and extracts 75 attraction URLs using XPath selectors.

**Key XPath Used:**
```xpath
//div[@class="uitk-card uitk-card-roundcorner-all ..."]/a
```

**Output**: List of 75 unique attraction page URLs

### Stage 2: Extract Attraction Details

For each attraction URL, the scraper opens the page and extracts:

| Field | XPath Selector | Fallback |
|-------|----------------|----------|
| Attraction Name | `//h4[@class="uitk-heading uitk-heading-4..."]` | "No Name" |
| Company | `//div[@class="uitk-text uitk-type-300..."]` | "No Company" |
| Rating | `(//span[@class="uitk-badge-base-text"])[1]` | "No Ratings" |
| Review Count | `//button[@class="uitk-link uitk-spacing..."]` | "No Reviews" |
| Price | `(//span[@class="uitk-lockup-price"])[1]` | "No Price" |
| Cancellation | `//ul[@class="uitk-typelist..."]/li[1]` | "No Cancellation Details" |
| Overview | `(//div[@class="uitk-layout-flex-item..."])[2]` | "No Overview" |
| Location | `(//ul[@class="uitk-typelist..."])[1]/li[1]` | "No Location" |
| Meeting Point | `(//ul[@class="uitk-typelist..."])[1]/li[2]` | "No Meeting Point" |

**Helper Function Example:**
```python
def read_element_text(driver, xpath, default_value):
    """Extract text from page element with fallback."""
    try:
        return driver.find_element("xpath", xpath).get_attribute("textContent").strip()
    except Exception:
        return default_value
```

### Stage 3: Extract Reviews

For each attraction page, scroll down to find the reviews section and extract:
- Customer name
- Review score
- Review date
- Customer country
- Full review text

**Output**: CSV with 500+ review records

### Stage 4: Data Cleaning

Raw extracted data is cleaned:
- Convert price strings (e.g., "$48.00") to numeric values
- Standardize rating formats
- Remove extra whitespace from text fields
- Handle missing values

---

## Analysis Workflow

The notebook performs the following analyses:

### 1. Descriptive Statistics
```python
attractions.describe()  # Summary statistics
attractions.groupby('Company').agg({'Rating': 'mean', 'Ticket_price': 'mean'})
```

### 2. Pricing Analysis
- Distribution of ticket prices
- Price vs. rating correlation
- Most expensive attractions
- Budget coverage analysis

### 3. Rating & Popularity Analysis
- Average ratings by company
- Review volume distribution
- High-rated vs. price relationship

### 4. Budget Planning
- Identify top N most expensive attractions
- Calculate cumulative cost
- Determine budget feasibility for premium options

### 5. Review Sentiment Analysis
- Extract themes from review text (e.g., "amazing experience", "crowded")
- Identify most mentioned keywords
- Assess overall sentiment trends

### 6. Itinerary Recommendations
- Suggest high-value attractions (high rating, moderate price)
- Identify full-day experiences
- Optimize for variety and budget

---

## Output & Insights

The analysis produces:

### Data Outputs
- Cleaned CSV files with normalized attraction and review data
- Summary statistics tables

### Visualizations (if applicable in extended versions)
- Price distribution histograms
- Rating vs. price scatter plots
- Review count distribution
- Company market share charts
- Review theme word clouds

### Textual Recommendations
- Top 10 attractions by value (rating-to-price ratio)
- Suggested itinerary combining attractions within budget
- Key customer sentiment themes
- Best providers/companies by average rating

---

## Contributing

Contributions are welcome! To contribute:

1. **Fork the repository** on GitHub
2. **Create a feature branch**:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes** and test thoroughly
4. **Commit with clear messages**:
   ```bash
   git commit -m "Add: Brief description of changes"
   ```
5. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```
6. **Open a Pull Request** describing your changes and improvements

### Areas for Contribution
- Add additional analysis sections (e.g., location-based clustering)
- Improve web scraping XPath selectors for robustness
- Add data visualization charts
- Extend sentiment analysis with NLP libraries (TextBlob, VADER)
- Create modular Python scripts (separate from notebook)
- Add unit tests
- Improve documentation and examples
- Support scraping other cities or destinations

---

## License

This project is licensed under the **GNU General Public License v3.0 (GPLv3)**.

See the [LICENSE](LICENSE) file for full license text.

**Key Points:**
- You are free to use, modify, and distribute this project
- If you distribute modified versions, you must include the source code and license
- The project comes with NO warranty
- This is a copyleft license—derivative works must also be open source under GPLv3

---

## Troubleshooting

### Issue: Selenium import error
**Solution**: Install Selenium:
```bash
pip install selenium webdriver-manager
```

### Issue: ChromeDriver version mismatch
**Solution**: The `webdriver-manager` package auto-handles this. If issues persist:
```bash
pip install --upgrade webdriver-manager
```

### Issue: Expedia page blocks scraper
**Solution**: This is expected. The scraper uses anti-automation detection bypasses, but Expedia may still block requests. Use the saved CSV files instead by setting `RUN_LIVE_SCRAPER = False`.

### Issue: CSV files not found
**Solution**: Ensure you're in the correct directory:
```bash
cd Expedia-Travel-Plan
ls *.csv  # Should list attractions.csv, reviews.csv, etc.
```

### Issue: Jupyter notebook won't start
**Solution**: 
```bash
# Restart the kernel within Jupyter or restart from terminal:
jupyter notebook --ip=127.0.0.1
```

---

## Contact & Support

For questions, issues, or suggestions:
- **GitHub Issues**: [Open an issue](https://github.com/Chakrapani2122/Expedia-Travel-Plan/issues)
- **Author**: Chakrapani Gajji

---

## Acknowledgments

- **Expedia**: Attraction listings and customer reviews
- **Selenium**: Web automation framework
- **Pandas**: Data manipulation library
- **Python Community**: Open-source tools and libraries

---

**Last Updated**: June 2025  
**Version**: 1.0
