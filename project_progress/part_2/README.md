# Part 2 – Indexing and Evaluation (IRWA Final Project)

This folder contains the Part 2 code: an inverted index over the fashion catalogue, conjunctive (AND) search with TF-IDF ranking, the candidate lists for the five test queries, and the evaluation of the two validation queries with seven metrics.

## Contents
- part2_indexing.ipynb: Main notebook. Builds the index, runs the AND search, writes the candidate list for the test queries, and computes the metrics on the validation queries.
- IRWA-2026-u233460-u232682-u233565-part-2.pdf:	Part 2 report with index and search, validation metrics, analysis of the metrics and limitations, relevance judgements, and use of AI tools.

## Data and paths

- The dataset, the validation labels and the judgements are too large for GitHub and are not committed. The data/ folder is listed in .gitignore.
- The notebooks use paths relative to project_progress/part_2/.

## Requirements and how to run
- Python 3.12, with `pip install numpy pandas nltk` (the notebook downloads the NLTK stop words).
- Considering `fashion_products_dataset.json` and `validation_labels.csv`, open `part2_indexing.ipynb` and run all cells from top to bottom (the preprocessing code is copied from Part 1).
- Output: `data/test_query_candidates.csv` (top 20 results of each of the five test queries).

## Design decisions
- Document id = `pid`. Title, description and product_details are merged into one bag of terms (same pre-processing as Part 1).
- Conjunctive (AND) search: a product must contain all query terms. Ranking: TF-IDF, idf = ln(N/df), term frequency normalised by the document norm.

## Evaluation protocol
- K = 10. Metrics: P@K, R@K, AP@K, F1@K, MAP, MRR, NDCG.
- For each validation query, the TF-IDF ranking is restricted to the 20 labelled products; unlabelled products are ignored.
- P@K divides by K even when fewer than K products are retrieved. R@K uses all relevant labelled products as denominator, including those the AND filter does not retrieve.

## Team and delivery
Carla Royo Gómez (u233460), Ingrid Sigró Alonso (u232682), Rita Alonso Casablancas (u233565). Git tag: `IRWA-2026-part-2`.
