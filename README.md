# Geological Language Models

## Introduction
Language models are the foundation for the predictive text tools that billions of people use on their smartphones and elsewhere in their everyday lives. Although these language models are often trained on a large digital corpora, they are often missing the specialized vocabulary and underlying concepts that are important to specific scientific sub-domains. Herein we address that knowledge gap and report two new language models that were updated using geological text. The raw and processed text from the GEOSCAN publications database, which were used to generate these new language models, are also reported. Language model performance and validation are discussed separately in pending manuscript. The supporting datasets and preferred language models can be used and expanded on in the future to support a range of down stream natural language processing tasks (e.g., keyword prediction, document similarity, and recommender systems).


### Geological Text
Language models are based, in part, on a variety of geoscientific publications sourced from the Natural Resources Canada (NRCan) GEOSCAN publications database (n = 27,081 documents). Figures, maps, tables, references, irregularly formatted text, and other large sections of documents from poor quality scans were excluded from further analysis (i.e., the total GEOSCAN database contains approximately 83k documents; however <32% were readily available for use as part of the current study). The “pdfminer” library was used to extract text from the remaining pdf documents prior to a number of pre processing steps, including removing punctuation, replacing upper casing, removing French text, removing specific forms of alpha-numeric data (e.g., DOIs, URLs, emails, and phone numbers), converting all non-ascii characters to their ascii equivalent, filtering text boxes that contain an insufficient percentage of detectable words, and merging all of the extracted text for each document. Raw and pre-processed text data from the GEOSCAN publications database will be made avialable in a pending Open File. Additional geoscientific publications that were used to re-train language models were sourced from provincial government publication databases (e.g., Ontario Geological Survey, Alberta Geological Survey, and British Columbia Geological Survey; n = 13,898 documents) and a subset of open access journals (e.g., Materials, Solid Earth, Geosciences, Geochemical Perspective Letters, and Quaternary) available through the Directory of Open Access Journals (DOAJ; n = 3,998 documents).


### GloVe Model
The Global Vectors for Word Representation (GloVe) method (Pennington et al., 2014) was used to map each word in the training corpus to a set of numerical vectors in N-dimensional space and was originally trained using billions of words, or sub-words, from the Wikipedia (2014) and the 5th Edition of English Gigaword (Parker et al., 2011). This original GloVe model was then re-trained as part of the current study using the smaller, but domain specific corpora to improve model performance (i.e., the preferred GloVe model). This preferred GloVe model was trained using the AdaGrad algorithm with the most abundant tokens (i.e., minimum frequency of 5), considering a context window of size 15 for 15 iterations, fixed weighing functions (x_max = 10 and alpha = 0.75) and is based on the 300 dimensional vectors as described by Pennington et al. (2014).


### BERT Model
Contextual language models, including the Bidirectional Encoder Representations from Transformers (BERT) method (Devlin et al., 2019), consider words and their neighbours for a more complete representation of their meaning. The original BERT model was pre trained on the Books Corpus (Zhu et al., 2015) and English Wikipedia, comprising billions of words. More recently, the DistilBERT method (Sanh et al., 2019) was proposed to simplify the training process for smaller datasets, produce language models that are less susceptible to overfitting, and yield model performance that are comparable to the original BERT method. The first step for all BERT models is to convert pre processed text to tokens, which may include words, sub-words or punctuation. Sub-word tokenization limits the number of out-of-vocabulary words, which allows BERT models trained on general corpora to be applied to specific sub-domains. A geology specific tokenizer was created as part of the current study by adding geology tokens prior to continued pre-training using the geological corpora. This preferred BERT (i.e., using the geo-tokenizer and geological corpora) model was generated using the “HuggingFace” machine learning library with the same combination of hyper-parameters described in the original Devlin et al. (2019) method (e.g., learning rate =  5e-5 and 2.5e-5; batch size = 48; max steps = 1 and 3 million; warm-up steps: 0, 100k, 300k).

