# Natural Language Processing (NLP)

Natural Language Processing (NLP) is a branch of artificial intelligence (AI) that enables computers to understand, interpret, and generate human language, bridging the gap between human communication and computer comprehension. It uses algorithms to analyze text and speech, automating tasks like sentiment analysis, translation, and text summarization.

**It involves multiple key steps,**

- Preprocessing: Cleaning data through tokenization (breaking text into words), stemming/lemmatization (reducing words to root forms), and removing stop words.
- Syntax/Parsing: Analyzing grammatical structure to understand relationships between words.
- Semantic Analysis: Using techniques like word-sense disambiguation to understand the intended meaning of words based on context.
- Named Entity Recognition (NER): Identifying key elements like names, locations, and organizations.
- Natural Language Generation (NLG): Producing human-like text from structured data.

**How It Works**
NLP combines linguistics (language rules) with machine learning algorithms. It treats language as data, processing inputs through several stages—including phonology, morphology, and pragmatics—to produce meaningful output.

Here are some common applications

- Virtual Assistants: Siri, Alexa, and Google Assistant.
  Machine Translation: Google Translate.
- Sentiment Analysis: Determining if social media posts or reviews are positive or negative.
- Text Summarization/Generation: Chatbots and automated reporting.
- Healthcare/Business: Analyzing patient records or automating document analysis.

---

## NLP applications

NLP in social media transforms vast amounts of unstructured user data into actionable insights for marketing, security, and research.

**Here are some key applications,**

- Sentiment Analysis: Gauges the emotional tone (positive, negative, neutral) of posts to monitor brand reputation, track campaign effectiveness, and understand public opinion.
- Social Listening & Brand Monitoring: Tracks brand mentions, competitor activities, and industry shifts in real-time, even when the brand isn't directly tagged.
- Topic Modeling & Trend Detection: Automatically identifies emerging themes and popular hashtags to help businesses adapt to shifting consumer interests.
- Threat Intelligence: Detects harmful content, including cyberbullying, hate speech, extremist content, and misinformation.
- Mental Health Surveillance: Analyzes linguistic patterns to identify signs of depression, anxiety, or potential crises in users.
- Customer Service Automation: Powers 24/7 chatbots that resolve routine queries and route complex issues to human agents.

**But there are some major challenges,**

- Informal Language & Noise: Social media text is rife with slang, abbreviations (e.g., "u" for "you"), misspellings, lack of punctuation, and emoticons, which can confuse traditional NLP models.
- Sarcasm & Ambiguity: Determining the true meaning of a post is difficult when the tone is ironic or sarcastic (e.g., "Great job!" as a complaint).
- Contextual Nuance: Meaning often depends on short, sparse contexts (like a 280-character tweet) or external real-world events that models may not know.
- Multilingualism: Data frequently spans multiple languages or uses code-switching (mixing languages), requiring robust cross-lingual capabilities.
- Data Scalability: The sheer volume and speed of social media data require high-performance architectures to process information in real-time without lag.
- Ethical & Privacy Issues: Handling user-generated data requires strict compliance with regulations (like GDPR) and constant effort to mitigate algorithmic bias.

---

## What is an end to end NLP pipeline?

An end-to-end NLP pipeline transforms raw, unstructured text into structured, actionable insights. While specific steps vary by task, the standard industry workflow follows this sequence:

**1. Data Acquisition & Collection**
The foundation of the pipeline.

- Sources: Web scraping, APIs (Twitter/X, Reddit), SQL databases, PDF/OCR scanning, or internal logs.
- Storage: Raw data is typically stored in a "Data Lake" (e.g., AWS S3) before processing.

**2. Text Pre-processing (Cleaning)**

- Converting "noisy" text into a standardized format.
  - Cleaning: Removing HTML tags, emojis, URLs, and special characters.
  - Normalization: Lowercasing, fixing spelling errors, and expanding contractions (e.g., "don't" → "do not").
  - Tokenization: Breaking sentences into individual words or sub-word units.
- Linguistic Refinement:
  - Stop-word Removal: Deleting high-frequency, low-value words (e.g., "the", "is").
  - Lemmatization/Stemming: Reducing words to their root form (e.g., "running" → "run").

**3. Feature Engineering & Vectorization**
Translating text into numbers that a machine can understand.

- Statistical: TF-IDF or Count Vectorizers (Bag-of-Words).
- Static Embeddings: Word2Vec, GloVe (capturing basic semantic relationships).
- Dynamic Embeddings: Contextual vectors from Transformers like BERT or RoBERTa (understanding that "bank" means different things in "river bank" vs. "bank account").

**4. Model Training & Fine-Tuning**
Selecting the brain of the pipeline.

- Traditional ML: Naive Bayes, Logistic Regression, or Support Vector Machines for speed and small datasets.
- Deep Learning: Training Hugging Face Transformers or LSTMs for complex language tasks.
- Fine-Tuning: Taking a pre-trained model (like GPT or BERT) and training it on your specific domain data (e.g., medical or legal).

**5. Evaluation & Optimization**
Testing the model against unseen data.

- Metrics: Accuracy, Precision, Recall, F1-Score, or ROUGE/BLEU for text generation.
- Error Analysis: Identifying where the model fails (e.g., struggling with sarcasm or specific entities).
- Hyperparameter Tuning: Using tools like Optuna to find the best model settings.

**6. Deployment & Monitoring (MLOps)**
Moving the model into production.

- Serving: Wrapping the model in an API using FastAPI or Flask.
- Inference Optimization: Speeding up the model using ONNX Runtime or Quantization.
- Monitoring: Tracking "Data Drift" (when real-world language changes over time) and performance degradation.

**7. Human-in-the-Loop (Optional but Recommended)**
A feedback loop where humans review uncertain model predictions to continuously improve the system through active learning.

---

## What are some NLP preprocessing techniques?

