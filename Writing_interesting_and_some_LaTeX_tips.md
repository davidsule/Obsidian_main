## Writing and Presenting

20min videos on scientific writing - https://www.coursera.org/learn/sciwrite

https://splasho.com/upgoer5/ - # The Up-Goer Five text editor

Can you explain a hard idea using only the [ten hundred](https://splasho.com/upgoer5/phpspellcheck/dictionaries/1000.dicin) most used words? It's not very easy. Type in the box to try it out.

https://github.com/widged/data-for-good/wiki/Visualisation-::-Choosing-a-chart Choose a chart

https://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3 Choose color schemes (color-blind, print friendly, visually pleasing. Originally for maps, but good for others, too)

http://datacolada.org/34 - My Links Will Outlive You. Content rot. (figure is from 2015)
![[Pasted image 20220310193453.png]]

Solution: [https://archive.org/web/ - Save Page -> archive, share Internet archive link](https://archive.org/web/)

### LaTeX tips

`\usepackage{algorithmic}` for pseudocode
`pandas.DataFrame.to_latex` to generate .tex file for tables from pandas DF
`\input{table.tex}` to import the above it into latex

**Define your own commands:**
- Highlight what still needs to be done (alternative to `\usepackage{todonotes}`)
```TeX
% Define custom command
\usepackage{color}  
\definecolor{myred}{rgb}{.8,.0,.0}  
\newcommand{\todo}[1]{\textcolor{myred}{#1}}
% USe custom command
\todo{Write the abstract}
```
- Some acronyms/names/values that might change (For example, if you call your method LesionKNN and decide to  rename to skin-lesion-knn). When inserting the command, it will always input your text there. So: Enough to change the name in the command definition and it will change everywhere.
```LaTeX
\newcommand{\ourmethod}{\texttt{skin-lesion-knn}}
% when calling the command, it isnert the text. Change the text, it will change everywhere.
```

Push to Github for version control (after main changes)

Organize files:
- different files for different sections:
	- avoid conflicts
	- easy to find bug (if it doesn't compile, you just comment out sections in main document file and see which one is causing the error)
	- include in main: `\input{section_file.tex}` 
- (folder for images)

References:
- local references: refs.bib
- bibliography managers
- Use naming conventions: Google scholar's format: `\cite{cheplygina2019cats}` last name of first author + year + first informative word