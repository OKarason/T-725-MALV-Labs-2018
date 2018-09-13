
```python
#1
from sys import argv

print('Number of parameters: ', len(argv)-1)
print('Script name: ', argv[0])
print('First parameter: ', argv[1])
print('Second parameter: ', argv[2])

#2
from sys import argv
from nltk import word_tokenize
from nltk.corpus import stopwords

with open(argv[1]) as infile:
    for w in word_tokenize(infile.read()):
        if w.lower() not in stopwords.words('english'):
            print(w)

#Since files are context managers, they can be used in a with-statement.
#The file will close when the code block is finished, even if an exception occurs

#3
[(w, len(w)) for w in sent]

#4
import nltk
from nltk.collocations import *
from nltk.metrics import BigramAssocMeasures, TrigramAssocMeasures
from nltk.corpus import brown, stopwords

bam = BigramAssocMeasures

corpus =  brown.words()  # ok to use a subset e.g. 'ca01' for testing

finder = BigramCollocationFinder.from_words(corpus)

word_filter = lambda w: len(w) < 3 or w.lower() in stopwords.words('english')
#def word_filter(w): return len(w) < 3 or w.lower() in stopwords.words('english')


finder.apply_freq_filter(2)
finder.apply_word_filter(word_filter)

print(finder.nbest(bam.raw_freq, 20))


finder_win3 = BigramCollocationFinder.from_words(corpus, window_size=3)
finder_win3.apply_freq_filter(2)
finder_win3.apply_word_filter(word_filter)
print(finder_win3.nbest(bam.raw_freq, 20))


tam = TrigramAssocMeasures

finder_tri = TrigramCollocationFinder.from_words(corpus)
finder_tri.apply_freq_filter(2)
finder_tri.apply_word_filter(word_filter)
print(finder_tri.nbest(tam.raw_freq, 20))
```