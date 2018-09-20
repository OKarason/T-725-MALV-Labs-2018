# Lab 5

**Hand in your code in Canvas before midnight tomorrow (21 September). One or more, `.py` files containing the solutions.**

**_Try to complete as much as you can. If you can't manage to complete a particular problem please hand in your incomplete solution._**

[Chapter 6 in the NLTK book](https://www.nltk.org/book/ch06.htmll), the [Classification HOWTO](http://www.nltk.org/howto/classify.html) and sections of the [NLTK Classification API documentation](https://www.nltk.org/api/nltk.classify.html) are relevant to this lab.

## 1. Naive Bayes classifier

Your task is simply to familiarlize yourselves with the classifier, try it out and understand how it works. Feel free to make some changes to see what effect they might have.

```python
from nltk.classify import NaiveBayesClassifier, util
from nltk.corpus import movie_reviews
 
# A helper function to create features
def bag_of_words(words):
    return dict([('contains(%s)' % word, True) for word in words])
    # Assigns the feature ('contains(some-word)', True) for each word in the review to the review type (good/bad)

negative = movie_reviews.fileids('neg')
positive = movie_reviews.fileids('pos')

# Assign the features to the two labels (good/bad)
negative_features = [(bag_of_words(movie_reviews.words(fileids=[f])), 'bad') for f in negative]
positive_features = [(bag_of_words(movie_reviews.words(fileids=[f])), 'good') for f in positive]

neg_size = int(len(negative_features) * 0.80)
pos_size = int(len(positive_features) * 0.80)

training = negative_features[:neg_size] + positive_features[:pos_size]
testing = negative_features[neg_size:] + positive_features[pos_size:]

print('Train on %d instances, test on %d instances' % (len(training), len(testing)))

classifier = NaiveBayesClassifier.train(training)
print('Accuracy using Naive Bayes: %7.4f%%' % (util.accuracy(classifier, testing) * 100))

classifier.show_most_informative_features()
```

**TODO: handin code and report results in comments.**

## 2. Logistic Regression

Algorithms from the [scikit-learn](http://scikit-learn.org/stable/) machine learning library have been embedded into the classification module in NLTK, among them is a Logistic Regression implementation that we are going to test out. For this problem you therefore need to install scikit-learn, NumPy, SciPy; `pip install sklearn numpy scipy`.


```python
from nltk.classify import util
from nltk.classify.scikitlearn import SklearnClassifier
from sklearn.linear_model import LogisticRegression
from nltk.corpus import movie_reviews

classifier = SklearnClassifier(LogisticRegression(max_iter=100))

# ...

classifier.train(training)
print('Accuracy using Logistic Regression: %7.4f%%' % (util.accuracy(classifier, testing) * 100))
```

The implementation we are going to test out is nearly identical to the implementation in problem 1. Note that SKLearn classifier does not have a `show_most_informative_features` method.

_Note that if you are using these packages with Python 3.7 you will see some Deprecation and Future warnings. You can ignore them._

**TODO: handin your code and report results in comments.**

## 3. Word embeddings

For this problem you have to [install the Gensim package on you machine](https://radimrehurek.com/gensim/install.html); `pip install gensim`.

[Documentation of the Gensim's word2vec module](https://radimrehurek.com/gensim/models/word2vec.html).

```python
from nltk.corpus import movie_reviews
from gensim.models import Word2Vec

sents = movie_reviews.sents() # a vector of vectors of words
model = Word2Vec(sents, iter=5, min_count=5, size=100)
# See the docs for the meaning of these parameters.

# Same as these:
# model = Word2Vec(min_count=1)
# model.build_vocab(sents)
# model.train(sents, total_examples=model.corpus_count, epochs=model.iter)
```

After training a model it is possible to save it to file and load is later for use without having to train again.

```python
model.save('movies-5-5-100.wv')                # Save to file.
model = Word2Vec.load('movies-5-5-100.wv')     # Load again.
```

The model has a couple of methods to query it. Note that you will get an exception if you use a word that is not found in the corpus.

```python
>>> model.most_similar('action', topn=5)
...
>>> model.wv['action']
# Numpy vector representing the word in the model
...
>>> model.wv.doesnt_match('drama action puppy comedy thriller'.split())
...
>>> model.wv.similarity('actress', 'actor')
...
```


**TODO: handin code and report the results of the queries in comments.**

## 4. Back to the features

In section 1 and 2 we used a very simple feature set, i.e. all the words that occured in each review. The purpose of this problem is to get you thinking about what would make good features. For example, what is bad about the _bag of words_ feature set implementation?

Your task is to think of better feature set implementations. That could be a new function to replace `bag_of_words()` or something more elaborate. Describe them in comments, explain why you think they would be an improvement and then try to implement them. The goal can either be to gain a higher accuracy or to streamline the learning process. Report the results also in comments -- remember to say which algorithm is being used.

Feel free to use another corpus instead of the movie reviews if that suites the task better, but remember there has to be some dichotomy or categories (labels) to learn. If you are completely stumped you could use an imaginary corpus that you would then have to describe.



**TODO: handin your descriptions in comments and code.**