NLP preprocessing transforms raw, messy text into a structured format to improve model performance and accuracy.

**Here are some fundamental cleaning & normalization**

- Sentence Segmentation: Breaking a body of text into individual sentences, typically using punctuation like periods as delimiters.
- Word Tokenization: Splitting a sentence into smaller units called "tokens" (words, numbers, or symbols).
- Lowercasing: Converting all characters to lowercase to ensure consistency, treating "Apple" and "apple" as the same word.
- Removing Digits/Punctuation: Deleting numerical values and special characters that do not contribute to semantic meaning.
- Stop Word Removal: Filtering out frequent but low-value words like "the," "is," or "in" to focus on meaningful content.
- Stemming: A fast, rule-based method that chops off suffixes to find a word's root (e.g., "running" "run"), though the result may not be a valid word.
- Lemmatization: A context-aware process that returns a word to its dictionary form (lemma) using linguistic rules (e.g., "better" "good").
- Normalization: Converting text into a canonical standard, such as expanding contractions ("don't" "do not") or standardizing varied spellings of the same word.

**Linguistic Identification & Handling**

- Language Detection: Identifying the primary language of the text to ensure the correct subsequent NLP models are applied.
- Code Mixing: Processing text where two or more languages are blended within a single sentence (e.g., "Hinglish"), which is common in social media.
- Transliteration: Converting text from one script to another based on phonetic similarity (e.g., writing Hindi words using English characters).

**Syntactic & Semantic Analysis**

- POS Tagging (Part-of-Speech): Labeling each word with its grammatical category, such as noun, verb, or adjective, to understand sentence structure.
- Parsing: Analyzing the grammatical structure of a sentence to establish relationships between "head" words and their modifiers (Dependency Parsing).
- Coreference Resolution: Identifying when different words or phrases (like "he" and "John") refer to the same entity in a text.

---

## What is feature engineering in NLP?

In NLP, feature engineering is the art of converting text into numerical representations (vectors) that machine learning algorithms can understand. This ranges from simple word counts to complex contextual embeddings.

**1. Traditional Vectorization (Count-Based)**
These methods focus on the frequency and importance of words within a document.

- **Bag-of-Words (BoW):** Represents text as a simple count of each word's occurrence. It ignores word order and grammar.
- **TF-IDF (Term Frequency-Inverse Document Frequency):** Weights words by how unique they are to a specific document. It penalizes common words (like "the") and highlights distinctive terms.
- **N-Grams:** Captures local context by grouping adjacent words (e.g., Bigrams: "New York"; Trigrams: "Machine Learning Models").

**2. Shallow Embeddings (Static)**
These provide a dense numerical vector for each word, where words with similar meanings are positioned close together in space.

- **Word2Vec:** Uses a shallow neural network to learn word associations (CBOW or Skip-gram models).
- **GloVe (Global Vectors):** Based on global word-word co-occurrence statistics from a large corpus.
- **FastText:** Treats words as a "bag of character n-grams," allowing it to handle out-of-vocabulary words and typos effectively.

**3. Contextual Embeddings (Deep Learning)**
Unlike static embeddings, these change based on the surrounding words (e.g., "bank" in "river bank" vs. "bank account").

- **BERT (Bidirectional Encoder Representations from Transformers):** Uses transformers to read text in both directions, providing deep context.
- **RoBERTa/ELMo:** Advanced variations that capture nuanced semantic and syntactic information.

**4. Structural & Linguistic Features**
Sometimes, manual "meta-features" provide a significant boost for specific tasks:

- **Syntactic Features:** Word counts, sentence length, or the ratio of nouns to verbs.
- **Entity Features:** Presence of Named Entities (NER) like locations, dates, or organizations.
- **Sentiment Scores:** Using a lexicon like VADER to extract polarity (positive/negative) as a numerical feature.
- **Readability Scores:** Metrics like the Flesch-Kincaid Grade Level to measure text complexity.

**5. Feature Selection & Dimensionality Reduction**
To avoid "the curse of dimensionality" (too many features for the model to handle):

- **PCA (Principal Component Analysis):** Compresses high-dimensional vectors into fewer, high-impact dimensions.
- **Chi-Square Test:** Identifies which words have the strongest statistical relationship with the target label.
- **L1 Regularization (Lasso):** Naturally pushes the coefficients of less important features to zero during training.

---

## Word2Vec

Word2Vec is a technique used to map words into high-dimensional numerical vectors (embeddings) so that computers can understand semantic relationships. It works on the principle that words appearing in similar contexts often have similar meanings.

**1. The Core Mechanism**
Word2Vec is a shallow, two-layer neural network. Instead of using the model for its actual output, we use the weights of the hidden layer as the word vectors.

- **Input:** Words are initially represented as sparse One-Hot Encoded vectors (a long string of 0s with a single 1).
- **Hidden Layer:** This layer "compresses" the large one-hot vector into a smaller, dense vector (e.g., 100 or 300 dimensions).
- **Output:** The model predicts either a target word or its neighbors.

**2. Training Architectures**
There are two primary ways to train the model:

- **Continuous Bag of Words (CBOW):** Predicts a center word based on the surrounding context words. For example, in "The cat [___] on the mat," it tries to predict "sat".
- **Skip-gram:** Predicts the surrounding context words given a single center word. If the input is "sat," the model predicts "cat," "on," "the," etc..

**3. Key Optimizations**
To make training on billions of words efficient, Word2Vec uses two main tricks:

- **Negative Sampling:** Instead of updating the entire vocabulary for every word (which is slow), the model only updates the correct neighbor and a few randomly chosen "negative" (non-neighbor) words.
- **Hierarchical Softmax:** Uses a tree structure to find the most probable words faster than checking every word in the dictionary.

**4. Why It Is Useful**

