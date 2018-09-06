# Lab 3

**Try to complete as many of the problems as you can. Hand in your code in Canvas before midnight tomorrow (7 September). Three files, `myscript.py`, `mytokenizer.py` and `FullName_lab3.txt` containing the solutions to problems 3 and 4.**

**_If you can't manage to complete a particular problem please hand in your incomplete solution._**

Chapter 3 in the [NLTK book](http://www.nltk.org/book/) is relevant to this lab as well as the [NLTK Collocations howto](http://www.nltk.org/howto/collocations.html) for the last problem.


## 1. `myscript.py`: argv

```python
from sys import argv

print(argv)
```

The list ''argv'' contains the name of the script plus any parameters used in the invocation.

```
$ python myscript.py One TWO three
['myscript.py', 'One', 'TWO', 'three']
```

If the number of parameters is fixed beforehand you can unpack them all into variables. Otherwise you use the index number to get a particular parameter.

```python
first_param = argv[1]    #using the index

script_name, first, second, third = argv     #unpacking the argv list into four variables
```

**TODO: Create a script named `myscript.py` that produces the following output when executed with the parameters indicated:**

```
$ python myscript.py file1.txt file2.txt
Number of parameters: 2
Script name: myscript.py
First parameter: file1.txt
Second parameter: file2.txt
```

[Information on executing Python scripts from the command line](https://docs.python.org/3.3/using/cmdline.html#using-on-cmdline).

## 2. `mytokenize.py`: Read file

**TODO: Create a script name `mytokenize.py` that reads a file contents, tokenizes them, removes stopwords and print out the remaining tokens, one per line.**

```python
from sys import argv
from nltk import word_tokenize
from nltk.corpus import stopwords

#Get file name from argv (see problem 1).
#Open file for reading.
#Read contents into a string.
#Tokenize the string.
#Remove stopwords (words in stopwords.words('english')).
#Print out the tokens, one per line.
```

You should be able to invoke the script using `python mytokenize.py test.txt`.

## 3. List comprehension

**TODO: Rewrite the following loop using "list comprehension"**:

```python
>>> sent = ['The', 'dog', 'gave', 'John', 'the', 'newspaper']
>>> result = []
>>> for word in sent:
...     word_len = (word, len(word))
...     result.append(word_len)
>>> result
[('The', 3), ('dog', 3), ('gave', 4), ('John', 4), ('the', 3), ('newspaper', 9)]
```

(Problem 10 in [Chapter 3](http://www.nltk.org/book/ch03.html)).

List comprehensions enable the descriptive construction of lists in a very compact, yet easily readable way. [The interwebs are full of learning resources](https://www.google.com/search?q=list+comprehension+python|google).

**NOTE: If you feel this problem is easy you should instead try your hand at problems 31 and 41.**

## 4. Bi- and Trigram Collocation finders

```python
import nltk
from nltk.collocations import *
from nltk.metrics import BigramAssocMeasures, TrigramAssocMeasures
from nltk.corpus import brown, stopwords
```

TODO:
  * Create a Bigram Collocation Finder for the Brown Corpus.
  * Apply a filter to remove bigrams that occur less than two times.
  * Apply a filter to remove bigrams that contain stopwords (`stopwords.words('english')`) and words that are two characters or shorter.
  * Print out the 20 most **frequent bigrams**.

REPEAT THIS FOR BOTH:
  * Bigrams using a window of size 3.
  * Trigrams.
