---
title: "Quantification"
date: 2021-02-02T17:56:51-04:00
draft: false
---


For this week's exercise, I used regular expressions to detect all of the named people in Corpus S. I've noticed, while cleaning OCR, that Surrealist text seems to directly name many Surrealists and other influential figures. I wanted to see if that theory was true. I used the following regex:

```
([A-Z][a-z]*) +([A-Z][a-z]*)
```

on RegExr to find all of the phrases that contained two capitalized words in each of the text files in Corpus S. Of course, this did not give me flawless results; I still had to sort through the resulting list to determine names from names of places, texts, and other phrases that weaseled their way into my search results.

I can confirm that many texts name a lot of Surrealists--especially those written by Andre Breton. Some of them didn't name any Surrealists at all, which is telling. It seems that the automatic writing texts named Surrealists much less than the novels and essays. 

The named_entities_in_corpus_s.csv file includes a full list of the names detected in each text. I listed each name, its corresponding text, and a quick attempt to recognize the person's significance. Namely, which people mentioned were Surrealists. I found that the Surrealists Benjamin Peret, Paul Eluard, and Robert Desnos were mentioned in several of the texts. I also found other people were used frequently, like philosophers, French royalty, poets, artists, etc. Overall, I'm happy with the results. I definitely could have done this a better way. I looked into using Named Entity Recognition and Natural Language Processing but ran into some errors with Python on my personal device (not sure why). In the future, I think using Python or R would give me better results. 

There were also lots of names that weren't picked up. For instance, three-word names were cut off. Also, single-word names were not detected. (I spotted a few during the process and included them in parentheses in the table.) Some names were cut off due to titles, like Saint Joan of Arc or King Charles V. Another issue is that the regex left out any phrase that came after a letter with an accent, so Benjamin Péret became Benjamin P. I had to make some biased decisions to figure out to what person I believed the phrase to be refering or go in and search the text to discover the full name.