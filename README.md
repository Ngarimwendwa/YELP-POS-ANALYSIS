1.	INTRODUCTION
The objective of this assignment is to prepare and analyze a large corpus of Yelp customer reviews spanning from 2017 to 2022. Customer feedback is a rich source of business intelligence, but raw text data is inherently unstructured, noisy and challenging for algorithms to interpret.
This project focuses on applying Natural Language processing (NLP) techniques to clean the data, identify key subjects and mathematically represent the text for machine learning applications.
The dataset contains millions of reviews, with unstructured text and metadata all in one. Due to computational restraints we will use a random sample of 200,000 localized records for this analysis.
3.	METHODOLOGY

2.1 DATA PREPROCESSING
When dealing with raw data as the one provided they tend to be inherently noisy, filled with inconsistencies such as casing, punctuation, numbers and grammatical fillers that would make any algorithm out there struggle to parse correctly. 
To prepare the Yelp dataset for analysis I used several steps which were:
•	NORMALIZATION 
I converted all text to lowercase to standardize the vocabulary. I also removed punctuation and digits, this helped prevent clumping with adjacent words for example “pizza” and “pizza!” If this was not done the vocabulary would end up with irrelevant tokens and would reduce the statistical power of the model.
•	TOKENIZATION
this step breaks down the continuous string of review text into a structured list of tokens. The NLTK library was a key element here.
•	STOP WORD REMOVAL
by removing stop words the focus shifts to the semantics core- nouns and adjectives that convey customer sentiment and specific subjects.
•	LEMMATIZATION
I chose stemming over lemmatization because lemmatization focuses on a dictionary to reduce words instead of chopping off word endings. It strengthens the key themes without losing interpretability.

2.2 PART OF SPEECH (POS) TAGGING, NER AND TEXT REPRESENTATION
•	POS Tagging: I applied ‘pos_tag’ function to the lemmatized tokens to classify each word’s grammatical role (noun, verb, adjective) allowing for statistical analysis of the sentence structures.
•	Name Entity Recognition (NER)
The ‘spaCy’ NLP library (en_core_web_sm) was utilized on the raw, un-normalized text. ‘spaCy’ basically analyzed capitalization and contextual grammar to extract proper nouns, which were filtered down to targets relevant to yelp.
•	TEXT REPRESENTATION
I applied two methodologies to convert the processed text into numerical vectors:
o	TF-IDF: The ‘TfidVectorizer” evaluated the frequency of words in individual reviews while penalizing words that occur universally across the entire dataset.
o	Word2Vec: The ‘Gensim’ Word2Vec model trained a neural network on the sequential lists of tokens to creatw dense vextor embeddings based on the contextual usage of each word.

3.	RESULTS AND DISCUSSION

3.1	POS TAG DISTRIBUTION
Analysis of the POS Tagging revealed that the dataset is heavily dominated by Nouns and Adjectives. 
Understanding this distribution confirms that the preprocessing successfully retained the core building blocks of customer opinions.
 
3.2	ACCURACY AND RELEVANCE OF NER OUTPUTS
 ‘spaCy’ proves highly relevant here. The top extracted entities heavily featured major cities and prominent national or local business chains. 
 We can see the accuracy of ‘spaCy’ because it successfully differentiates between standard nouns and proper entities based on context.
For this YELP sample, aggregating NER data allows for the automated generation of highly accurate, user-driven tags for businesses, improving regional search algorithms.
 
3.3	COMPARISON OF TEXT REPRESENTATION TECHNIQUES 
TF-IDF and Word2Vec offer opposite strengths and weaknesses:
•	TF-IDF: highly effective at identifying the most distinctive, defining keywords of a document. Towards the computer is is efficient and interpretable. It however creates a sparse matrix that ignores word order, meaning and context.
•	Word2Vec: captures deep semantic meaning. It learnt that “pizza”, “burger” and “taco” represent similar concepts. This allows models models to recognize similarities between reviews even if they don’t share identical vocabulary. 
Its primary weaknesses are its computational intensity, its blackbox lack of iterpretability, and the fact that it models individual words rather than entire documents out of the box.
 
Above a snippet output of the TF-IDF/Word2Vec output.
4.	CONCLUSION

4.1	SUMMARY OF KEY FINDINGS
This analysis has confirmed that sequential data preprocessing- normalization, tokenization, stop word removal and lemmatization- is mandatory to expose the semantic core of customer reviews. 
POS tagging confirmed that customer feedback is structurally reliant on noun-adjective pairings. NER extraction proved to be a viable method for automatically isolating key locations and subjects, offering immediate business intelligence.
Finally, representing this text numerically requires a strategic choice: TF-IDF is best for distinctive keyword extraction, while Word2Vec is required for models attempting to understand deep contextual sentiment.

4.2	FUTURE EXPLORATION
Future improvements I would suggest is to involve experimenting with more advanced Transformer-based models (such as BERT), which represent entire sentences contextually rather than individual words. 
Also, connecting the NER entity outputs directly to the adjectives that surround them could provide automated, accurate sentiment scores for specific products within a single business.
