# Week 01: Words, Corpora, Text Normalization

We covered the following topics in order
1. Regular Expressions
2. Basic ELIZA Understanding
3. Words and Corpora
4. Text-Normalization
   - Tokenization
   - Lemmatization (Stemming)
   - Sentence Segmentation

## 1. Words and Corpora
This section discusses how to identify and differentiate words in a text.
- **Token**: An instance of a type in the text.
- **Type**: An element of the vocabulary.
- **Lemma**: The base or dictionary form of a word (same stem or rough word sense)
- **Wordform**: The full inflected form of the word.

*Example*: In "My cat and the cats in Ecuador are different from other cats." 
- each word is a token (12 tokens). 
- but only 11 types in the vocabulary, cats is a type of the vocabulary $V$.
- the lemma of "cats" and "cat" is the same "cat".
- the wordform of "cats" is "cats".

**Herdan's Law**: establish a relationship between the number of types |V| and number of tokens N. This relationship indicate us that the larger the corpora we look at, the more word types
we find.

$$|V| = kN^\beta$$ 
where $k$ and $\beta$ are positive constants, and $0 < \beta < 1$, typically ranging between 0.67 and 0.75.

## 2. Text Normalization
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
- **Method**: Commonly uses space-based tokenization for languages with spaces between words (e.g., Arabic, Cyrillic, Greek, Latin-based systems).
- **Tools**: Unix tools like the "tr" command can be used for basic tokenization.
- **Challenges**: 
  - Handling punctuation (e.g., "m.p.h.", "Ph.D.").
  - Dealing with prices, dates, URLs, hashtags, and email addresses.
- **Advanced Tokenization**: Utilizes regular expressions and NLP tools (e.g., NLTK) for complex patterns and exceptions.
- **Example**: Using `tr -sc ’A-Za-z’ ’\n’` to isolate each word in a text file&#8203;``【oaicite:2】``&#8203;.

### Normalizing Word Formats
- **Purpose**: Converts words or tokens into a standard format.
- **Processes**:
  - **Case Folding**: Converting text to lower or upper case as needed.
  - **Handling Variations**: Dealing with different forms of a word (e.g., "U.S.A." vs. "USA").
  - **Lemmatization**: Reducing words to their base or dictionary form.
- **Morphological Parsing**: Breaks down words into morphemes (stems and affixes).
- **Importance**: Essential for applications like information retrieval and sentiment analysis.
- **Example**: Normalizing "am," "is," "are" to their lemma "be"&#8203;``【oaicite:1】``&#8203;.

### Segmenting Sentences
- **Objective**: Dividing text into individual sentences.
- **Challenge with Periods**: The period (".") is ambiguous (used in abbreviations, numbers, and as a sentence boundary).
- **Approach**:
  - **Initial Tokenization**: Classify each period as part of a word or a sentence boundary.
  - **Use of Tools**: Abbreviation dictionaries and machine learning algorithms.
- **Final Step**: Applying rules for sentence segmentation based on the initial tokenization.
- **Example**: Differentiating sentence-ending periods from those in abbreviations like "Inc." or "Dr."&#8203;``【oaicite:0】``&#8203;.


### Summary Table

| Topic             | Description                                       | Key Terms                          | Example                            |
|-------------------|---------------------------------------------------|------------------------------------|------------------------------------|
| Words and Corpora | Discussing the concept of words in texts.         | Token, Type, Lemma, Wordform       | "cats" (Token), "cat" (Type/Lemma) |
| Text Normalization| Converting raw text to a uniform format for NLP.  | Tokenizing, Normalizing, Segmenting| "U.S.A." -> ["usa"]                |
| Byte Pair Encoding| An automatic method for tokenizing words.         | Subword tokenization               | "lower" -> ["l", "o", "w", "e", "r"] |
