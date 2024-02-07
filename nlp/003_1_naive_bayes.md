# Week 03_1: Naive Bayes

This chapter introduced the naive Bayes model for classification and applied it to
the text categorization task of sentiment analysis.

- Many language processing tasks can be viewed as tasks of classification.
- Text categorization, in which an entire text is assigned a class from a finite set,
includes such tasks as sentiment analysis, spam detection, language identification, and authorship attribution.
- Sentiment analysis classifies a text as reflecting the positive or negative orientation (sentiment) that a writer expresses toward some object.
- Naive Bayes is a generative model that makes the bag-of-words assumption
(position doesn’t matter) and the conditional independence assumption (words
are conditionally independent of each other given the class)
- Naive Bayes with binarized features seems to work better for many text classification tasks

## NOTES:

- Note the Naive Bayes include logarithms to avoid computation underflow errors.
- Note if a word in the test is not in the vocabulary, we just don't sum up over those words. The probability will only be log(prior(class)) if we don't have any word from the training in the test
- Note when you are calculating by hand the denominator is always the same for each class
- The likelihood (multiplication of different conditional) can be understood as a language model of unigrams given a condition -> Review the concept correctly TENGO MUCHO sueño

