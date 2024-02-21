# Week 05.2: Compositional Embeddings

## Compositional Embeddings
Compositional embeddings are a concept in NLP that involve constructing representations (embeddings) of larger linguistic units (such as phrases, sentences, or even entire documents) from the embeddings of smaller units (like words or subwords).

- The process of creating compositional embeddings typically involves some form of operation or model that combines the individual word embeddings into a single, coherent vector representation that captures the semantics of the larger text fragment.
- Compositional embeddings can capture more nuanced and context-specific meanings
- Compositional embeddings can account for word order, context, and even long-range dependencies within the text.

## Compositionality: Word to Text
In NLP applications, we are interested in understanding the phrase's meaning. However, embeddings (until now, Word2Vec) only represent the word's meaning. We study how we can use embeddings to represent phrase's meaning.

By considering the word meaning as a vector (or tensor), we can calculate the phrase's meaning as

1. **Vector Addition**: just sum all vectors together (simplest form)
    - Advantages:
        - Easy to calculate
        - Fixed vector length, regardless of text length
        - Although the disadvantage, in some tasks, it provides descent results.
    - Disadvantages:
        - Loses word order
        - Lower impact of individual words. In some phrases, some words are more important than others.
2. **Vector Concatenation**: just concatenate the vectors
    - Advantages
        - Simplicity
        - It keeps partially the word-level semantics by preserving the order, but it doesn't provide a full understanding of the order.
        - Variable information about the sentence is preserved by keeping the information of each word.
    - Disadvantage
        - High-dimensional sentence vectors
        - Many machine learning systems require fixed-length inputs, but this approach is variable.
        - **Inefficiency in Capturing Sentence-Level Semantics**: While word vectors contain semantic information, the meaning of a sentence is more than the sum of its parts.
        - **Contextual Ambiguity**: simple concatenation does not address polysemy (words with multiple meanings) effectively.
3. **Complex (hierarchical) operations**, such as recursive compositionality
    - It represents the meaning of a word as a (vector, matrix) multiplication.
    - The compositionality is a recursive vector-matrix operation
    - Follow the syntactic structure.
    - It's theoretically inspired but commonly doesn't work.
4. **Via Deep Neural Networks** 
    - Current state-of-the-art
    - Input the vector embeddings into a neural network and let the network handle the interactions
    - The network architecture determines the compositionality by generating **Contextual Word Embeddings**, which are embeddings that consider the context to define the meaning of a word.
    - Some of these solutions can handle the **Contextual Ambiguity** problem.
    - They can capture syntactic and semantic relationships between words in a sentence. 
    - There are different models:
        - MLP in NLP (not recommended)
        - CNN in NLP (not recommended)
        - RNNs: LSTM, BiLSTM (ELMO), GRU
        - Transformers: BERT, GPT

- **Contextual Ambiguity**: In NLP, some words can have multiple meanings depending on the context. This phenomenon is known as **polysemy**, and it's handled nowadays for Deep Learning methods.
    - It is a common challenge for contextual embeddings.



## ELMO

TODO: Write a short comprehension of ELMO
