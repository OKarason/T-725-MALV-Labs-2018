# Lab 4

**Try to complete as many of the problems as you can. Hand in your code in Canvas before midnight tomorrow (14 September). A single file, `FullName_lab4.py` containing the solutions in the same order as the given problems.**

**_If you can't manage to complete a particular problem please hand in your incomplete solution._**

Chapter 4 in the [NLTK book](http://www.nltk.org/book/) is relevant to this lab.


## 1. Down the Garden Path

Lets get started by trying out the POS-Tagger in NLTK. See if you can think of some ambiguous sentences that confuse the tagger -- or google for some [garden path sentences](http://www.fun-with-words.com/ambiguous_garden_path.html).

```python
import nltk

text = nltk.word_tokenize("The horse raced past the barn fell.")

tagged_text = nltk.pos_tag(text)
print(tagged_text)
```

Use `nltk.help.upenn_tagset()` to look up the meaning of the tags.

```python
nltk.help.upenn_tagset('NN')
nltk.help.upenn_tagset('NN.*')

#FYI, there is also a lookup function for the tagset used for the Brown corpus:
nltk.help.brown_tagset('NN')
```

See if making slight changes to the wording of the sentences is enough for the tagger to tag it correctly. For example adding `that was` after `horse` in the example above.

**TODO: handin code with example sentences, with and without changes.**

## 2. Training and Testing Data, and Finding the Baseline 

```python
from nltk.corpus import brown
```

Get the tagged sentences from the Brown corpus and separate them into training (90%) and testing parts (10%). (Note: we will use them also in the two remaining problems). You can limit the corpus to the `news` category during testing but use the whole corpus for the handin.

Train the **Unigram Tagger** on the training sentences using **Default Tagger** as backoff. Use 'NN' as the default tag.

Evaluate the taggers performance on the testing sentences. How well does it do? Do you think this is a fair baseline to measure other taggers against?

**TODO: handin code and answers in comments.**

## 3. A Cascade of Taggers

Extend the tagger combination in [[http://www.nltk.org/book/ch05.html#combining-taggers|5.4 Combining Taggers]] by defining a `TrigramTagger` called `t3`, which backs off to `t2` as suggested.

```python
t0 = nltk.DefaultTagger('NN')
t1 = nltk.UnigramTagger(brown_train_sents, backoff=t0)
t2 = nltk.BigramTagger(brown_train_sents, backoff=t1)
print(t2.evaluate(brown_test_sents))
[...]
```

Evaluate both `t2` and `t3` and report the difference. You can also evaluate `t0` and `t1` to see what each step brings to the overall result.

**TODO: handin code and report results in comments.**

## 4. Most frequent tag of Hapax legomenon 

Instead of using the most common tag overall for the Default Tagger some say that [_hapax legomenon_](https://en.wikipedia.org/wiki/Hapax_legomenon) is a better model for unknown words. That is, that words that occur only once in the corpus are likely to be representative of the words that never occur, the unseen words.

See if you can write code to find the most common tags in the set of words that occur only once in the Brown corpus. You might prefer to use `brown.tagged_words()` here, and even `brown.tagged_words(categories='news')` during testing.

What is the most common tag of _hapax legomenon_?

Looking at the twenty most common tags, how do you think the difference between the overall model and hapax legomenon model will develop as the training corpus grows larger?

**TODO: handin code or describe method, and answer in comments.**