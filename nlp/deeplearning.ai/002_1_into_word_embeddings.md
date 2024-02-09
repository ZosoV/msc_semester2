# Week 2.1: Intro Word Embeddings

## Word Representation

- One drawback of the one-hot representation is that it treats each word as a thing unto itself, which makes difficult to genearlize across words
    - All it's because every dot-product between two one-hot representation words will be zero, which doesn't provides a notion of similarity. (e.g. knowing "orange juice", it could not autocomplete "apple ___" )
    $$\text{one-hot representation: } o_{1245}$$

    where the index 1245 is the position of the word in the vocabulary (it's the unique value 1).

- The solution is replace an one-hot representation for something more informative like **a vector of features** (**embedding**), which indicates certain qualities of the word. It's like a high-dimensional representation of a word, in commonly 150, 200, or 300 dimensions. $$\text{embedding: } e_{1245}$$ 
where the index 1245 again represent the word 1245 in the vocabulary

- It possible to visualize these embedding using method to project data, such t-SNE.
- The term embedding is because your are embedding a word into 300 dimensional space.

