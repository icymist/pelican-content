Title: Using git and latexdiff
Date: 2015-04-10 17:41:40
Category: Productivity
Tags: latex, git, linux

`latexdiff` makes a diff of an `old` latex file and a `new` latex file and gives a new `diff` file.
The `diff` file can now be compiled and will show all the additions and deletions in the `new` file compared to the `old` one.

    :::bash
    latexdiff old.tex new.tex > diff.tex
    pdflatex diff.tex

`latexdiff` might fail if the encodings of the old and the new tex files are different.

To convert a text file with Windows line endings to unix line endings and encoded in ASCII:

    :::bash
    iconv -f CP1252 -t ASCII//TRANSLIT windows-CP1252.txt | dos2unix > unix-ascii.txt

Use the `TRANSLIT` option to overcome issues related to failed encodings of certain characters.

Use `git-latexdiff` to compare two version of the document in version control.
For example, suppose that you are writing a paper.
You call the paper `paper.tex` and just sent a version, after committing it, to your supervisor for corrections.
Your supervisor has sent back paper.tex with corrections and comments.
You can now just overwrite the old paper.tex with the new one and do:

    :::bash
    git-latexdiff --main paper.tex <sha-of-old-commit> --

This will compare the old commit with the one in the working directory (represented by `--`).
