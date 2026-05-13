# READMEFIRST — Do Presidents Govern As They Speak?

**Author:** David Lopez  
**Course:** DS-GA 1015 — Text as Data  
**Project type:** Reproducible text-as-data research notebook  
**Main notebook:** `David Lopez_Do_Presidents_Govern_As_They_Speak_Notebook.ipynb`

---

## 1. What this project does

This project asks:

> **Do U.S. presidents govern consistently with the ideological positions they express publicly?**

The notebook builds two text corpora:

- **Say corpus:** public presidential speech, including interviews, inaugural addresses, farewell addresses, speeches, and news conferences when available.
- **Do corpus:** formal presidential action, mainly executive orders and written presidential orders.

The project then places each president twice in a two-axis ideological space:

- **X-axis:** left ↔ right
- **Y-axis:** libertarian ↔ authoritarian

Each president receives:

1. a **Say position**, based on public rhetoric;
2. a **Do position**, based on governing action;
3. a **Say–Do gap**, calculated as the geometric distance between those two positions.

A smaller gap means the president’s words and actions are more aligned. A larger gap means the president’s rhetoric and formal actions are farther apart.

---

## 2. What to open first

For a fast review, open these files in this order:

1. **Final PDF report**  
   Read this first for the written argument, methodology, results, and conclusion.

2. **`READMEFIRST.md`**  
   This file explains how the replication package is organized.

3. **`David Lopez_Do_Presidents_Govern_As_They_Speak_Notebook.ipynb`**  
   This is the full reproducible notebook.

4. **`process_outputs/dictionary_based_full_outputs_FINAL.xlsx`**  
   Main president-level outputs.

5. **`process_outputs/gap_explanation_outputs/say_do_gap_explanation_workbook.xlsx`**  
   Explanation tables showing which phrase families drive the largest Say–Do gaps.

6. **Key figures**
   - `process_outputs/say_do_gap_FINAL.png`
   - `process_outputs/say_do_gap_ranked_FINAL.png`
   - `process_outputs/party_say_do_gap_FINAL.png`
   - `process_outputs/gap_explanation_outputs/top_family_deltas_largest_gaps.png`

---

## 3. Repository structure

Recommended GitHub structure:

```text
.
├── READMEFIRST.md
├── David Lopez_Do_Presidents_Govern_As_They_Speak_Notebook.ipynb
├── requirements.txt
├── final_report.pdf
├── presidents_say_do_corpus_output/
│   ├── full_say_do_document_corpus.csv
│   ├── full_say_do_chunked_audit.csv
│   ├── say_document_corpus.csv
│   ├── do_document_corpus.csv
│   └── corpus_visualizations/
│       ├── 01_corpus_composition_by_document_type_words.png
│       ├── 02_say_vs_do_total_words.png
│       ├── 04_words_per_president_say_do_proportions.png
│       ├── 05_timeline_coverage_total_words_by_year.png
│       ├── 05_timeline_coverage_total_words_by_decade.png
│       └── 06_document_length_distribution_by_document_type.png
├── process_outputs/
│   ├── say_document_corpus.csv
│   ├── do_document_corpus.csv
│   ├── president_evidence_filter_table.csv
│   ├── ideological_phrase_dictionary_FINAL.csv
│   ├── ideological_phrase_dictionary_FINAL.xlsx
│   ├── dictionary_president_corpus_scores_FINAL.csv
│   ├── dictionary_say_do_gap_scores_FINAL.csv
│   ├── dictionary_based_full_outputs_FINAL.xlsx
│   ├── say_do_gap_FINAL.png
│   ├── say_do_gap_ranked_FINAL.png
│   ├── party_dictionary_corpus_scores_FINAL.csv
│   ├── party_say_do_gap_scores_FINAL.csv
│   ├── party_based_full_outputs_FINAL.xlsx
│   ├── validation_outputs/
│   │   ├── dictionary_validation_audit_workbook.xlsx
│   │   ├── president_validation_summary.csv
│   │   ├── top_phrase_families_by_president_corpus_axis.csv
│   │   └── top_variants_by_president_corpus_axis.csv
│   └── gap_explanation_outputs/
│       ├── president_gap_axis_decomposition.csv
│       ├── president_family_axis_contribution.csv
│       ├── president_say_do_family_delta_explanation.csv
│       ├── top_president_gap_explanations.csv
│       └── say_do_gap_explanation_workbook.xlsx
└── raw_chunked_files/
    ├── us_presidents_interviews_*_chunked.xlsx
    ├── us_presidents_inaugural_addresses_chunked.xlsx
    ├── us_presidents_farewell*_chunked.xlsx
    ├── us_presidents_news_conferences*_chunked.xlsx
    ├── us_presidents_executive_orders_*_chunked.xlsx
    └── us_presidents_written_presidential_orders*_chunked.xlsx
```

