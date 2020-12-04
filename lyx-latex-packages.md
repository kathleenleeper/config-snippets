Using Lyx is a way to avoid LaTeX, but unfortunately I particularly like the Tufte classes, as I am a cheap-n-easy design b***h,  which upon initial install you will find does not work due to not having all the classes you need.

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