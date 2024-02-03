# Week 01: Words, Corpora, Text Normalization

We covered the following topics in order
1. Regular Expressions
2. Basic ELIZA Understanding
3. Words and Corpora
4. Text-Normalization
   - Tokenization
   - Lemmatization (Stemming)
   - Sentence Segmentation
5. Edit Distance

## 3. Words and Corpora
This section discusses how to identify and differentiate words in a text.
- **Token**: An instance of a type in the text.
- **Type**: An element of the vocabulary.
- **Lemma**: The base or dictionary form of a word (same stem or rough word sense)
- **Wordform**: The full inflected form of the word.

*Example*: In "My cat and the cats in Ecuador are different from other cats." 
- each word is a token (12 tokens). 
- but only 11 types in the vocabulary, "cats" is a type of the vocabulary $V$.
- the lemma of "cats" and "cat" is the same "cat".
- the wordform of "cats" is "cats".

**Herdan's Law**: establish a relationship between the number of types |V| and number of tokens N. This relationship indicate us that the larger the corpora we look at, the more word types
we find.

$$|V| = kN^\beta$$ 
where $k$ and $\beta$ are positive constants, and $0 < \beta < 1$, typically ranging between 0.67 and 0.75.

## 4. Text Normalization
This involves converting raw text into a uniform format for NLP tasks.
- **Tokenizing (Segmenting) Words**: Breaking down text into words or tokens.
- **Normalizing Word Formats**: Standardizing the format of words.
- **Segmenting Sentences**: Dividing text into sentences.

*Example*: "U.S.A." 
- Tokenization: ["U", ".", "S", ".", "A", "."]
- Normalization: ["usa"]
- Sentence Segmentation: Treated as a sentence.

### Tokenizing (Segmenting) Words
- **Definition**: Breaking down text into individual words or tokens.
- **Basic Tokenization**: Commonly uses space-based tokenization for languages with spaces between words (e.g., Arabic, Cyrillic, Greek, Latin-based systems).
- **Tools**: Unix tools like the "tr" command can be used for basic tokenization.
- **Challenges**: 
  - Handling punctuation (e.g., "m.p.h.", "Ph.D.").
  - Dealing with contraction (e.g. "didn't, what're")
  - Dealing with multiword expressions (e.g. New York and rock 'n' roll). Then, it is tied up with named entity recognition.
  - Dealing with prices, dates, URLs, hashtags, and email addresses.
- **Advanced Tokenization**: Utilizes regular expressions and NLP tools (e.g., NLTK) for complex patterns and exceptions.
  - Deterministic algorithms are used in practice because tokenization must run very fast during pre-processing.
  - Word tokenization is more complex in languages like written Chinese, Japanese, and Thai. (e.g. In Chinese, each char, called hanzi, is used as token.)
  - Although is basic, **Byte-Pair Encoding** is a common algorithm.

### Normalizing Word Formats
- **Purpose**: Converts words or tokens into a standard format, chosing a single normal form for words with multiple forms (e.g: USA and US)
- There are different ways to normalize depending of the task at hand:
  - **Case Folding**: Converting text to lower or upper case as needed.
  - **Handling Variations**: Dealing with different forms of a word (e.g., "U.S.A." vs. "USA").
  - **Lemmatization**: Reducing words to their base or dictionary form (e.g. *is*, *are*, *am* shared the lemma *be*, or *dinner* and *dinners*.)
    - **Morphological Parsing (Most Sophisticated)**: Breaks down words into morphemes (stems and affixes). Note a stem is the central morphene of the word, supplying the main meaning.
    - **Stemming (Naive Version)**: consits in chopping off word-final affixes. It's algorithmn consists in a set of rules that are applied sequentially,
- **Importance**: Essential for applications like information retrieval and sentiment analysis.


### Segmenting Sentences
- **Objective**: Dividing text into individual sentences.
- **Challenge with Periods**: The period (".") is ambiguous (used in abbreviations, numbers, and as a sentence boundary).
  - For that reason, sentence tokenization and word tokenization may be addressed jointly.
- **Approach**:
  - **Initial Tokenization**: Classify each period as part of a word or a sentence boundary.
    - It's possible to use different tools, such as abbreviation dictionaries and machine learning algorithms.
  - Applying rules for sentence segmentation based on the initial tokenization.


### Summary Table

| Topic             | Description                                       | Key Terms                          | Example                            |
|-------------------|---------------------------------------------------|------------------------------------|------------------------------------|
| Words and Corpora | Discussing the concept of words in texts.         | Token, Type, Lemma, Wordform       | "cats" (Token), "cat" (Lemma), "cats" (Type) |
| Text Normalization| Converting raw text to a uniform format for NLP.  | Tokenizing, Normalizing (Morphological Parsing and Stemming), Segmenting| "U.S.A." -> ["usa"]                |
| Byte Pair Encoding| An automatic method for tokenizing words.         | Subword tokenization               | "lower" -> ["l", "o", "w", "e", "r"] |
