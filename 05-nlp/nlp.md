#### Document-Term Matrix (DTM)

A Document-Term Matrix (DTM) in NLP is a mathematical structure representing a corpus, where rows represent documents and columns represent unique terms (words). Each cell contains the count or weight (e.g., TF-IDF) of a term in a document, enabling quantitative analysis of unstructured text data.

Key Characteristics and Components
Structure: Documents are usually rows, and terms are columns (or vice versa in a Term-Document Matrix).
Sparsity: Because not every word appears in every document, DTMs are often sparse, containing mostly zeros.
Vectorization: It converts text into numerical, high-dimensional vectors, allowing algorithms to process documents.
Weighting: Cells can contain raw counts (Bag of Words) or weighted values like Term Frequency-Inverse Document Frequency (TF-IDF) to highlight meaningful words.

Applications in NLP
Topic Modeling: Discovering hidden thematic structures in documents.
Text Classification: Categorizing documents based on word frequencies.
Search & Information Retrieval: Improving search results by identifying relevant documents.
Dimensionality Reduction: Techniques like Singular Value Decomposition (SVD) are used to handle high sparsity.

Limitations
Ignores Context: The order of words and grammatical structure are lost, treating documents as "bags of words".
High Dimensionality: As the vocabulary size increases, the matrix becomes extremely large, requiring significant memory.

**Stop words in NLP**
Stop words in NLP are common, high-frequency words (e.g., "the," "is," "in," "and") filtered out during text preprocessing to reduce noise, improve computational efficiency, and focus on meaningful content. They are typically ignored in tasks like sentiment analysis, search indexing, and topic modeling.

Key Aspects of Stop Words:
Definition: Words that carry little unique information, such as articles, prepositions, and conjunctions.
Purpose: Removing them reduces dataset size, lowers computational load, and helps algorithms focus on important terms.
Examples: "a," "an," "the," "is," "in," "on," "of," "and," "but".
When to Keep: Removing them can destroy context or meaning (e.g., in sentiment analysis, "not" is a crucial stop word).
Implementation: Libraries like NLTK and spaCy provide default lists that can be customized.

Example:
Original: "The quick brown fox jumps over the lazy dog."
After Stop Word Removal: "quick brown fox jumps lazy dog."

#### N-gram

An N-gram is a contiguous sequence of
items (typically words or characters) from a given sample of text or speech. In Natural Language Processing (NLP), an N-gram model is a probabilistic language model that predicts the next item in a sequence based on the previous
items.
Types of N-Grams
The value of
defines the order of the model:
Unigram (
): Single words (e.g., "Natural", "Language", "Processing").
Bigram (
): Pairs of consecutive words (e.g., "Natural Language", "Language Processing").
Trigram (
): Triplets of consecutive words (e.g., "Natural Language Processing").
4-gram, 5-gram, etc.: Higher-order sequences.
Core Concept: The Markov Assumption
Calculating the probability of a word given its entire preceding history is computationally expensive and data-intensive. N-gram models simplify this using the Markov Assumption, which states that the probability of a word depends only on a limited window of previous words. For example, a Bigram model assumes:

Common Applications
Text Prediction: Powering autocomplete functions in search engines and mobile keyboards.
Speech Recognition: Helping systems choose the most likely sequence of words from noisy audio.
Spelling Correction: Identifying the most probable word in a specific context (e.g., correcting "in fifteen minuets" to "minutes").
Machine Translation: Ensuring generated sentences follow natural word patterns in the target language.
Plagiarism Detection: Identifying overlapping sequences of words across different documents.
Challenges and Solutions
Data Sparsity: As
increases, many perfectly valid word sequences may not appear in the training data, resulting in zero probabilities.
Smoothing: Techniques like Laplace (Add-one) Smoothing or Kneser-Ney Smoothing are used to assign non-zero probabilities to unseen N-grams.
Storage Limitations: The number of possible N-grams grows exponentially with
, leading to high memory overhead.
Limited Context: Unlike modern Transformers, N-grams cannot capture long-range dependencies because they only "see" the last few words.

#### skipgrams

skip-grams are a way of looking at pairs of words in a sentence while skipping over some words in between.
They help NLP models understand context even when words aren't sitting right next to each other.

1. How they work (The Visual)
   Imagine the sentence: "The cat sat on the mat."
   Standard Bigram (No skips): You only look at neighbors.
   ("The", "cat"), ("cat", "sat"), ("sat", "on")...
   1-Skip-Bigram: You are allowed to skip one word to find a pair.
   ("The", "sat"), ("cat", "on"), ("sat", "the")...
   By allowing these "skips," the model learns that "cat" and "sat" are related, but it also learns that "cat" and "on" have a relationship in the sentence structure.
2. Two Main Uses in NLP
   A. In Word Embeddings (Word2Vec)
   The Skip-gram model is a famous architecture where you pick a target word and try to predict the context words around it.
   Goal: If I give the model the word "Apple," the skip-gram training helps the model predict "juice," "iPhone," or "fruit" as likely neighbors.
   B. In Evaluation (ROUGE-S)
   As we discussed earlier, ROUGE-S uses skip-bigrams.
   The Benefit: It is much more flexible than BLEU. If a human says "The quick brown fox" and the AI says "The brown fox," a standard bigram count would fail to see a match for "quick" and "fox." A skip-bigram would still find the match ("The", "fox") because it's allowed to skip the word "brown."
