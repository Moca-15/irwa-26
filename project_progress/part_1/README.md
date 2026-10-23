## Part 1 - Text Processing and Exploratory Data Analysis
Carla Royo Gómez (u233460)
Ingrid Sigró Alonso(u232682)
Rita Alonso Casablancas (u233565)

This folder contains the Part 1 deliverables of the IRWA final project.

- **irwa-part1.ipynb** is the code for text pre-processing (Part 1) and exploratory data analysis (Part 2 of the assignment).
- **IRWA-2026-u233460-u232682-u233565-part-1.pdf** is the report with the decisions, assumptions, and results.

### Data

The data files are not in the GitHub repository, because the dataset is too large to upload, so you must change them before running the notebook. Use the full path, including the file name. 

### Content
#### Part 1 – Data preparation

Text pre-processing: lowercasing, tokenization, punctuation removal, NLTK stop words, Porter stemming.
Output fields: the 14 fields every result must return, with pid kept for evaluation.
Categorical fields: brand, category, sub_category, seller as normalised labels; product_details flattened to text.
Numeric fields: prices, discount, rating and stock parsed to numbers and kept as metadata.
Applying the pipeline to all 28,080 products.

#### Part 2 – Exploratory data analysis

Missing values, text lengths, sentences, vocabulary before and after processing, most frequent terms, word cloud, categories and brands, prices, ratings, discounts and stock, rankings, named entities, and the analysis of the validation labels.
