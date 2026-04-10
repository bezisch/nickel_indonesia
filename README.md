Structure of the subfolder ln_training: 

NB1 loads the manually coded dataset (~590 labeled snippets drawn from 153 newspaper articles), explores the distribution of codes, and builds the binary training matrix used by the three training notebooks.

NB2 takes the full LexisNexis corpus (2,334 articles), removes the 153 articles already used for labeling, and splits the remaining 2,181 articles into roughly 83,000 snippets using a sliding window approach (target length 60-80 words, one-sentence overlap). This unlabeled pool is the inference target for the trained models.

NB3A fine-tunes a DistilBERT model as a multi-label classifier on the 5 conflict type classes (Environmental & Health, Labour & Social, Governance & Corruption, Economic & Industrial, Geopolitical & Strategic). It uses binary cross-entropy loss, an 80/20 train/validation split, macro F1 as the evaluation metric. 
After training, the model is applied to the full 83k snippet pool. 

NB3B identifies actor categories using two complementary approaches: a fine-tuned DistilBERT classifier following the same setup as NB3A, and a rule-based extraction method that matches named entities and trigger phrases against a manually built actor codebook.

NB3C covers character role codes (not started yet).

