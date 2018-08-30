# Lab 2

**Try to complete as many of the problems as you can. Hand in your code in Canvas before midnight tomorrow (31 August). A single file, `FullName_lab2.txt` containing the solutions in the same order as the given problems.**

**_If you can't manage to complete a particular problem please hand in your incomplete solution._**

Chapter 2 in the [NLTK book](http://www.nltk.org/book/) is relevant to this lab as well as the respective `man` pages for the Unix tools. Windows users might want to install [Git Bash](https://git-scm.com/downloads) for the first two problems.


# 1. Text processing tools

Use the [`otb.txt`](otb.txt) file from the lab's Github repo and any of `wc`, `head`, `tail` and `grep`.

**TODO: Show the commands you would use to do the following:**
1. **Find the number of lines in `otb.txt`.**
2. **Create a new text file named `small_otb.txt` containing only the first 5000 lines of `otb.txt`.**
3. **Find the number of tokens in `otb.txt`.**
4. **Find the number of nouns starting with the letter _s_ in `otb.txt`. (format 'lexeme/tag', nouns have tags starting with _n_).**
5. **Create a new file named `angist.txt` that contains only the lines from `otb.txt` that have the lexeme _angist_ in them.**

# 2. More text processing tools

Use the [`mobydick.txt`](mobydick.txt) file from the lab's Github repo and any of `wc`, `head`, `tail`, `grep`, `uniq`, `sort`, `sed`, and `awk`.

**TODO: Show the commands you would use to do the following:**
1. **Create a new text file named `tokens.txt`. Containing one token per line. It would be preferable if (1b) punctuation tokens were handled seperately and (1c) that the file contained no empty lines.**
2. **Create a new text file named `top100freq.txt` that contains two columns with frequency and token for the 100 most frequent tokens in `tokens.txt`.**

# 3. Frequency Distributions and N-grams

Chapter one introduced FreqDist() which we used to create a frequency distribution for the tokens in Moby Dick. Its functionality can be used for more than single words.

**TODO: Define a function that creates a frequency distribution for bigrams from list of tokens.***

```python
def bigrams_from_tokens(token_list):
    bigram_fd = nltk.FreqDist()
    
    #add code
    
    return bigram_fd
```

Note that ''ConditionalFreqDist'' is not suitable for this task.

Use the function you defined to print out the twenty most frequent bigrams in Moby Dick. How often does the bigram "Moby Dick" occur?

Example output:
```python
>>> moby_bigrams = bigrams_from_tokens(tokens)
>>> moby_bigrams.most_common(10)
[(', and', 2607), ('of the', 1847), ("' s", 1737), ('in the', 1120), (', the', 908), ('; and', 853), ('to the', 712), ('. But', 596), (', that', 584), ('. "', 557)]
>>> moby_bigrams['Moby Dick']
83
```

**OPTIONAL TODO: Now alter the function to make an n-gram version for extra credit.**

Note that you have to make special arrangements for n > 2 to make sure that the n-grams do not cross over between sentences. One solution would be to copy the token_list and add '.' padding (n-2 times) after punctuation.

```python
def ngrams_from_tokens( token_list, n=2):
    ngram_fd = FreqDist()

    #copy and pad at both ends
    #add padding after punctuation

    #loop through the list and update ngram_fd

    return ngram_fd
```

# 4. Initial letter frequency for males vs. females

**TODO: Define a conditional frequency distribution over the Names corpus that allows you to see which initial letters are more frequent for males vs. females** cf. 4.4 in chapter 2 [http://www.nltk.org/book/ch02.html#fig-cfd-gender].

Exercise 8 in chapter 2: [http://www.nltk.org/book/ch02.html]

For which gender are names starting with 'Z' more numerous?
