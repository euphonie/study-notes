> All information gathered from Udacity's Natural Language Processing Nanodegree

## NLP Pipeline

A basic processing pipeline for natural language could be identified as having the following stages:
- Text processing. Takes raw input text, cleans it, normalizes it.
- Feature extraction. Generates feature representations appropriate for the desired model.
- Modeling. NLP task.

### Text processing

Text processing is needed because information is gathered from multiple sources where text might be entangled with different markups, formats or constructs that are information only valid to the type of source from where the text is extracted.

### Feature Extraction

Computers don't hold standard representations of words. The features depende directly from the kind of model that is needed for the task in hand.
Examples:
- Graph-based model => words can be represented as nodes with relationships being the edges.
- Statistical modals => numerical representation
- Document or Sentiment analysis => Word of bags or doc2vec
- Text generation or machine translation => word level representation (word2vec or glove)

### Modeling
The phases it may comprise are: 
- Design a statiscally or machine learning model
- Fit parameters to training data with optimization procedure
- Use model to make predictions about unseen data

> Written with [StackEdit](https://stackedit.io/).

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg4MjcxODkyNCwtMjg1MzEyNDc4XX0=
-->