The exact folder names may differ slightly depending on how the files are packaged. The notebook uses relative paths and recursive file search where possible.

---

## 4. Data source

The source texts are scraped from **The American Presidency Project**:

```text
https://www.presidency.ucsb.edu/
```

The notebook includes scraping code for:

- presidential interviews;
- farewell addresses;
- inaugural addresses;
- executive orders;
- news conferences.

The scraped files are saved as Excel workbooks with two tabs:

```text
interviews
transcript_chunks
```

Even when the document type is not literally an interview, the notebook expects this same two-sheet format for consistency.

---

## 5. Environment setup

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

---

## 6. How to reproduce the project

### Option A — fastest replication

Use this option if the replication package already includes the scraped `.xlsx` files and generated outputs.

1. Download or clone the repository.
2. Open the repository folder.
3. Install the dependencies.
4. Open:

```text
David Lopez_Do_Presidents_Govern_As_They_Speak_Notebook.ipynb
```

5. Run the notebook from top to bottom.
6. Review the outputs in:

```text
presidents_say_do_corpus_output/
process_outputs/
```

### Option B — full replication from raw scraping

Use this option only if the raw scraped files are missing or need to be regenerated.

1. Open the notebook.
2. Run the scraping sections first:
   - Scrape Data — Interviews
   - Scrape Data — Farewell Address
   - Scrape Data — Inaugural
   - Scrape Data — Executive Orders
   - Scrape Data — News Conferences
3. Then run the corpus-building section.
4. Then run the preprocessing and scoring sections.

Important: the scraper uses a delay between requests. This is intentional and helps avoid making too many requests too quickly.

---

## 7. Notebook run order

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

---

## 8. Main methodology

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
NGRAMS_TO_RUN = [2, 3, 4]
MIN_COUNT = 5
TOP_N = 50
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
intensity_0_to_5
theme
variant
```

### Step 5 — Score presidents

The scoring method counts dictionary phrase hits in each president’s Say and Do corpora.

Main settings:

```text
SCORING_MODE = document_presence_with_variant_and_family_caps
MIN_DICTIONARY_HITS_PER_CORPUS = 25
VARIANT_DOCUMENT_HIT_CAP = 25
FAMILY_HIT_CAP = 100
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

---

## 9. Main outputs

### Corpus outputs

```text
presidents_say_do_corpus_output/full_say_do_document_corpus.csv
presidents_say_do_corpus_output/full_say_do_chunked_audit.csv
presidents_say_do_corpus_output/presidents_say_do_corpus_summary.xlsx
```

### Preprocessed corpora

```text
process_outputs/say_document_corpus.csv
process_outputs/do_document_corpus.csv
process_outputs/president_evidence_filter_table.csv
```

### Dictionary outputs

```text
process_outputs/ideological_phrase_dictionary_FINAL.csv
process_outputs/ideological_phrase_dictionary_FINAL.xlsx
process_outputs/ideological_phrase_dictionary_LOOKUP_SORTED.csv
process_outputs/ideological_phrase_dictionary_axis_audit.csv
process_outputs/ideological_phrase_dictionary_family_audit.csv
```

### President-level scoring outputs

```text
process_outputs/dictionary_president_corpus_scores_FINAL.csv
process_outputs/dictionary_say_do_gap_scores_FINAL.csv
process_outputs/dictionary_based_full_outputs_FINAL.xlsx
process_outputs/president_number_legend_mapping_FINAL.csv
```

### Validation outputs

```text
process_outputs/validation_outputs/dictionary_validation_audit_workbook.xlsx
process_outputs/validation_outputs/president_validation_summary.csv
process_outputs/validation_outputs/top_phrase_families_by_president_corpus_axis.csv
process_outputs/validation_outputs/top_variants_by_president_corpus_axis.csv
```

### Gap explanation outputs

```text
process_outputs/gap_explanation_outputs/president_gap_axis_decomposition.csv
process_outputs/gap_explanation_outputs/president_family_axis_contribution.csv
process_outputs/gap_explanation_outputs/president_say_do_family_delta_explanation.csv
process_outputs/gap_explanation_outputs/top_president_gap_explanations.csv
process_outputs/gap_explanation_outputs/say_do_gap_explanation_workbook.xlsx
```

### Party-level outputs

```text
process_outputs/party_dictionary_corpus_scores_FINAL.csv
process_outputs/party_say_do_gap_scores_FINAL.csv
process_outputs/party_president_mapping_FINAL.csv
process_outputs/party_based_full_outputs_FINAL.xlsx
```

---

## 10. Key figures

