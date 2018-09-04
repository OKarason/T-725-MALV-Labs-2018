# Solutions to lab 2

```python
#1

#1.1
wc -l otb.txt   # 36921

#1.2
head -n 5000 otb.txt > small_otb.txt

#1.3
wc -w otb.txt   # 590300
# Alternative:
# grep -ow '[^/ ]*/[^ ]*' otb.txt | wc -w

#1.4
grep -ow 's[^/ ]*/n[^ ]*' otb.txt | wc -l   # 15506

#Note, grep's -c parameter counts lines not matches.

#1.5
grep -w angist otb.txt > angist.txt
# Alternative:
# grep '\bangist/' otb.txt > angist.txt

#2

#2.1

#a) Add space before puntucation.
sed 's/[,.?]/ &/g' mobydick.txt

#b) Remove empty lines
sed ‘/^$/d’        # delete empty lines
sed '/^\s*$/d'     # --""--, including optional whitespace

#c) Print one token per line.
grep -Eo '[^ ]+' mobydick.txt > tokens.txt
# Identical to:
# grep -o '[^ ][^ ]*' mobydick.txt > tokens.txt
# egrep -o '[^ ]+' mobydick.txt > tokens.txt
# Alternative:
# awk '{for (i=1;i<=NF;i+=1) print $i}' mobydick.txt

sed 's/[,.?]/ &/g' mobydick.txt | grep -Eo '[^ ]+' > tokens.txt

# Note, not necessary to removing empty lines explicitly in this solution.

#2.2
sort tokens.txt | uniq -c | sort -nr | head -n 100 > top100freq.txt

# Sort tokens, count and remove duplicates (add count column), 
# sort by number in reverse (count column), extract first 100.

#3
def bigrams_from_tokens( token_list):
    bigram_fd = nltk.FreqDist()

    bigram_fd['. '+token_list[0]] = 1  # first bigram ('.' padding + first word)

    for i in range(1, len(token_list)):
        bigram_fd[token_list[i - 1] + ' ' + token_list[i]] += 1
	
    return bigram_fd

# This problem can be solved in various other ways.
# E.g. using the bigram function mentioned in chapter 1
# to create a list of bigram tuples that are then fed 
# into the FreqDist, or simply used as keys.

#4
names = nltk.corpus.names

cfd = nltk.ConditionalFreqDist()
for name in names.words('male.txt'):
    cfd['male'][name[0]] += 1
for name in names.words('female.txt'):
    cfd['female'][name[0]] += 1

# This problem is almost identical to one whose solution
# is given at the end of chapter 2.4.1. By changing
# name[-1] (last letter) to name[0] (inital letter) we get.
cfd = nltk.ConditionalFreqDist(
           (fileid[:-4], name[0])
           for fileid in names.fileids()
           for name in names.words(fileid))

# This creates a list of tuples (gender, initial) that the cfd is initialized with.
```