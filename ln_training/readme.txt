Indonesia Nickel — ML Classification Pipeline

## NB1 — Labeled Data Preparation
Loads and explores the manually coded snippet dataset (~589 labeled snippets from 153 newspaper articles). 
Parses and visualizes the distribution of code categories, produces co-occurrence heatmaps across Actor categories, Character Roles, and Conflict types, and analyzes snippet structure (word counts). Builds the labeled training matrix with binary conflict-type columns used as input for model training.

## NB2 — Unlabeled Data Preparation
Loads the full LexisNexis article dataset (2,334 articles), excludes the 153 articles already used for labeling, and splits the remaining 2,181 articles 
into ~83,000 snippets using a sentence-grouped sliding window approach (target: 60–80 words, one-sentence overlap). 
Includes sanity checks on snippet length distribution and a keyword co-occurrence analysis (China, Indonesia, Nickel).
TO DO: exclude more articles ex ante.

## NB3A — Conflict Codes Training
Fine-tunes a DistilBERT model on the 5 conflict type classes 
(Environmental & Health, Labour & Social, Governance & Corruption, Economic & Industrial, Geopolitical & Strategic) using the labeled snippets from NB1. 
Evaluates on a held-out validation set and applies the trained model to all 83k unlabeled snippets, saving predictions and probability scores to CSV.

## NB3B — Actor Codes Training
Fine-tunes a DistilBERT model for actor-related classification using the same labeled dataset and inference pipeline as NB3A. 
Intended as a parallel track to NB3A; actor identification may also be complemented by a dedicated NER approach.
