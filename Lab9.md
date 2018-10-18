# Lab 9

**Try to complete as much as you can. Hand in a python code file (`fullName_lab9.py`) and a grammar file (e.g. `grammar.fcfg`) with what you have finished in MySchool before midnight tomorrow (19 October).**

If you can't manage to complete the problem please hand in your incomplete code -- comment it out if it produces an error.

## 0. Introduction

Create a short python script that uses the NLTK to evaluate whether a statement provided in natural language is True or False for a given model of the world. _You are given complete freedom to choose what this model is like and what sentences your system understands._

The exercise can be divided into two distinct parts:
* Semantic analysis of the natural language input using a parser and a grammar with semantic attachments, resulting in a FOL representation of the input.
* Evaluating the FOL representation of the input against a model created to represent a particular state of affairs in the world.

## 1. Parsing using "feature-based CFG" with semantic attachments

**Semantic analysis of the natural language input using a parser and a grammar with semantic attachments, resulting in a [First-Order Logic](https://en.wikipedia.org/wiki/First-order_logic) (FOL) representation of the input.**

You can perform syntax-driven semantic analysis of the natural language input sentence (as seen in chapters 18.1 and 18.2 in the text book) by building a NLTK parser from a "feature-based context free grammar" (fcfg) that contains semantic attachments as features. [Feature-based parsing is covered in chapter 9 in the NLTK book](http://www.nltk.org/book/ch09.html).

Building the parser is as simple as calling `nltk.load_parser("<fcfg filename>")` and assigning the resulting parser object to a variable like `parser`. NLTK creates the right kind of parser by inspecting the grammar. To begin with, simply use the fcfg file provided in the examples in [chapter 10.4 in the NLTK book](http://www.nltk.org/book/ch10.html#the-semantics-of-english-sentences): `nltk_data/grammars/book_grammars/simple-sem.fcfg`. [View grammar file contents](https://raw.githubusercontent.com/nltk/nltk_teach/master/examples/grammars/book_grammars/simple-sem.fcfg).

```python
>>> from nltk import load_parser
>>> parser = load_parser('grammars/book_grammars/simple-sem.fcfg', trace=0)
>>> sentence = 'Angus gives a bone to every dog'
>>> tokens = sentence.split()
>>> for tree in parser.parse(tokens):
...     print(tree.label()['SEM'])     ## print the resulting semantic representation
all z2.(dog(z2) -> exists z1.(bone(z1) & give(angus,z1,z2)))
```

Create a copy of the grammar and change the lexicon to reflect the kind of sentences you wish to work with (you are not required to make drastic changes to the semantic attachments other than changing the names of the terms and the predicates). You should make sure you can parse at least one kind of quantified sentence like "some monkeys love banana". Test that you get the FOL representation you expect.

## 2. Building a model and evaluate against it

**Evaluating the FOL representation of the input against a model created to represent a particular state of affairs in the world.**

You can build a model in NLTK using the exact same set-based model-theoretic semantics as the text book explains in chapter 17.2 and shows in Figure 17.2. Note that a NLTK model already specifies certain denotation and interpretation. That is, you include specific Objects, Properties and Relations and associate them with certain elements of the domain, sets and sets of tuples, respectively.

You build the model object from a special string representation of the model contents using the `nltk.Valuation.fromstring()` function which returns a so-called valuation. An example of this is given in the [3.4 Truth in Model section in chapter 10 in the NLTK book](http://www.nltk.org/book/ch10.html#truth-in-model).

```python
>>> v = """
... bertie => b
... olive => o
... cyril => c
... boy => {b}
... girl => {o}
... dog => {c}
... walk => {o, c}
... see => {(b, o), (c, b), (o, c)}
... """
>>> val = nltk.Valuation.fromstring(v)
>>> print(val)
{'bertie': 'b',
 'boy': {('b',)},
 'cyril': 'c',
 'dog': {('c',)},
 'girl': {('o',)},
 'olive': 'o',
 'see': {('o', 'c'), ('c', 'b'), ('b', 'o')},
 'walk': {('c',), ('o',)}}
```

If you store the valuation in variable `val` you can then pass it, along with its domain, into the constructor of a new Model: `m = nltk.Model(val.domain, val)`. You can then start evaluating FOL statements (in string format) against the model like this: `m.evaluate("all monkeys love banana", nltk.Assignment(val.domain))` (The second parameter contains any variable substitutions if there are any, in this case there are none and we are passing the default assignments).

```python
val = nltk.Valuation.fromstring(model_representation)
var_assignments = nltk.Assignment(val.domain)
m = nltk.Model(val.domain, val)

# evaluate a semantic representation given the world model
m.evaluate("...", var_assignments) 
```

Test your model by evaluating various statements.

## 3. Interactive python script

Once you have the two parts working you glue them together in a python script. You should allow users to type in sentences and see their truth value printed until they finally type "quit". When the program starts, you should print out some useful information, for instance, provide samples of sentences that would produce results.

```
--> John loves Mary
True
--> every boy loves a girl
False
--> some monkeys love banana
True
--> quit
```

Here we want to pass `tree.label()['SEM']` from the parser as the first argument to the `evaluate()` method of the model.


**Note** that `tree.label()['SEM']` returns an object of type `nltk.sem.logic.ApplicationExpression` (as can be seen by checking its type with `type()`) and not a string even though you can print it out. To use it in `evaluate()` it has to be turned into a string. The simplest way to do that is to use `str(semantic_expression)` or the format operator `"%s" % semantic_representation` which return a string.