- **Word Analogies:** Because the vectors capture meaning, you can perform math on them: King - Man + Woman ≈ Queen.
- **Semantic Proximity:** Words like "Paris" and "Berlin" will be mathematically "close" to each other in the vector space.
- **Downstream Tasks:** These vectors serve as powerful inputs for Sentiment Analysis, machine translation, and recommendation systems.

---

## Continuous Bag of Words (CBOW)

Continuous Bag of Words (CBOW) is an architecture in Word2Vec that predicts a single target word (the center word) based on its surrounding context words.

**How it Works**
Think of CBOW as a "fill-in-the-blank" exercise for a neural network.

- **Context Selection:** You define a window size (e.g., 2), which determines how many words before and after the target word are used as context.

- **Aggregation:** The model takes the One-Hot Encoded vectors of all context words and averages or sums them to create a single input for the hidden layer.
- **Prediction:** This averaged input is passed through a hidden layer (the "projection layer") and an output layer that uses a Softmax Activation Function to predict the most likely target word from the entire vocabulary.

**Key Characteristics**

- **Averaging Effect:** Because CBOW averages the context word vectors, it loses information about the order of those words (hence the "Bag of Words" name).
- **Speed:** It is generally faster to train than Skip-gram because it makes one prediction per context window rather than multiple.
- **Frequency Bias:** CBOW tends to perform better and produce more accurate embeddings for frequently occurring words compared to rare ones.

**Example**
If the training sentence is "The cat sat on the mat" and the window size is 2:
Context: ["The", "cat", "on", "the"], Target: "sat"
The model learns to associate the combined meaning of "The," "cat," "on," and "the" with the word "sat".

---

## TF-IDF (Term Frequency-Inverse Document Frequency)

TF-IDF (Term Frequency-Inverse Document Frequency) is a numerical statistic used to rank how "important" a word is to a specific document within a larger collection (corpus).

While Word2Vec focuses on meaning, TF-IDF focuses on uniqueness.

**1. The Two Components**
It is the product of two different measurements:

- **Term Frequency (TF):** How often a word appears in a single document.
  Logic: If a word appears a lot, it’s probably important to that topic.

- **Inverse Document Frequency (IDF):** How rare a word is across the entire collection of documents.
  Logic: Words like "the," "is," or "and" appear everywhere. IDF penalizes these common words and boosts rare, descriptive words (like "photosynthesis" or "arbitrage").

A high score is achieved by having a high term frequency (in the specific document) and a low document frequency of the term in the whole collection.

**4. Practical Example**
If you have 1,000 articles about technology:

- The word "the" will have a high TF but a very low IDF (because it’s in every article), resulting in a low total score.
- The word "blockchain" might appear 20 times in one specific article but only in 5 articles total. This creates a high total score, marking "blockchain" as a key descriptor for that document.

---

## Negative Sampling and Hierarchical Softmax

Both Negative Sampling and Hierarchical Softmax were designed to solve the same problem: the "Big Vocabulary Bottleneck."
In a standard neural network, the output layer has one node for every word in your vocabulary (e.g., 100,000 words). Calculating the Softmax for all 100,000 nodes every time you process a single word is computationally expensive and incredibly slow.

**1. Negative Sampling**
Instead of asking the model to choose the 1 correct word out of 100,000, Negative Sampling turns the problem into a simple Yes/No (Binary) classification.

The idea is that for every "positive" pair (a word and its actual neighbor), pick a small number (e.g., 5 to 20) of "negative" words at random from the dictionary that are not neighbors.

The goal is to train the model to distinguish the real neighbor from the random noise.

**Why it works:** Instead of updating 100,000 weights, the model only updates the weights for the 1 positive word and the 5 negative samples. This makes training massively faster while still producing high-quality vectors.

**2. Hierarchical Softmax (The "Tree Search")**
Hierarchical Softmax uses a binary tree structure (typically a Huffman Tree) to represent the vocabulary.

- The Structure: All the words in the vocabulary are "leaves" at the bottom of the tree. Frequent words are placed on shorter paths, and rare words are deeper.

- The Process: To calculate the probability of a word, the model doesn't look at all words. It traces a path from the root of the tree down to that specific word's leaf.

For a vocabulary of 65,536 words, the model only needs to make 16 binary decisions instead of 65,536 calculations.

---

## BM25 (Best Matching 25)

BM25 (Best Matching 25) is a ranking function used by search engines to estimate the relevance of documents to a given search query. It is widely considered the state-of-the-art for keyword-based (lexical) search and is the default algorithm for Elasticsearch, Lucene, and Solr.

While it shares the core concepts of TF-IDF, it fixes major flaws to provide more intuitive results.

**1. The Core Components**
BM25 calculates a relevance score based on three main signals:

- **Inverse Document Frequency (IDF):** Rare words are more valuable than common ones. For example, in a search for "the asteroid," the term "asteroid" is a much stronger signal than "the".
- **Term Frequency (TF) with Saturation:** In standard TF-IDF, a word appearing 100 times is 10 times "better" than a word appearing 10 times. BM25 introduces saturation: the 10th occurrence matters much less than the 1st, and the 50th occurrence barely changes the score at all.
- **Document Length Normalization:** Longer documents naturally contain more words, increasing the chance of keyword matches by pure coincidence. BM25 penalizes longer documents and rewards shorter, more focused ones that contain the same query terms.

**2. Key Tunable Parameters**
One reason BM25 is so effective is that it can be fine-tuned via two main variables:

- **Saturation Control**: Determines how quickly term frequency reaches saturation. A common default is 1.2. Higher values mean that more occurrences of a word continue to boost the score for longer.

- **Length Normalization**: Controls how strictly the document length is penalized. It ranges from 0 to 1, with 0.75 as a standard default. If 1, full normalization is applied; if 0, length is ignored entirely.

**3. Real Use Cases**

