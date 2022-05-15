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



Possible improvement / note for report:  In pre-processing, the I'm -> I am expansion (and abbreviation expansion) only works if there is no punctuation around it. Maybe do that part of the tokenization together with pre-processing? Or the whole thing together? (like if you had originally I'm)
Or maybe just run it again after tokenization?

Also, Allcaps should only find len>1. But for example "   X, " is allcaps ()