# READMEFIRST — Do Presidents Govern As They Speak?

**Author:** David Lopez  
**Course:** DS-GA 1015 — Text as Data  
**Project type:** Reproducible text-as-data research notebook  
**Main notebook:** `David Lopez\_Do\_Presidents\_Govern\_As\_They\_Speak\_Notebook.ipynb`

\---

## 1\. What this project does

This project asks:

> \*\*Do U.S. presidents govern consistently with the ideological positions they express publicly?\*\*

The notebook builds two text corpora:

* **Say corpus:** public presidential speech, including interviews, inaugural addresses, farewell addresses, speeches, and news conferences when available.
* **Do corpus:** formal presidential action, mainly executive orders and written presidential orders.

The project then places each president twice in a two-axis ideological space:

* **X-axis:** left ↔ right
* **Y-axis:** libertarian ↔ authoritarian

Each president receives:

1. a **Say position**, based on public rhetoric;
2. a **Do position**, based on governing action;
3. a **Say–Do gap**, calculated as the geometric distance between those two positions.

A smaller gap means the president’s words and actions are more aligned. A larger gap means the president’s rhetoric and formal actions are farther apart.

\---

## 2\. What to open first

For a fast review, open these files in this order:

1. **Final PDF report**  
Read this first for the written argument, methodology, results, and conclusion.
2. **`READMEFIRST.md`**  
This file explains how the replication package is organized.
3. **`David Lopez\_Do\_Presidents\_Govern\_As\_They\_Speak\_Notebook.ipynb`**  
This is the full reproducible notebook.
4. **`process\_outputs/dictionary\_based\_full\_outputs\_FINAL.xlsx`**  
Main president-level outputs.
5. Zip contains data for Say Corpus and Do Corpus

\---

## 3\. Repository structure

Recommended GitHub structure:

```text
.
├── READMEFIRST.md
├── David Lopez\_Do\_Presidents\_Govern\_As\_They\_Speak\_Notebook.ipynb
├── requirements.txt
├── final\_report.pdf
├── presidents\_say\_do\_corpus\_output/
│   ├── full\_say\_do\_document\_corpus.csv
│   ├── full\_say\_do\_chunked\_audit.csv
│   ├── say\_document\_corpus.csv
│   ├── do\_document\_corpus.csv
│   └── corpus\_visualizations/
│       ├── 01\_corpus\_composition\_by\_document\_type\_words.png
│       ├── 02\_say\_vs\_do\_total\_words.png
│       ├── 04\_words\_per\_president\_say\_do\_proportions.png
│       ├── 05\_timeline\_coverage\_total\_words\_by\_year.png
│       ├── 05\_timeline\_coverage\_total\_words\_by\_decade.png
│       └── 06\_document\_length\_distribution\_by\_document\_type.png
├── process\_outputs/
│   ├── say\_document\_corpus.csv
│   ├── do\_document\_corpus.csv
│   ├── president\_evidence\_filter\_table.csv
│   ├── ideological\_phrase\_dictionary\_FINAL.csv
│   ├── ideological\_phrase\_dictionary\_FINAL.xlsx
│   ├── dictionary\_president\_corpus\_scores\_FINAL.csv
│   ├── dictionary\_say\_do\_gap\_scores\_FINAL.csv
│   ├── dictionary\_based\_full\_outputs\_FINAL.xlsx
│   ├── say\_do\_gap\_FINAL.png
│   ├── say\_do\_gap\_ranked\_FINAL.png
│   ├── party\_dictionary\_corpus\_scores\_FINAL.csv
│   ├── party\_say\_do\_gap\_scores\_FINAL.csv
│   ├── party\_based\_full\_outputs\_FINAL.xlsx
│   ├── validation\_outputs/
│   │   ├── dictionary\_validation\_audit\_workbook.xlsx
│   │   ├── president\_validation\_summary.csv
│   │   ├── top\_phrase\_families\_by\_president\_corpus\_axis.csv
│   │   └── top\_variants\_by\_president\_corpus\_axis.csv
│   └── gap\_explanation\_outputs/
│       ├── president\_gap\_axis\_decomposition.csv
│       ├── president\_family\_axis\_contribution.csv
│       ├── president\_say\_do\_family\_delta\_explanation.csv
│       ├── top\_president\_gap\_explanations.csv
│       └── say\_do\_gap\_explanation\_workbook.xlsx
└── raw\_chunked\_files/
    ├── us\_presidents\_interviews\_\*\_chunked.xlsx
    ├── us\_presidents\_inaugural\_addresses\_chunked.xlsx
    ├── us\_presidents\_farewell\*\_chunked.xlsx
    ├── us\_presidents\_news\_conferences\*\_chunked.xlsx
    ├── us\_presidents\_executive\_orders\_\*\_chunked.xlsx
    └── us\_presidents\_written\_presidential\_orders\*\_chunked.xlsx
```