- **Search Engines:** Powering internal searches for e-commerce, legal databases, and enterprise systems.
- **Hybrid Search:** Often paired with Semantic Search (Dense Retrieval) to catch exact keyword matches that AI models sometimes miss.
- **RAG (Retrieval-Augmented Generation):** Used to retrieve the most relevant chunks of text to provide as context for Large Language Models.

---

## GloVe (Global Vectors for Word Representation)

GloVe (Global Vectors for Word Representation) is an unsupervised learning algorithm developed at Stanford University for generating word embeddings.
While Word2Vec is a "predictive" model (predicting neighbors), GloVe is a "count-based" model that looks at the global statistics of the entire dataset at once.

**1. How it Works: The Co-occurrence Matrix**
GloVe starts by building a massive table (matrix) that counts how often every word in your vocabulary appears near every other word.

- The Idea: If "Ice" and "Cold" appear together frequently, their vectors should be close.
- The Global View: Unlike Word2Vec, which only looks at a small local window of words at a time, GloVe analyzes the entire corpus to build this matrix before it starts training.

**2. Ratios of Probabilities**
The genius of GloVe is that it doesn't just look at raw counts; it looks at the ratios of co-occurrence probabilities.

- Example: Consider the words Ice and Steam in relation to Water.
  Ice co-occurs with Solid frequently and Steam co-occurs with Solid rarely.
  The ratio of these probabilities helps the model pinpoint that "Ice" is to "Solid" what "Steam" is to "Gas."

**3. Why use it?**
GloVe is famous for its pre-trained vectors. Because it's trained on massive datasets like Wikipedia and Common Crawl, you don't have to train it yourself. You can simply download the vectors and plug them into your model to give it an "instant" understanding of English.

---

## FastText

FastText, developed by Facebook's AI Research (FAIR) lab, is essentially the "evolution" of Word2Vec. While Word2Vec treats every word as an unbreakable atom, FastText breaks words down into smaller chunks called n-grams.

**1. The Core Innovation: Subword Information**
The biggest difference is that FastText represents a word as the sum of its character n-grams.

Example: For the word “apple” with n = 3 to 6, the n-grams are: <ap, app, ppl, ple, le>, and the whole word <apple>. The final vector for “apple” is the average of all these subword vectors.

**2. Why is this better?**
This "subword" approach solves the two biggest headaches in NLP:

- **Out-of-Vocabulary (OOV) Words:** In Word2Vec, if the model encounters a word it hasn't seen during training (like "bio-robotics"), it fails. FastText can look at the chunks ("bio", "robot", "ics") and guess the meaning of the new word.
- **Morphologically Rich Languages:** In languages like German, Spanish, or Turkish, words change endings based on grammar (e.g., eat, eats, eating, eaten). FastText realizes these words share the same root, whereas Word2Vec treats them as completely different words.

**Use Cases**

- Dirty Data: Great for social media text (Twitter/X) where people use weird spellings or slang.
- Rare Words: Excellent at representing words that only appear once or twice in your text.
- Language Support: Often the best choice for non-English languages with complex word structures.

---

## Document-Term Matrix (DTM)

A Document-Term Matrix (DTM) in NLP is a mathematical structure representing a corpus, where rows represent documents and columns represent unique terms (words). Each cell contains the count or weight (e.g., TF-IDF) of a term in a document, enabling quantitative analysis of unstructured text data.

**Here are some key characteristics and components**

- Structure: Documents are usually rows, and terms are columns (or vice versa in a Term-Document Matrix).
- Sparsity: Because not every word appears in every document, DTMs are often sparse, containing mostly zeros.
- Vectorization: It converts text into numerical, high-dimensional vectors, allowing algorithms to process documents.
- Weighting: Cells can contain raw counts (Bag of Words) or weighted values like Term Frequency-Inverse Document Frequency (TF-IDF) to highlight meaningful words.

**Here are some applications of DTM,**

- Topic Modeling: Discovering hidden thematic structures in documents.
- Text Classification: Categorizing documents based on word frequencies.
- Search & Information Retrieval: Improving search results by identifying relevant documents.
- Dimensionality Reduction: Techniques like Singular Value Decomposition (SVD) are used to handle high sparsity.

**Limitations**

- Ignores Context: The order of words and grammatical structure are lost, treating documents as "bags of words".
- High Dimensionality: As the vocabulary size increases, the matrix becomes extremely large, requiring significant memory.

---

## Stop words in NLP

Stop words in NLP are common, high-frequency words (e.g., "the," "is," "in," "and") filtered out during text preprocessing to reduce noise, improve computational efficiency, and focus on meaningful content. They are typically ignored in tasks like sentiment analysis, search indexing, and topic modeling.

**Here are some key aspects of stop words,**

- Definition: Words that carry little unique information, such as articles, prepositions, and conjunctions.
- Purpose: Removing them reduces dataset size, lowers computational load, and helps algorithms focus on important terms.
- Examples: "a," "an," "the," "is," "in," "on," "of," "and," "but".
- When to Keep: Removing them can destroy context or meaning (e.g., in sentiment analysis, "not" is a crucial stop word).
- Implementation: Libraries like NLTK and spaCy provide default lists that can be customized.

**Example:**
Original: "The quick brown fox jumps over the lazy dog."
After Stop Word Removal: "quick brown fox jumps lazy dog."

---

## N-gram

An N-gram is a contiguous sequence of n items (typically words or characters) from a given sample of text or speech. In Natural Language Processing (NLP), an N-gram model is a probabilistic language model that predicts the next item in a sequence based on the previous items.

**Types of N-Grams**
The value of n defines the order of the model:

- Unigram (n=1): Single words (e.g., "Natural", "Language", "Processing").
- Bigram (n=2): Pairs of consecutive words (e.g., "Natural Language", "Language Processing").
- Trigram (n=3): Triplets of consecutive words (e.g., "Natural Language Processing").
- 4-gram, 5-gram, etc.: Higher-order sequences.

