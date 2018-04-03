## Natural language processing

Programmatical approach to solve the riddles requires a huge Greek text corpora.
Bigger it is, the better. I will download and preprocess available open source
Greek corpora, which is a quite daunting task for many reasons. Programming
language of my choice is Python<!-- cite author="python.org" title="Python" date="" location="" type="website" href="http://python.org" --> for it has plenty of good and stable open source
libraries required for my work. Python is widely recognized in academic and
scientific field and well oriented to the research projects.

I have left the most of the overly technical details of these chapters
for the enthusiasts to read straight from the commented code in
[functions.py](https://git.io/vAS2Z)<!-- cite author="Marko Manninen" title="functions.py" date="2018" location="" type="website" href="https://git.io/vAS2Z" --> script. By collecting
the large part of the used procedures to the separate script maintains this
document more concise too.

In the end of the task of the first chapter, I'll have a word database
containing hundreds of thousands of unique Greek words extracted from the
naturally written language corpora. Then words can be further used in the riddle
solver in the second chapter.

<!-- note -->
Note that rather than just reading, this, and the following chapters can also be
run interactively in your local Jupyter notebook<!-- cite author="jupyter.org" title="Jupyter notebook" date="" location="" type="website" href="https://jupyter.org" -->
installation if you prefer. That means that you may test and verify the
procedure or alter parameters and try solving the riddles with your own
parameters.
<!-- endnote -->

Your can download independent Jupyter notebooks for
[processing corpora](https://git.io/vASwM)<!-- cite author="Marko Manninen" title="Processing corpora" date="2018" location="" type="website" href="https://git.io/vASwM" -->,
[solving riddles](https://git.io/vASrY)<!-- cite author="Marko Manninen" title="Solving riddles" date="2018" location="" type="website" href="https://git.io/vASrY" -->, and
[analysing results](https://git.io/vASrY)<!-- cite author="Marko Manninen" title="Analysing results" date="2018" location="" type="website" href="https://git.io/vASrY" -->.

You may also run the code of this book directly from Python shell<!-- cite author="python.org" title="Python shell" date="" location="" type="website" href="https://www.python.org/shell/" -->,
no problem. All you need is basicly the `functions.py` script on the directory
you are launching Python shell or running the Jupyter Notebook document.

{% include 'footnotes.md' %}