The exact folder names may differ slightly depending on how the files are packaged. The notebook uses relative paths and recursive file search where possible.

\---

## 4\. Data source

The source texts are scraped from **The American Presidency Project**:

```text
https://www.presidency.ucsb.edu/
```

The notebook includes scraping code for:

* presidential interviews;
* farewell addresses;
* inaugural addresses;
* executive orders;
* news conferences.

The scraped files are saved as Excel workbooks with two tabs:

```text
interviews
transcript\_chunks
```

Even when the document type is not literally an interview, the notebook expects this same two-sheet format for consistency.

\---

## 5\. Environment setup

### Recommended environment

Use Python 3.11 or newer.

This project was designed to run in Jupyter Notebook or JupyterLab.

### Install dependencies

From the repository folder, run:

```bash
pip install pandas numpy matplotlib requests beautifulsoup4 openpyxl scikit-learn jupyter
```

Optional but recommended:

```bash
pip freeze > requirements.txt
```

### Main Python libraries used

```text
pandas
numpy
matplotlib
requests
beautifulsoup4
openpyxl
scikit-learn
pathlib
re
shutil
tempfile
```

\---

## 6\. How to reproduce the project

### Option A — fastest replication

Use this option if the replication package already includes the scraped `.xlsx` files and generated outputs.

1. Download or clone the repository.
2. Open the repository folder.
3. Install the dependencies.
4. Open:

```text
David Lopez\_Do\_Presidents\_Govern\_As\_They\_Speak\_Notebook.ipynb
```

5. Run the notebook from top to bottom.
6. Review the outputs in:

```text
presidents\_say\_do\_corpus\_output/
process\_outputs/
```

### Option B — full replication from raw scraping

Use this option only if the raw scraped files are missing or need to be regenerated.

1. Open the notebook.
2. Run the scraping sections first:

   * Scrape Data — Interviews
   * Scrape Data — Farewell Address
   * Scrape Data — Inaugural
   * Scrape Data — Executive Orders
   * Scrape Data — News Conferences
3. Then run the corpus-building section.
4. Then run the preprocessing and scoring sections.

Important: the scraper uses a delay between requests. This is intentional and helps avoid making too many requests too quickly.

\---

## 7\. Notebook run order

Run the notebook in this order:

```text
Part 1: Introduction and Research Question
Part 2: Corpus and Data
    1. Scrape Data from The American Presidency Project
    2. Build Say Corpus and Do Corpus
    3. Corpus Visualizations

Part 3: Methodology
    4. Basic Text Cleaning
    5. Executive-Order Boilerplate Removal
    6. Negation Standardization
    7. Normalize and Confidence Filter
    8. Corpus-Guided N-Gram Discovery
    9. Build Ideological Phrase Dictionary
   10. President-Level Dictionary-Based Say–Do Scoring
   11. Validation Audit
   12. Party-Level Dictionary-Based Say–Do Aggregation
   13. Difference Interpretation
```

Do not skip the preprocessing cells if rerunning the scoring section. Later sections depend on objects and files created earlier.