**Core Concept: The Markov Assumption**
Calculating the probability of a word given its entire preceding history is computationally expensive and data-intensive. N-gram models simplify this using the Markov Assumption, which states that the probability of a word depends only on a limited window of previous words.

**Here are some common applications,**

- **Text Prediction:** Powering autocomplete functions in search engines and mobile keyboards.
- **Speech Recognition:** Helping systems choose the most likely sequence of words from noisy audio.
- **Spelling Correction:** Identifying the most probable word in a specific context (e.g., correcting "in fifteen minuets" to "minutes").
- **Machine Translation:** Ensuring generated sentences follow natural word patterns in the target language.
- **Plagiarism Detection:** Identifying overlapping sequences of words across different documents.

**Challenges and Solutions**

1. Data Sparsity: As n increases, many perfectly valid word sequences may not appear in the training data, resulting in zero probabilities.
2. Smoothing: Techniques like Laplace (Add-one) Smoothing or Kneser-Ney Smoothing are used to assign non-zero probabilities to unseen N-grams.
3. Storage Limitations: The number of possible N-grams grows exponentially with n, leading to high memory overhead.
4. Limited Context: Unlike modern Transformers, N-grams cannot capture long-range dependencies because they only "see" the last few words.

---

## Skipgrams

skip-grams are a way of looking at pairs of words in a sentence while skipping over some words in between.
They help NLP models understand context even when words aren't sitting right next to each other.

**1. How they work?**
Imagine the sentence: "The cat sat on the mat."

- Standard Bigram (No skips): You only look at neighbors.
  ("The", "cat"), ("cat", "sat"), ("sat", "on")...
- 1-Skip-Bigram: You are allowed to skip one word to find a pair.
  ("The", "sat"), ("cat", "on"), ("sat", "the")...

By allowing these "skips," the model learns that "cat" and "sat" are related, but it also learns that "cat" and "on" have a relationship in the sentence structure.

**2. Two Main Uses in NLP**

1.  **In Word Embeddings (Word2Vec)**
    The Skip-gram model is a famous architecture where you pick a target word and try to predict the context words around it.
    Goal: If I give the model the word "Apple," the skip-gram training helps the model predict "juice," "iPhone," or "fruit" as likely neighbors.

2.  **In Evaluation (ROUGE-S)**
    As we discussed earlier, ROUGE-S uses skip-bigrams.
    The Benefit: It is much more flexible than BLEU. If a human says "The quick brown fox" and the AI says "The brown fox," a standard bigram count would fail to see a match for "quick" and "fox." A skip-bigram would still find the match ("The", "fox") because it's allowed to skip the word "brown."

---

## Data Augmentation in nlp

In Natural Language Processing (NLP), data augmentation is the practice of artificially increasing the size and diversity of a training dataset by creating modified versions of existing text. Unlike image augmentation (e.g., rotating or flipping), text augmentation is more complex because even minor changes can drastically alter a sentence's meaning or grammatical correctness.

**What are some core techniques?**
Data augmentation methods in NLP are generally categorized by the level at which they operate:
**1. Lexical (Word-level) Augmentation:**

- Synonym Replacement (SR): Randomly replaces words with their synonyms using databases like WordNet.
- Random Insertion (RI): Finds a synonym of a random word and inserts it into a random position in the sentence.
- Random Swap (RS): Randomly chooses two words in a sentence and swaps their positions.
- Random Deletion (RD): Randomly removes words from a sentence based on a defined probability.
- Easy Data Augmentation (EDA): A popular framework that combines the four techniques mentioned above.

**2. Sentence-level Augmentation:**

- Back-Translation: Translates a sentence into another language (e.g., English to French) and then back to the original language to generate a paraphrase.
- Paraphrasing: Uses models like T5 or GPT-2 to rewrite sentences while maintaining original intent.
- Sentence Shuffling: Randomizes the order of sentences within a multi-sentence document.

**3. Character-level Augmentation:**

- Keyboard Error Injection: Simulates common typos by replacing characters with nearby keys on a QWERTY keyboard.
- Random Character Swapping/Deletion: Introduces noise at the character level to improve model robustness against noisy real-world data.

**4. Feature-space Augmentation:**

- Mixup: Interpolates the hidden representations (embeddings) of two different sentences to create a "virtual" training sample.

**Why It's Used?**

- Preventing Overfitting: Helps models generalize better by exposing them to diverse linguistic patterns.
- Addressing Data Scarcity: Useful for training "data-hungry" deep learning models when labeled datasets are small.
- Handling Class Imbalance: Generates extra samples for minority classes to ensure the model doesn't become biased toward the majority class.
- Improving Robustness: Trains models to handle real-world "noise" like typos, slang, and varying sentence structures.

**Several open-source libraries simplify the implementation of these techniques:**

- NLPAug: Supports character, word, and sentence-level augmentations, including back-translation.
- TextAttack: Focused on adversarial attacks and data augmentation for robustness.
- AugLy: A multi-modal library by Meta for augmenting text, images, and audio.

---

## Text extraction and cleaning

In Natural Language Processing (NLP), text extraction and cleanup are the critical first steps used to transform raw, messy data into a structured format suitable for analysis.

**1. Text Extraction**
This phase involves pulling plain text from various unstructured file formats using specialized tools:

- **PDFs:**
  - PyMuPDF (Fitz): Highly efficient for general text, metadata, and extracting content by blocks or paragraphs.
  - pdfplumber: Best for detailed extraction, especially when dealing with complex layouts or tables.
  - pypdf: A pure-Python library commonly used for simpler text extraction and page management.

