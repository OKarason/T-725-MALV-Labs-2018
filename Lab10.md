# Lab 10

**Try to complete as much as you can. Hand in a **text** file (''FullName_lab10.{pdf|doc|txt}'') with what you have finished in Canvas before midnight tomorrow (26 October).**

_*Note that no programming is required for this lab. But you will be required to think like a computer and may use computational tools to help you.*_


## 1. Resolving Coreferences with a simple Algorithm

In this exercise you will attempt to resolve coreferences in the following discourse:

```
The man in the brown coat was no stranger to extraordinary events. 
He had been in the private investigation business for longer than Cuban cigars. 
What happened here did not shake his sense of reality. 
He had seen it all before. Back in the day, it was simply called "magic". 
In fact, the spell that had been cast here felt strangely familiar. 
Someone was coming back from his past. A dangerous criminal had escaped from prison. 
And he had put him there.
```

First, pretend that you are a computer that is processing this text and trying to understand what all the personal pronouns such as _he_, _she_ and _they_ are referring to. Follow the simplistic method of using a recency list and morphosyntactic feature agreement. Proceed as follows:

  * Identify all noun phrases (NPs).
  * Tag each NP with number and gender.
  * Walk through the NPs from beginning to end, and do the following:
    - If the NP is not a personal pronoun, create a new discourse entity at the front of a list L that represents our discourse model (use a unique name for the entity, such as LADLE-MAKER1). Give the discourse entity the same number and gender as the NP and record the NP itself as the first reference to this entity (antecedent).
    - If the NP is a personal pronoun, link it to the first discourse entity in L that matches in number and gender, starting with the most recent entry. Record our NP as a subsequent reference to the entity (anaphor).
  * Show each entry of L on a separate line, with all found coreferences to it (antecedent and anaphors).

_*Note* that you could use POS tagging [Lab 4](Lab4.md) and Regular Expression NP-Chunking [Lab 8](Lab8.md) to aid you in the process._

## 2. Resolving Coreferences Manually

Now return to your human form and manually construct a table that contains all the discourse entities you can find in this text, and for each entity list all noun phrases that coreference it. Be aware that a few referring expressions may refer to discourse entities that were not explicitly created by another noun phrase, but are still a part of the context.

## 3. Compare the Models

Finally Compare the two discourse models that you have created and answer the following questions:
  - How well/poorly did the computer algorithm perform in interpreting the pronouns? How well/poorly did it do in identifying discourse entities and coreferences to them in general?
  - What reasonably tractable modifications could you make to the compute algorithm to improve its discourse modelling performance?
  - What aspects of your manual approach do you think will be particularly hard for computers to imitate?
  - There are three referring expressions in the last sentence: _He_, _him_ and _there_. What do they refer to and how do you know this? What would a computer need to know to draw the same conclusion?

  **Handin the list, the table and the anwers to the four questions.**