\---

## 8\. Main methodology

### Step 1 — Build corpora

The notebook collects presidential texts and separates them into:

```text
Say = public rhetoric
Do  = formal presidential action
```

The notebook rebuilds full documents from chunked transcript files.

Expected corpus size from the completed notebook:

```text
Say corpus words: 12,484,484
Do corpus words:  6,092,542
Full corpus words: 18,577,026
```

### Step 2 — Preprocess text

The notebook performs:

1. **Basic text cleaning**  
Lowercases text, removes URLs, removes non-letter symbols, and standardizes whitespace.
2. **Executive-order boilerplate removal**  
Removes repeated legal phrases from the Do corpus so the scoring is less dominated by formal executive-order language.
3. **Negation standardization**  
Standardizes phrases like “do not,” “cannot,” and related constructions so they are easier to count consistently.
4. **Normalize and confidence filter**  
Keeps presidents with enough evidence in both corpora.

The confidence filter requires:

```text
minimum Say words: 5,000
minimum Do words:  5,000
```

The notebook kept 21 presidents after this stage.

### Step 3 — Discover n-grams

The notebook extracts 2-grams, 3-grams, and 4-grams from the Say and Do corpora.

Settings:

```text
NGRAMS\_TO\_RUN = \[2, 3, 4]
MIN\_COUNT = 5
TOP\_N = 50
```

This step supports dictionary construction and phrase-quality review.

### Step 4 — Build ideological dictionary

The notebook builds a four-pole dictionary:

```text
left
right
libertarian
authoritarian
```

Dictionary size from the notebook:

```text
Families: 80
Expanded clean rows: 640
Unique clean variants: 634
```

Each phrase family has:

```text
family
axis
direction
intensity\_0\_to\_5
theme
variant
```

### Step 5 — Score presidents

The scoring method counts dictionary phrase hits in each president’s Say and Do corpora.

Main settings:

```text
SCORING\_MODE = document\_presence\_with\_variant\_and\_family\_caps
MIN\_DICTIONARY\_HITS\_PER\_CORPUS = 25
VARIANT\_DOCUMENT\_HIT\_CAP = 25
FAMILY\_HIT\_CAP = 100
```

Each president receives:

```text
Say x-coordinate
Say y-coordinate
Do x-coordinate
Do y-coordinate
Say–Do gap
```

### Step 6 — Explain differences

The final section decomposes the Say–Do gap by:

```text
left-right difference
libertarian-authoritarian difference
phrase family contribution
top phrase variants
```

This makes the results interpretable instead of only producing a distance score.

\---

## 9\. Main outputs

### Corpus outputs

```text
presidents\_say\_do\_corpus\_output/full\_say\_do\_document\_corpus.csv
presidents\_say\_do\_corpus\_output/full\_say\_do\_chunked\_audit.csv
presidents\_say\_do\_corpus\_output/presidents\_say\_do\_corpus\_summary.xlsx
```

### Preprocessed corpora

```text
process\_outputs/say\_document\_corpus.csv
process\_outputs/do\_document\_corpus.csv
process\_outputs/president\_evidence\_filter\_table.csv
```

### Dictionary outputs

```text
process\_outputs/ideological\_phrase\_dictionary\_FINAL.csv
process\_outputs/ideological\_phrase\_dictionary\_FINAL.xlsx
process\_outputs/ideological\_phrase\_dictionary\_LOOKUP\_SORTED.csv
process\_outputs/ideological\_phrase\_dictionary\_axis\_audit.csv
process\_outputs/ideological\_phrase\_dictionary\_family\_audit.csv
```

### President-level scoring outputs

```text
process\_outputs/dictionary\_president\_corpus\_scores\_FINAL.csv
process\_outputs/dictionary\_say\_do\_gap\_scores\_FINAL.csv
process\_outputs/dictionary\_based\_full\_outputs\_FINAL.xlsx
process\_outputs/president\_number\_legend\_mapping\_FINAL.csv
```

### Validation outputs

