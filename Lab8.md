# Lab 8

**Hand in your code in Canvas before midnight tomorrow (12 October). One or two `.py` files containing the solutions.**

_Try to complete as much as you can. If you can't manage to complete a particular problem please hand in your incomplete solution._

**Answer questions or report results in comments in your code.**

[Section 2 in chapter 7 contains information on Chunking](http://www.nltk.org/book/ch07.html#chunking).

## 1. Training a tagger to Chunk NPs

```python
import nltk.chunk, nltk.tag
```

We will be using the CoNLL 2000 corpus for training and test data since it contains chunk IOB tags (I-inside, O-outside, B-begin) as well as POS tags.

```python
from nltk.corpus import conll2000
test_sents = conll2000.chunked_sents('test.txt', chunk_types=['NP'])
train_sents = conll2000.chunked_sents('train.txt', chunk_types=['NP'])
```

Use the `UnigramChunker` class from Example 3.1 in [section 3.2 in Chapter 7](http://www.nltk.org/book/ch07.html#simple-evaluation-and-baselines).

```python
class UnigramChunker(nltk.ChunkParserI):
    def __init__(self, train_sents):
        train_data = [[(t,c) for w,t,c in nltk.chunk.tree2conlltags(sent)]
                      for sent in train_sents]
        self.tagger = nltk.UnigramTagger(train_data)

    def parse(self, sentence):
        pos_tags = [pos for (word,pos) in sentence]
        tagged_pos_tags = self.tagger.tag(pos_tags)
        chunktags = [chunktag for (pos, chunktag) in tagged_pos_tags]
        conlltags = [(word, pos, chunktag) for ((word,pos),chunktag)
                     in zip(sentence, chunktags)]
        return nltk.chunk.conlltags2tree(conlltags)
```

Train an NP chunker on CoNLL 2000 corpus. Use the `test_sents` to evaluate the newly trained NP chunker.

```python
chunker = UnigramChunker(train_sents)

print(chunker.evaluate(test_sents))
```

Try out the chunker on some sentences.

```python
sentence = nltk.pos_tag('While winter reigns the earth reposes but these colorless green ideas sleep furiously.'.split())

print(chunker.parse(sentence))
```

### 1.1 Evaluate UnigramChunker

**TODO: Report the evaluation results from using the UnigramChunker on the train_sents.**


### 1.2 Create MyChunker and Evaluate it

**TODO: Create a new class based on UnigramChunker that uses a trigram tagger with an unigram tagger as a backoff in `__init__` (see [5.4 Combining taggers](http://www.nltk.org/book/ch05.html#combining-taggers)). Evaluate your new chunker and report the results.**

### 1.3 Get a feel for NP chunking

**TODO: Extract sentences from one of the many corpora available in NLTK or/and make up some sentences with complex NPs. Parse them with the chunker you created and examine the chunks.**


## 2. A Regular Expression NP Chunker


```python
pattern = '''
    NP: {<DT>?<NN>} #chunk rule: optional determiner followed by a noun
    '''

re_chunker = nltk.RegexpParser(pattern) # create a re chunk parser

print(re_chunker.parse(sentence))
```

You can use the CoNLL `test_sents` to evaluate your hand-crafted NP chunker.

```python
print(re_chunker.evaluate(test_sents))
```

### 2.1 Improve the Regexp Chunker

**TODO: Improve upon the Regular Expressions NP chunking patterns.** You could use the tag patterns you discovered in 1.3 to guide you. [Section 2 in chapter 7](http://www.nltk.org/book/ch07.html#chunking) also contains some relevant examples.

```python
pattern = '''
    NP: {[...]} #first NP chunk rule
        {[...]} #second NP chunk rule
        {[...]} #and so on ...
    '''
```

Note the special RE Syntax for Chunk Rules:
```
 Example:      Matches:

 {<A>}         #Tag A
 {<A|B>}       #Tag A or tag B
 {<A><B>}      #Tag A followed by tag B
 {<A>?<B.*>}   #Optional tag A followed by tag Bx where x is some optional character
 {<A><A><A>*}  #Two or more A tags in a row.
```

Remember that you can use `nltk.help.upenn_tagset()` to look up the tags.


**NOTE: You should at least be able to get the IOB Accuracy for `test_sents` above 66%. Report you results.**