- **Images & Scanned Docs (OCR):**
  - pytesseract: A wrapper for Google’s Tesseract-OCR, standard for general image-to-text tasks.
  - EasyOCR: A deep learning-based tool that supports 80+ languages and often performs better than Tesseract on diverse fonts.
  - Web Content (HTML):
    BeautifulSoup: Used to strip HTML tags and isolate relevant text from raw web data.

- **Multi-format:**
  - Unstructured: A comprehensive library designed to ingest and partition documents of almost any type (PDF, Word, Excel, etc.) into a consistent format for LLM pipelines.

**2. Text Cleanup (Preprocessing)**
Once extracted, text must be "cleaned" to remove noise and standardize variations.

**Common steps include:**

- Noise Removal: Deleting irrelevant elements like HTML tags, URLs, special characters (e.g., emojis or symbols), and extra whitespaces.

- Normalization:
  - Lowercasing: Converting all text to lowercase to ensure consistency (e.g., treating "Apple" and "apple" as the same token).
  - Contraction Expansion: Replacing shortened forms like "don't" with "do not" to standardize phrasing.
  - Spell Checking: Correcting typos using tools like pyspellchecker or TextBlob.
  - Tokenization: Breaking the text down into smaller, meaningful units like words or sentences.
  - Stop Word Removal: Filtering out common words that carry little semantic weight (e.g., "the," "is," "and").

**Stemming & Lemmatization:**

- Stemming: A fast, rule-based approach that chops off suffixes (e.g., "running" becomes "run").
- Lemmatization: A more accurate, dictionary-based approach that considers word context (e.g., "better" becomes "good").

**Common Python Libraries for Cleanup**

- NLTK: The most traditional toolkit for tokenization, stemming, and stop word removal.
- spaCy: A high-performance library ideal for production-level lemmatization and entity recognition.
- CleanText: A specialized library that handles multiple cleaning steps (URLs, emails, emojis) in a single command.

---

## Unicode Normalization, Spelling Correction, System-Specific Error Correction

After text extraction, data must be normalized and corrected to ensure downstream NLP models interpret it accurately and consistently.

**1. Unicode Normalization**
Unicode allows the same character to be represented in multiple ways (e.g., an accented "é" can be one code point or a combination of "e" + "´"). Normalization converts these variations into a single standard form.

Forms:

- NFC (Composed): Merges characters into their shortest equivalent (e.g., "e" + "´"
  "é"). This is the standard for most web and Windows applications.
- NFD (Decomposed): Breaks composed characters into base letters and marks (e.g., "é", "e" + "´").
- NFKC / NFKD (Compatibility): More "aggressive" forms that normalize symbols with the same meaning but different formatting, such as converting circled digits (①) to regular digits (1) or expanding ligatures like "ﬁ" to "fi".

- Usage: Primarily used for text matching and search consistency. Python’s unicodedata.normalize() is the standard tool.

**2. Spelling Correction**
Spelling errors act as "noise," causing models to misidentify words.

**Standard Algorithms:**

- SymSpell: Highly favored for production due to its extreme speed; it uses a symmetric delete algorithm to find candidates within a specific "edit distance" (e.g., characters to change/delete to reach a real word).
- TextBlob: Uses a simplified approach based on word frequency and edit distance, making it very beginner-friendly.
- JamSpell: A context-aware library that uses surrounding words to decide the best correction.

- Workflow: Typically involves detecting non-dictionary words and then ranking potential candidates by similarity.

**3. System-Specific Error Correction**
Errors often follow predictable patterns based on how the text was generated (e.g., OCR or ASR systems).

- **OCR Correction (Optical Character Recognition):** Addresses visual misreadings, such as confusing "0" with "O" or "1" with "l". Custom regex or mapping dictionaries are often used to fix these specific character-level swaps.
- **ASR Correction (Automatic Speech Recognition):** Fixes phonetic errors (e.g., "sea" instead of "see"). Advanced systems use "N-best" fusion, comparing multiple transcriptions from the speech model to vote on the most likely correct word.
  Domain-Specific Noise: Includes removing platform-specific markers, such as "RT" for retweets on Twitter, or replacing industry jargon and medical abbreviations with full terms.

---

## One-Hot Encoding and bag of words

**1. One-Hot Encoding (OHE)**
OHE represents individual words as binary vectors.

- How it works: Create a vector with a length equal to your entire vocabulary. For a specific word, put a 1 at its unique index and 0 everywhere else.

- Example: If your vocabulary is ["cat", "dog", "run"]:
  "cat" = [1, 0, 0] and "dog" = [0, 1, 0]

- Downside: It is "sparse" (mostly zeros) and cannot represent a whole sentence in one vector without losing the "one-hot" property.

**2. Bag-of-Words (BoW)**
BoW represents an entire document or sentence by summing up the word counts.

- How it works: It counts how many times each vocabulary word appears in a text. It "throws words into a bag," meaning it ignores word order and grammar.
- Example: Sentence: "dog meets dog"
  Using the vocabulary ["cat", "dog", "meets"], the BoW vector is [0, 2, 1].
- Usage: Great for basic document classification (e.g., spam vs. ham) where the presence of certain words is more important than their sequence.

---

## Distributed Representations in nlp

Unlike One-Hot Encoding or Bag-of-Words, Distributed Representations (also known as Word Embeddings) represent words as dense, low-dimensional, real-valued vectors.

The core idea is based on the Distributional Hypothesis: "Words that occur in similar contexts tend to have similar meanings."

**What are some key characteristics and techniques?**

- Dense Vectors: Instead of thousands of zeros, words are represented by a fixed-size vector (e.g., 50, 100, or 300 dimensions) of floating-point numbers.
- Semantic Proximity: Related words like "king" and "queen" are mathematically close to each other in the vector space.
- Linear Relationships: They capture analogies through vector arithmetic, famously.
- Word2Vec: Developed by Google, it uses two architectures:
- CBOW (Continuous Bag of Words): Predicts a target word based on its context.
- Skip-gram: Predicts the surrounding context words given a single target word.
- GloVe (Global Vectors): Developed by Stanford, it creates embeddings by analyzing global word-word co-occurrence statistics across the entire corpus.
- FastText: Developed by Facebook, it treats words as a collection of character n-grams. This allows it to generate representations for "Out of Vocabulary" (OOV) words by looking at their sub-parts.