```text
process\_outputs/validation\_outputs/dictionary\_validation\_audit\_workbook.xlsx
process\_outputs/validation\_outputs/president\_validation\_summary.csv
process\_outputs/validation\_outputs/top\_phrase\_families\_by\_president\_corpus\_axis.csv
process\_outputs/validation\_outputs/top\_variants\_by\_president\_corpus\_axis.csv
```

### Gap explanation outputs

```text
process\_outputs/gap\_explanation\_outputs/president\_gap\_axis\_decomposition.csv
process\_outputs/gap\_explanation\_outputs/president\_family\_axis\_contribution.csv
process\_outputs/gap\_explanation\_outputs/president\_say\_do\_family\_delta\_explanation.csv
process\_outputs/gap\_explanation\_outputs/top\_president\_gap\_explanations.csv
process\_outputs/gap\_explanation\_outputs/say\_do\_gap\_explanation\_workbook.xlsx
```

### Party-level outputs

```text
process\_outputs/party\_dictionary\_corpus\_scores\_FINAL.csv
process\_outputs/party\_say\_do\_gap\_scores\_FINAL.csv
process\_outputs/party\_president\_mapping\_FINAL.csv
process\_outputs/party\_based\_full\_outputs\_FINAL.xlsx
```

\---

## 10\. Key figures

```text
presidents\_say\_do\_corpus\_output/corpus\_visualizations/01\_corpus\_composition\_by\_document\_type\_words.png
presidents\_say\_do\_corpus\_output/corpus\_visualizations/02\_say\_vs\_do\_total\_words.png
presidents\_say\_do\_corpus\_output/corpus\_visualizations/04\_words\_per\_president\_say\_do\_proportions.png
presidents\_say\_do\_corpus\_output/corpus\_visualizations/05\_timeline\_coverage\_total\_words\_by\_year.png
presidents\_say\_do\_corpus\_output/corpus\_visualizations/05\_timeline\_coverage\_total\_words\_by\_decade.png
presidents\_say\_do\_corpus\_output/corpus\_visualizations/06\_document\_length\_distribution\_by\_document\_type.png

process\_outputs/say\_corpus\_numbered\_markers\_FINAL\_full.png
process\_outputs/do\_corpus\_numbered\_markers\_FINAL\_full.png
process\_outputs/say\_corpus\_numbered\_markers\_FINAL\_zoom\_2\_5.png
process\_outputs/do\_corpus\_numbered\_markers\_FINAL\_zoom\_2\_5.png
process\_outputs/say\_do\_gap\_FINAL.png
process\_outputs/say\_do\_gap\_ranked\_FINAL.png

process\_outputs/party\_say\_corpus\_markers\_FINAL.png
process\_outputs/party\_do\_corpus\_markers\_FINAL.png
process\_outputs/party\_say\_do\_gap\_FINAL.png
process\_outputs/party\_say\_do\_gap\_ranked\_FINAL.png

process\_outputs/validation\_outputs/top\_family\_contributions\_largest\_gaps.png
process\_outputs/validation\_outputs/dictionary\_coverage\_by\_president\_corpus.png

process\_outputs/gap\_explanation\_outputs/gap\_axis\_decomposition\_ranked.png
process\_outputs/gap\_explanation\_outputs/top\_family\_deltas\_largest\_gaps.png
```

\---

## 11\. Expected sanity-check results

A successful run should produce results close to these notebook outputs:

```text
Full corpus words: 18,577,026
Say corpus words: 12,484,484
Do corpus words: 6,092,542
Kept presidents after confidence filter: 21
Dictionary families: 80
Expanded dictionary rows: 640
Unique clean phrase variants: 634
Presidents used in final party aggregation: 16
Parties used: 2
```

Largest president-level Say–Do gaps in the notebook:

```text
1. Gerald R. Ford
2. Dwight D. Eisenhower
3. John F. Kennedy
4. Donald J. Trump
5. Jimmy Carter
```

Party-level Say–Do gap from the notebook:

