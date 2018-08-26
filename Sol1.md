# Solutions to lab 1

```python
#1, e.g.
my_str.upper()
my_int.str()
my_float.is_integer()
my_list.pop(2)
my_dict.keys()

#2
from nltk.book import text6
text6.concordance("knight")
text6.similar("knight")
text6.collocations(25)

#3
#    \w+|[^\w\s]+   # one or more word-chars or one or more not (word-chars or whitespace)

#4, e.g.
#    ^[A-Z]+$       # uppercase words, one or more uppercase letters
#    ^\d\D+$        # ordinal numbers (1st, 2nd, 3rd ...), a digit followed by one or more non-digit

#5
>>> fd['starboard']
16
>>> fd.max()
','
>>> fd.most_common(10)
[(',', 18713), ('the', 13721), ('.', 6862), ('of', 6536), ('and', 6024), ('a', 4569), ('to', 4542),
(';', 4072), ('in', 3916), ('that', 2982)]

# You only needed to give answer in the last part.
# But to do it in code you could have done something like:

>>> from nltk.corpus import stopwords
>>> ignore = stopwords.words('english')
>>> fd100 = fd.most_common(100)
>>> anwc = re.compile('\W') # any non word character
>>> [t for t in fd100 if not anwc.match(t[0]) and t[0].lower() not in ignore][0]
('whale', 906)

```