**Why They Are Superior**

- Efficiency: They significantly reduce dimensionality compared to sparse methods like One-Hot Encoding.
- Generalization: Because "hotel" and "motel" have similar vectors, a model trained on "hotel" data can still perform well when it encounters the word "motel".
- Transfer Learning: You can download Pre-trained Vectors trained on billions of words (Wikipedia, Common Crawl) and plug them into your own smaller models to boost performance.

---

## Naive Bayes Classifier in NLP

Naive Bayes is a widely used probabilistic machine learning algorithm in Natural Language Processing (NLP), primarily for text classification tasks like spam detection and sentiment analysis. It is based on Bayes' Theorem and makes the "naive" assumption that all features (words) are independent of each other given the class label.

**What are some core mechanisms in NLP?**

- Bayes’ Theorem: It calculates the probability of a class (e.g., "Spam") given a set of features (words).
- The "Naive" Assumption: It assumes that the presence of one word in a document is unrelated to the presence of any other word. While linguistically inaccurate (e.g., "San" and "Francisco" are highly related), this simplification makes the algorithm extremely fast and computationally efficient.
- Bag-of-Words Model: Text is typically represented as a "bag-of-words," where word order is ignored and only frequency counts or presence/absence matter.
- Laplace Smoothing: To prevent "zero-frequency" problems—where a word not seen in training results in a total probability of zero—a small value (usually 1) is added to every word count.

**What are the variants used in NLP?**

- Multinomial Naive Bayes: The most common version for text. It uses word frequency counts (how many times "offer" appears).
- Bernoulli Naive Bayes: Focused on word presence or absence (did "offer" appear at all? Yes/No). This is effective for shorter documents or binary classification.
- Complement Naive Bayes: Specifically designed to correct for imbalanced datasets where one class has much more data than another.

**Pros**

- Fast & Efficient: Requires only a single pass over the data.
- Small Data: Performs well even with limited training samples.
- High Dimensionality: Handles thousands of features (words) easily.

**Cons**

- Independent Assumption: Fails to capture context or word order (e.g., "not good" vs "good").
- Poor Probability Estimator: While good at picking the right class, its calculated probability values are often unreliable.
- Feature Sensitivity: Sensitive to irrelevant features if not pre-processed properly.

**Typical Implementation Steps**

- Pre-processing: Tokenization, lowercase conversion, and removing stop words (e.g., "the", "is") or punctuation.
- Vectorization: Converting text to numbers using tools like Scikit-learn’s CountVectorizer or TfidfVectorizer.
- Training: Fitting the model using labeled data (e.g., MultinomialNB().fit(X, y)).
- Evaluation: Using metrics like accuracy, precision, and F1-score to measure performance.

---

## Logistic Regression in NLP

In Natural Language Processing (NLP), Logistic Regression (LR) is a foundational discriminative machine learning algorithm used for supervised text classification. Unlike generative models like Naive Bayes, LR learns the direct relationship between input features (words) and class labels by optimizing a decision boundary.

**How it Works in NLP**

- Text Representation: Text must first be converted into numerical vectors. Common methods include:
- Bag-of-Words (BoW): Simple word counts.
- TF-IDF: Weights words by their frequency and rarity across the corpus.
- Word Embeddings: Dense vectors (like Word2Vec or GloVe) that capture semantic meaning.
- Linear Combination: The model calculates a weighted sum of these input features plus a bias term.
- Sigmoid Function: To convert this sum into a probability between 0 and 1, the model applies the sigmoid function.
- Decision Boundary: Typically, if the probability is 1, it is assigned to the positive class; otherwise, it belongs to the negative class.

**What are some common applications?**

- Sentiment Analysis: Categorizing reviews as positive, negative, or neutral.
- Spam Detection: Classifying emails or SMS messages as "spam" or "ham".
- Topic Classification: Sorting news articles into categories like politics or sports.
- Duplicate Detection: Identifying similar questions on platforms like Quora.

**Key Considerations**

- Regularization: Techniques like L1 (Lasso) or L2 (Ridge) are essential to prevent overfitting, especially when dealing with high-dimensional text data.
- Multi-class Tasks: For more than two categories, LR uses Multinomial Logistic Regression (Softmax) or a One-vs-Rest (OvR) strategy.
- Linearity: LR assumes a linear relationship between features and the log-odds of the class, which may not capture complex semantic nuances as well as deep learning models.

---

## Keyphrase extraction

Keyphrase extraction is an NLP technique used to automatically identify the most important words or phrases in a document. These phrases serve as a succinct summary, making it easier to index, search, and categorize vast amounts of content.

**Core Extraction Pipelines**
Most systems follow a two-stage framework:

- Candidate Selection: Identifying all potential words or phrases (often nouns or noun phrases).
- Ranking: Scoring these candidates to select the top-N most representative phrases.

**Types of Methods**
Methods are generally categorized based on whether they require labeled training data.

- **Unsupervised Methods (No Training Data Required)**
  These are highly popular because they work "out of the box" across different domains.
  - Statistical: Uses word frequency, position, and co-occurrence (e.g., TF-IDF, RAKE, YAKE).
  - Graph-Based: Treats a document as a graph where words are nodes. Algorithms like TextRank or PositionRank use a PageRank-style approach to find the most "central" words.
  - Embeddings-Based: Uses modern models like BERT to compare the semantic meaning of candidate phrases to the entire document (e.g., KeyBERT, EmbedRank).

