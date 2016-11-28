# Sentiment Analysis in Stock Movement Prediction
Use NLP technique to predict stock price movement based on news from Reuters

1. Data Collection

  1.1 get the whole ticker list
  
  1.2 crawl news from Reuters using BeautifulSoup
  
  1.3 crawl prices using Yahoo Finance API
  
2. Applied GloVe to train a dense word vector from Reuters corpus in NLTK
3. Feature Engineering

  3.1 Extract feature using feature hashing
  
  3.2 Remove punctuations, unify tense, singular & plural
  
  3.3 Pad word senquence (essentially a matrix)
  
4. Train a ConvoNet to predict the stock price movement.
5. The result shows a 15% percent improve on the validation set, and 1-2% percent improve on the test set


## 1. Data Collection


#### 1.1 Download the ticker list from [NASDAQ](http://www.nasdaq.com/screening/companies-by-industry.aspx)

```python
./crawler_allTickers.py 20  # keep the top e.g. 20% marketcap companies
```

#### 1.2 Use BeautifulSoup to crawl news headlines from [Bloomberg](http://www.bloomberg.com/search?query=goog&sort=time:desc) and [Reuters](http://www.reuters.com/finance/stocks/overview?symbol=FB.O)

```python
./crawler_bloomberg.py # Bloomberg news is not that correlated, ignore this data at this moment
./crawler_reuters.py # much more valueable, despite with a much smaller size
```

#### 1.3 Use Yahoo Finance [API](https://pypi.python.org/pypi/yahoo-finance/1.1.4) to crawl historical stock prices

```python
./crawler_stockPrices.py
```

## 2. Word Embedding

Applied [GloVe](https://github.com/lazyprogrammer/machine_learning_examples/blob/master/nlp_class2/glove.py) to train a dense word vector from Reuters corpus in NLTK

```python
./word_embedding.py
```

## 3. Feature Engineering

lower case, remove punctuation, get rid of stop words using [NLTK](http://www.nltk.org/), unify tense using [en](https://www.nodebox.net/code/index.php/Linguistics#verb_conjugation)


## Training and Model Selection

## Prediction and analysis


## Issues
1. remove_punctuation() handles middle name (e.g., P.F -> pf)

## References:
1. [Keras predict sentiment-movie-reviews using deep learning](http://machinelearningmastery.com/predict-sentiment-movie-reviews-using-deep-learning/)
2. [Keras sequence-classification-lstm-recurrent-neural-networks](http://machinelearningmastery.com/sequence-classification-lstm-recurrent-neural-networks-python-keras/)
3. [tf-idf + t-sne](https://github.com/lazyprogrammer/machine_learning_examples/blob/master/nlp_class2/tfidf_tsne.py)
4. [IMPLEMENTING A CNN FOR TEXT CLASSIFICATION IN TENSORFLOW](http://www.wildml.com/2015/12/implementing-a-cnn-for-text-classification-in-tensorflow/)
5. [Implementation of CNN in sequence classification](https://github.com/dennybritz/cnn-text-classification-tf)
6. [Convolutional Neural Networks for Sentence Classification](http://www.aclweb.org/anthology/D14-1181)
7. [GloVe: Global Vectors for Word Representation](http://www-nlp.stanford.edu/pubs/glove.pdf)