```text
Republican:  1.892293
Democratic:  1.107003
```

These values are useful as a quick check that the notebook ran correctly.

\---

## 12\. Reproducibility notes

To make the project reproducible:

* Keep the notebook, raw scraped files, and outputs together.
* Do not rename the key output folders unless the notebook is updated.
* Run the notebook from the repository root.
* Use the same Python environment when possible.
* Include the generated `.csv`, `.xlsx`, and `.png` outputs in the submitted replication package.
* Keep the raw chunked `.xlsx` files so the project can be rerun without scraping.
* If scraping is rerun later, results may change slightly because the source website may update.

\---

## 13\. Troubleshooting

### `FileNotFoundError`

Make sure the raw chunked Excel files are inside the repository folder or a subfolder. The notebook searches recursively from the current working directory.

### `Missing sheet: interviews` or `Missing sheet: transcript\_chunks`

Each raw Excel workbook must contain these two sheets:

```text
interviews
transcript\_chunks
```

### `No corpus dataframe found`

Run the corpus-building and preprocessing sections before running n-gram discovery.

### `No presidents remain after the minimum dictionary-hit filter`

This means the dictionary-hit threshold is too strict for the available data. The notebook currently uses:

```text
MIN\_DICTIONARY\_HITS\_PER\_CORPUS = 25
```

### OneDrive or Windows file-locking issues

If Excel files are open while the notebook runs, close them first. The notebook copies files to a temporary folder to reduce OneDrive locking problems.

### Very slow scraping

This is expected. The scraping cells use a delay between requests. For normal grading or review, use the included raw `.xlsx` files instead of scraping again.

\---

## 14\. Suggested `requirements.txt`

If a `requirements.txt` file is not already included, create one with:

```text
pandas
numpy
matplotlib
requests
beautifulsoup4
openpyxl
scikit-learn
jupyter
```

Then install with:

```bash
pip install -r requirements.txt
```

\---

## 15\. Suggested `.gitignore`

Use this to avoid uploading temporary or machine-specific files:

```gitignore
.ipynb\_checkpoints/
\_\_pycache\_\_/
\*.pyc
.DS\_Store
Thumbs.db
\~$\*.xlsx
presidents\_say\_do\_temp/
\*.pkl
```

Do **not** ignore the final `.csv`, `.xlsx`, or `.png` outputs if those files are part of the required replication package.

\---

## 16\. Suggested GitHub submission checklist

Before sharing the repository URL, confirm that:

* \[ ] `READMEFIRST.md` is in the root folder.
* \[ ] The final PDF report is included.
* \[ ] The notebook opens correctly on GitHub.
* \[ ] The raw chunked data files are included or clearly linked.
* \[ ] `process\_outputs/` is included.
* \[ ] `presidents\_say\_do\_corpus\_output/` is included.
* \[ ] The main figures open from GitHub.
* \[ ] The Excel workbooks open correctly.
* \[ ] No private API keys, passwords, or personal files are included.
* \[ ] The repository is public or shared with the professor.
* \[ ] The professor can click the repository URL directly.

For GitHub’s automatic front-page display, either rename this file to:

```text
README.md
```

or keep both:

```text
README.md
READMEFIRST.md
```

where `README.md` can be a short landing page that links to this detailed file.

\---

## 17\. Maintainer

**David Lopez**  
Email: `davidrlopezd@gmail.com`

\---

## 18\. License and use

This project is submitted for academic coursework. If a public GitHub repository is used, add a license file only if reuse by others is intended.

Recommended options:

* No license file: keeps reuse rights reserved by default.
* MIT License: allows broad reuse with attribution.
* CC BY 4.0: useful for academic writing and documentation.

\---

## 19\. Citation note

If referencing this project, cite it as:

```text
Lopez, David. "Do Presidents Govern As They Speak? A Text-as-Data Analysis of Presidential Rhetoric and Executive Action." DS-GA 1015 Text as Data, New York University, 2026.
```