- **Supervised Methods (Training Data Required)**
  These treat extraction as a binary classification problem (is it a keyphrase or not?) or a sequence labeling task.
  - Classical Models: Uses features like TF-IDF and position to train classifiers like Naive Bayes (e.g., KEA, Maui).
  - Deep Learning: Uses neural networks like Bi-LSTMs or Transformers to capture long-term context and semantic relationships.

**Popular Python Libraries**
Several libraries provide easy-to-use implementations of these algorithms:

- KeyBERT: Leverages BERT embeddings for minimal, high-quality extraction.
- YAKE: A lightweight, unsupervised approach that doesn't require a corpus.
- RAKE-NLTK: A common Python implementation of the Rapid Automatic Keyword Extraction algorithm.
- spaCy: Often used for the initial "Candidate Selection" phase, such as extracting noun chunks.

---

## Named Entity Disambiguation (NED) and Named Entity Linking (NEL)

Named Entity Disambiguation (NED) and Named Entity Linking (NEL) are critical NLP tasks that resolve which specific real-world entity a name refers to in a given context. While often used interchangeably, they represent two halves of a process that turns ambiguous text into structured knowledge.

**1. Key Differences**

- Named Entity Disambiguation (NED): Focuses on the decision-making process. It resolves ambiguity when a single name could refer to multiple distinct entities (e.g., deciding if "Apple" refers to the fruit or the technology company based on nearby words like "iPhone" or "orchard").
- Named Entity Linking (NEL): Focuses on the connection to a structured resource. It maps the identified name to a unique identifier (URI) in a Knowledge Base (KB) such as Wikidata, DBpedia, or a private company database.

**2. The Standard Pipeline**
A typical entity linking system follows three main steps:

- Entity Recognition (NER): Spotting a mention in the text and classifying its general type (e.g., identifying "Jordan" as a PERSON).
- Candidate Generation: Searching the knowledge base to find all potential matches for that name (e.g., Michael Jordan the athlete, the country of Jordan, or the river Jordan).
- Candidate Ranking (Disambiguation): Scoring the candidates using contextual clues, popularity (prior probability), and semantic relatedness to other entities in the same text to select the best match.

**3. Common Techniques**

- Contextual Similarity: Comparing words surrounding the mention with descriptions in the knowledge base.
- Knowledge Graph Proximity: Using the relationships between entities in a graph. For example, if "Chicago" is also mentioned, it significantly boosts the score for "Michael Jordan" the basketball player.
- Deep Learning Embeddings: Modern tools like BLINK or KeyBERT use dense vector representations to capture deep semantic meaning.

**4. Popular Tools & Libraries**

- spaCy Entity Linker: An extension for the spaCy library that links entities directly to Wikidata.
- DBpedia Spotlight: A widely used tool for automatically annotating text mentions with DBpedia URIs.
- Hugging Face Transformers: Provides pre-trained models that can be fine-tuned for high-accuracy end-to-end entity linking.
- Stanford CoreNLP: A robust Java-based suite that can be integrated with disambiguation modules.

---

## Tokenizing Texts for different nlp tasks

Tokenization converts raw text into structured numerical units (tokens) that machine learning models can process. The strategy you choose depends on the specific NLP task and its requirements for granularity or context.

**1. Tokenization by Level of Granularity**

- Word Tokenization: Splits text by whitespace and punctuation into individual words. It is best for standard text classification, sentiment analysis, and keyword extraction.

- Subword Tokenization: Breaks words into smaller meaningful units (e.g., "unhappiness" -> "un", "happi", "ness"). Algorithms like Byte Pair Encoding (BPE) or WordPiece are industry standards.It is ideal for modern transformer models (BERT, GPT) to handle "out-of-vocabulary" (OOV) words and rare terms.

- Sentence Tokenization: Segments a document into distinct sentences.
  It is best for summarization, machine translation, and document-level analysis.

- Character Tokenization: Treats every character as a token.
  It is best for languages without clear word boundaries (Chinese, Japanese), spelling correction, or phonetic analysis.

**2. Task-Specific Strategies**
NLP Task Recommended Strategy

- Named Entity Recognition (NER) Subword + Alignment Preserves internal word structure to identify entities like "San Francisco" correctly.
- Machine Translation Sentence + Subword Captures sentence-level context while managing vast vocabularies across different languages.
- Sentiment Analysis Word or Subword Focuses on key emotional triggers (e.g., "happy", "not").
- Question Answering Subword with Offsets Needs to map the exact start/end character positions of the answer in the original text.

**3. Implementation Tools**

- Hugging Face Tokenizers: Fast, Rust-based library that handles the complex subword mapping required for transformers.
- spaCy: A production-ready tool that uses sophisticated linguistic rules to handle contractions (e.g., "don't"
  "do", "n't") and punctuation.
- NLTK: Offers a wide range of rule-based tokenizers like word_tokenize and sent_tokenize, ideal for educational use and rapid prototyping.

---

_Resources:_

1. [Natural Language Processing with Deep Learning (Stanford CS224N) by Christopher Manning](https://www.youtube.com/watch?v=DzpHeXVSC5I&list=PLoROMvodv4rOaMFbaqxPDoLWjDaRAdP9D)

2. [Practical Natural Language Processing: A Comprehensive Guide to Building Real-World NLP Systems by Sowmya Vajjala, Bodhisattwa Majumder, Anuj Gupta, and Harshit Surana](https://dokumen.pub/practical-natural-language-processing-a-comprehensive-guide-to-building-real-world-nlp-systems-1492054054-9781492054054-h-1409126.html)

3. [Natural Language Processing with Python by Steven Bird, Ewan Klein, and Edward Loper](https://www.oreilly.com/library/view/natural-language-processing/9780596803346/)

4. [Natural Language Processing with Python (NLTK Book) by Steven Bird, Ewan Klein, and Edward Loper](https://www.nltk.org/book/)