```text
presidents_say_do_corpus_output/corpus_visualizations/01_corpus_composition_by_document_type_words.png
presidents_say_do_corpus_output/corpus_visualizations/02_say_vs_do_total_words.png
presidents_say_do_corpus_output/corpus_visualizations/04_words_per_president_say_do_proportions.png
presidents_say_do_corpus_output/corpus_visualizations/05_timeline_coverage_total_words_by_year.png
presidents_say_do_corpus_output/corpus_visualizations/05_timeline_coverage_total_words_by_decade.png
presidents_say_do_corpus_output/corpus_visualizations/06_document_length_distribution_by_document_type.png

process_outputs/say_corpus_numbered_markers_FINAL_full.png
process_outputs/do_corpus_numbered_markers_FINAL_full.png
process_outputs/say_corpus_numbered_markers_FINAL_zoom_2_5.png
process_outputs/do_corpus_numbered_markers_FINAL_zoom_2_5.png
process_outputs/say_do_gap_FINAL.png
process_outputs/say_do_gap_ranked_FINAL.png

process_outputs/party_say_corpus_markers_FINAL.png
process_outputs/party_do_corpus_markers_FINAL.png
process_outputs/party_say_do_gap_FINAL.png
process_outputs/party_say_do_gap_ranked_FINAL.png

process_outputs/validation_outputs/top_family_contributions_largest_gaps.png
process_outputs/validation_outputs/dictionary_coverage_by_president_corpus.png

process_outputs/gap_explanation_outputs/gap_axis_decomposition_ranked.png
process_outputs/gap_explanation_outputs/top_family_deltas_largest_gaps.png
```

---

## 11. Expected sanity-check results

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

---

## 12. Reproducibility notes

To make the project reproducible:

- Keep the notebook, raw scraped files, and outputs together.
- Do not rename the key output folders unless the notebook is updated.
- Run the notebook from the repository root.
- Use the same Python environment when possible.
- Include the generated `.csv`, `.xlsx`, and `.png` outputs in the submitted replication package.
- Keep the raw chunked `.xlsx` files so the project can be rerun without scraping.
- If scraping is rerun later, results may change slightly because the source website may update.

---

## 13. Troubleshooting

### `FileNotFoundError`

Make sure the raw chunked Excel files are inside the repository folder or a subfolder. The notebook searches recursively from the current working directory.

### `Missing sheet: interviews` or `Missing sheet: transcript_chunks`

Each raw Excel workbook must contain these two sheets:

```text
interviews
transcript_chunks
```

### `No corpus dataframe found`

Run the corpus-building and preprocessing sections before running n-gram discovery.

### `No presidents remain after the minimum dictionary-hit filter`

This means the dictionary-hit threshold is too strict for the available data. The notebook currently uses:

```text
MIN_DICTIONARY_HITS_PER_CORPUS = 25
```

### OneDrive or Windows file-locking issues

If Excel files are open while the notebook runs, close them first. The notebook copies files to a temporary folder to reduce OneDrive locking problems.

### Very slow scraping

This is expected. The scraping cells use a delay between requests. For normal grading or review, use the included raw `.xlsx` files instead of scraping again.

---

## 14. Suggested `requirements.txt`

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

---

## 15. Suggested `.gitignore`

Use this to avoid uploading temporary or machine-specific files:

```gitignore
.ipynb_checkpoints/
__pycache__/
*.pyc
.DS_Store
Thumbs.db
~$*.xlsx
presidents_say_do_temp/
*.pkl
```

Do **not** ignore the final `.csv`, `.xlsx`, or `.png` outputs if those files are part of the required replication package.

---

## 16. Suggested GitHub submission checklist

Before sharing the repository URL, confirm that:

- [ ] `READMEFIRST.md` is in the root folder.
- [ ] The final PDF report is included.
- [ ] The notebook opens correctly on GitHub.
- [ ] The raw chunked data files are included or clearly linked.
- [ ] `process_outputs/` is included.
- [ ] `presidents_say_do_corpus_output/` is included.
- [ ] The main figures open from GitHub.
- [ ] The Excel workbooks open correctly.
- [ ] No private API keys, passwords, or personal files are included.
- [ ] The repository is public or shared with the professor.
- [ ] The professor can click the repository URL directly.

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

---

## 17. Maintainer

**David Lopez**  
Email: `davidrlopezd@gmail.com`

---

## 18. License and use

This project is submitted for academic coursework. If a public GitHub repository is used, add a license file only if reuse by others is intended.

Recommended options:

- No license file: keeps reuse rights reserved by default.
- MIT License: allows broad reuse with attribution.
- CC BY 4.0: useful for academic writing and documentation.

---

## 19. Citation note

If referencing this project, cite it as:

```text
Lopez, David. "Do Presidents Govern As They Speak? A Text-as-Data Analysis of Presidential Rhetoric and Executive Action." DS-GA 1015 Text as Data, New York University, 2026.
```
