Using Lyx is a way to avoid LaTeX, but unfortunately I particularly like the Tufte classes, as I am a cheap-n-easy design b***\h,  which upon initial install you will find does not work due to not having all the classes you need.

# installing latex dependencies with DNF
However, instead of wrestling with system files, once Lyx is installed, you can use dnf to install additional missing classes.

problem description: https://wiki.lyx.org/LaTeX/TeXLivePackages
solution: https://docs.fedoraproject.org/en-US/neurofedora/latex/

The delightfully simple syntax is:
```
$ sudo dnf install 'tex(beamer.cls)' 
```

To get Tufte specifically, the missing dependencies (as of time of writing, of course):
```
$ sudo dnf install 'tex(tufte-handout.cls)' 'tex(hardwrap.sty)'
```
If you have opened LyX, reconfigure and restart the program to load changes, as per usual.

# managing Tufte citations

Using the Tufte handout class in LyX is beautiful and my preferred notetaking format, but citations are not fun. Among other reasons, as of writing, the only way to achieve proper side citations is by copying the sample handout file and editing appropriately. This is...not viable. Even when done 'properly' (i.e. Lyx rewrites the /cite inset to be /footnote/citep{} in the sample handout), the citations are incredibly long (full author list, title, all information) because they are meant to serve as full citations, and they are long *every* time they are cited. Sadly, there isn't tracking and the consequent ibid. type abbreviations.

Biblatex solves these. Implementing this takes a couple of steps, and citations need to be manually input with \autocite{key}, but...they're pretty, and they take Biblatex formatting commands, which means if you do use a full citation in the side notes it doesn't do it everytime. Onwards.

## Biblatex setup

### In LyX: Document settings

1. Add "nobib" as an class option.
2. Add this to the preamble (and change the options as you like -- specifically style may be of interest, especially if you want full ciations instead of just author-year).
```
\usepackage{hyphenat} % this hyphens things
\usepackage[
  style=authoryear-comp,
  autocite=footnote,
  backend=biber,
  % isbn=false, %optional line
  % url=false, %optional line
  % eprint=false %optional line
]{biblatex}

\addbibresource{PATH_TO_YOUR_BIB.bib} %you can stack these
```
3. Change the bibliography generation to biber; default BibTex style plain (this last may not matter).

## In the main document

4. Comment out or delete the LyX Bibliography insert. In ERT, insert
```
\printbibliography
```

## Citation syntax
To produce a footnote style citation, in ERT use:

``` \autocite{key} ``` 

Lots of additional options -- look up biblatex citation patterns for variations (\cite, \parencite, \citetitle)
