# Part 3 – Ranking and Filtering (IRWA Final Project)

This folder contains the Part 3 code: conjunctive (AND) retrieval ranked with TF-IDF + cosine, BM25, our own score and Word2Vec + cosine; the top-20 lists of the five test queries; the comparison of the rankings; and the evaluation on the two validation queries.

## Contents
- `part3_ranking.ipynb`: main notebook. Builds the index, implements the four rankers, writes the top-20 files, compares the methods and computes the metrics.
- `IRWA-2026-u233460-u232682-u233565-part-3.pdf`: Part 3 report.

## Data and paths
- The dataset and the validation labels are not committed (`data/` is in `.gitignore`). Place `fashion_products_dataset.json` and `validation_labels.csv` in `data/` at the repository root.
- The notebook uses paths relative to `project_progress/part_3/` (`DATA_PATH`, `LABELS_PATH`, `OUT_DIR` in the first code cell).

## Requirements and how to run
- Python 3.12 with `pip install numpy pandas nltk gensim` (the notebook downloads the NLTK stop words).
- Open `part3_ranking.ipynb` and run all cells from top to bottom (the pre-processing code is copied from Part 1 and the index from Part 2).
- Outputs (written to `data/`): `part3_top20_tfidf.csv`, `part3_top20_bm25.csv`, `part3_top20_custom.csv`, `part3_top20_word2vec.csv` (top 20 of each of the five test queries for each method).

## How to choose the ranking method and the options
- Every method is a function `rank_<method>(query)` that returns `[(pid, score), ...]` for the AND matches, best first: `rank_tfidf`, `rank_bm25`, `rank_custom`, `rank_word2vec`.
- `show_top(query, method, top=20)` prints the ranking of any query with any method (`"tfidf"`, `"bm25"`, `"custom"`, `"word2vec"`), e.g. `show_top("men slim jeans blue", "bm25")`.
- BM25 parameters: `K1`, `B` (defaults 1.2 and 0.75).
- Our own score: weights in `CUSTOM_WEIGHTS` (`text`, `title`, `rating`, `discount`) and `OUT_OF_STOCK_FACTOR`.
- Word2Vec: hyper-parameters in the `Word2Vec(...)` call (100 dimensions, window 5, min_count 2, skip-gram, 15 epochs, fixed seed, one worker for reproducibility).

## Design decisions
- Retrieval is conjunctive: a product must contain all the query terms; all methods rank the same set of matches, only the order changes.
- TF-IDF: `(1 + ln tf) * ln(N/df)`, cosine with the norm of the whole document vector (Part 2 normalised raw term frequencies only).
- BM25: Okapi with `k1 = 1.2`, `b = 0.75`, idf `ln(1 + (N - df + 0.5) / (df + 0.5))`.
- Own score: normalised BM25 + title coverage + rating + discount, multiplied by 0.5 for out-of-stock products (details and justification in the report).
- Word2Vec: trained on the pre-processed corpus; text vector = average of its word vectors; cosine between query and document vectors.
- Evaluation: same protocol as Part 2 (K = 10, ranking restricted to the labelled products).

## Team and delivery
Carla Royo Gómez (u233460), Ingrid Sigró Alonso (u232682), Rita Alonso Casablancas (u233565). Git tag: `IRWA-2026-part-3`.
