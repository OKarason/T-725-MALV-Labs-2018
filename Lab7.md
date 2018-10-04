# Lab 7

**Hand in your code in Canvas before midnight tomorrow (5 October). One or two, `.py` files containing the solutions.**

**_Try to complete as much as you can. If you can't manage to complete a particular problem please hand in your incomplete solution._**

## 1. Parse CFG

Lets start with the CFG grammar from [section 3.3 in chapter 8](http://www.nltk.org/book/ch08.html#recursion-in-syntactic-structure) and expand upon it.

```python
grammar = nltk.CFG.fromstring("""
  S  -> NP VP
  NP -> Det Nom | PropN
  Nom -> Adj Nom | N
  VP -> V Adj | V NP | V S | V NP PP
  PP -> P NP
  PropN -> 'Buster' | 'Chatterer' | 'Joe'
  Det -> 'the' | 'a'
  N -> 'bear' | 'squirrel' | 'tree' | 'fish' | 'log'
  Adj  -> 'angry' | 'frightened' |  'little' | 'tall'
  V ->  'chased'  | 'saw' | 'said' | 'thought' | 'was' | 'put'
  P -> 'on'
  """)

parser = nltk.ChartParser(grammar)
sent = 'Joe saw a squirrel'.split()
for tree in parser.parse(sent):
    print(tree)
    #tree.draw()
```

### 1.1 Understand and Expand

Play around with the grammar and make sure you understand how the production rules work. Add some new words (terminals) to the productions and make up some sentences to parse.

You can use the ``draw`` method to render parse-trees.

### 1.2 Add Personal Pronouns

Add some [personal pronouns](https://en.wikipedia.org/wiki/Pronoun#Personal) to the grammar.

Examples: 'I saw a bear', 'he frightened me'

### 1.3 Transitive vs. Intransitive Verbs

Add some verbs and alter the grammar to make it differentiate between [transitive](https://en.wikipedia.org/wiki/Transitive_verb) and [intransitive verbs](https://en.wikipedia.org/wiki/Intransitive_verb).

Examples: 'the bear died', 'Joe saw the bear was dead', 'Buster gave Joe a fish'

### 1.4 Add Number Agreement

Alter the grammar to add [number agreement](https://en.wikipedia.org/wiki/Agreement_(linguistics)#Number), start with something like ``S -> NPsg VPsg | NPpl VPpl`` and continue down the productions. The terminals could for example be something like: ``Nsg -> 'bear' | ...``, ``Vtsg -> 'eat' | 'eats' | ...``. Add plural forms of nouns.

Examples: 'a fish dies', 'the bears frightened a little squirrel'

**What to hand in: Your CFG grammar with all the modifications. Code to print out a couple of sentence parses for each subsection here above.**

## 2. Parse PCFG

Now create a probabilistic version of your grammar (see [section 3.6 in chapter 8](http://www.nltk.org/book/ch08.html#weighted-grammar)) by adding made up, but reasonable probabilities to your productions.

```python
pgrammar = nltk.PCFG.fromstring("""
  S  -> NPsg VPsg [0.5] | NPpl VPpl [0.5]
  ...
  """)

viterbi_parser = nltk.ViterbiParser(pgrammar)
for tree in viterbi_parser.parse('Buster saw a bear'.split()]):
    print(tree)
```

Try to find ambiguous sentences to parse with the grammar. Then alter the production probabilities to change which is the most probable parsing.

**What to hand in: A PCFG grammar. Code to print out the sentence parses you tried out.**
