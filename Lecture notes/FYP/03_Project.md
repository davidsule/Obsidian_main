# 02 Lecture



# Project notes

- Lecture 01: Manual tokenization of a small subset of data and compare with result from tokenizer
- Calculate Word boundary recall (R)

![[Pasted image 20220504142801.png]]


### Recommended Readings from Christian:
I would recommend starting with the textbook by Jurafsky and Martin, one of the standard textbooks in NLP, particularly Chapters 2 (Preprocessing) and 3 (N-gram language modelling). You can find the chapters here: https://web.stanford.edu/~jurafsky/slp3/
For the part on data annotation and annotation quality, I'd go directly to the journal article by Artstein and Poesio: https://aclanthology.org/J08-4004.pdf


To review:
- L02:
	- Freuqncy stats in code

- L03:
	- Smoothing algorithmes (WB KN) (theory)
	- Sentence scoring (theory)
	- Score and logscore in code
	- Perplexity in code
	- (Backoff and Interpolation)

- L04:



How to add extra features to model and GSCV?
SRILM



Abbreviation expansion changes to word to lowercase -> makes GingerIt's work harder + shows up as extra GingerIt correction. But no, beacause abbreaviations are often uppercase but referring to lowercase stuff. Hard to separate: I'm hungry AF. -> I'm hungry as fuck from Ain't she gonna take him home? -> Isn't she gonna take him home? Okay, maybe if abbreviation's first letter is uppercase but not the rest -> First word of expansions capitalize, if allcaps or lowercase, then lowercase.

Abbr dicts: Some lowercase, some upper case (like twitter slang) - > let's lowercase everything in the input dictionaries, and then search for the lowercased word? (not lwoercase word is searched for now in Marta's new function.) Plus see above paragraph.

Plus, let's delete HAND (have a nice day) from twitter slang -> way more likely to be misinterpreted (no HAND in train hate). Actually no corpus has it in this sense, only actual hands.



Lemmatization: If no tag --> maybe fall back to noun? 

How nltk pos_tag's tagset types work with lemmatizer?


Train-Val-Test split and Cross-Validation
https://machinelearningmastery.com/training-validation-test-split-and-cross-validation-done-right/


