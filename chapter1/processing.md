## Natural language processing

Programmatical approach to solve the riddles requires huge Greek text corpora.
Bigger it is, the better. I will download and preprocess available open source
Greek corpora, which is a quite daunting task for many reasons. Programming
language of my choice is Python<!-- cite author="python.org" title="Python" date="" location="" type="website" href="http://python.org" --> for it has plenty of good and stable open source
libraries required for my work. Python is widely recognized in academic and
scientific field and well oriented to the research projects.

I have left the most of the overly technical details of these chapters
for the enthusiasts to read straight from the commented code in
[functions.py](https://git.io/vAS2Z)<!-- cite author="Marko Manninen" title="functions.py" date="2018" location="" type="website" href="https://git.io/vAS2Z" --> script. By collecting the large
part of the used procedures to the separate script maintains this
document more concise too.

In the end of the task of the first chapter, I'll have a word database
containing hundreds of thousands of unique Greek words extracted from
the naturally written language corpora. Then words can be further used
in the riddle solver in the second chapter.

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

You may also run code directly from Python shell<!-- cite author="python.org" title="Python shell" date="" location="" type="website" href="https://www.python.org/shell/" -->
environment, no problem.

### Required components

The first sub task is to get a big raw ancient Greek text to operate
with. I have implemented an importer interface with
[tqdm](https://github.com/tqdm/tqdm) library to the
[Perseus](http://www.perseus.tufts.edu/hopper/opensource/download)[^11]
and the
[First1KGreek](http://opengreekandlatin.github.io/First1KGreek/)[^12]
open source data sources in this chapter.

I'm using my own [Abnum](https://github.com/markomanninen/abnum3)[^13]
library to remove accents from the Greek words, remove non-alphabetical
characters from the corpora, as well as calculating the isopsephical
value of the Greek words. [Greek
accentuation](https://github.com/jtauber/greek-accentuation)[^14]
library is used to split words into syllables. This is required because
the riddles of my closest interest contain specific information about
the syllables of the words. [Pandas](http://pandas.pydata.org/)[^15]
library is used as an API (application programming interface) to the
collected database. [Plotly](https://plot.ly/)[^16] library and online
infographic service are used for the visual presentation of the
statistics.

You can install these libraries by uncommenting and running the next
install lines in the Jupyter notebook:

```
import sys

#!{sys.executable} -m pip install tqdm abnum
#!{sys.executable} -m pip install pandas plotly
#!{sys.executable} -m pip install greek_accentuation
```

For your convenience, my environment is the following:

```
print("Python %s" % sys.version)
```

Output:

```
Python 3.6.1 | Anaconda 4.4.0 (64-bit) | (default, May 11 2017, 13:25:24)
[MSC v.1900 64 bit (AMD64)]
```

Note that Python 3.4+ is required for all examples to work properly. To
find out other ways of installing PyPI maintained libraries, please
consult: <https://packaging.python.org/tutorials/installing-packages/>

### Downloading corpora

I'm going to use Perseus and OpenGreekAndLatin corpora for the study by
combining them into a single raw text file and unique words database.

The next code snippets will download hundreds of megabytes of Greek text
to a local computer for quicker access. tqdm downloader requires a
stable internet connection to work properly.

One could also download source zip files via browser and place them to
the same directory with the Jupyter notebook or where Python is
optionally run in shell mode. Zip files must then be renamed as
perseus.zip and first1k.zip.

1.  Download packed zip files from their GitHub repositories:

``` {.sourceCode .python}
from functions import download_with_indicator, perseus_zip_file, first1k_zip_file
# download from perseus file source
fs = "https://github.com/PerseusDL/canonical-greekLit/archive/master.zip"
download_with_indicator(fs, perseus_zip_file)
# download from first1k file source
fs = "https://github.com/OpenGreekAndLatin/First1KGreek/archive/master.zip"
download_with_indicator(fs, first1k_zip_file)
```

Output:

``` {.sourceCode .txt}
Downloading: https://github.com/PerseusDL/canonical-greekLit/archive/master.zip
71.00MB [04:15, 211.08KB/s]
Downloading: https://github.com/OpenGreekAndLatin/First1KGreek/archive/master.zip
195.00MB [09:15, 201.54KB/s]
```

2.  Unzip files to the corresponding directories:

``` {.sourceCode .python}
from functions import perseus_zip_dir, first1k_zip_dir, unzip
# first argument is the zip source, second is the destination directory
unzip(perseus_zip_file, perseus_zip_dir)
unzip(first1k_zip_file, first1k_zip_dir)
```

3\. Copy only suitable Greek text xml files from perseus\_zip\_dir and
first1k\_zip\_dir to the temporary work directories. Original
repositories contain a lot of unnecessary files for the riddle solver
which are skipped in this process.

``` {.sourceCode .python}
from functions import copy_corpora, joinpaths, perseus_tmp_dir, first1k_tmp_dir
# important Greek text files resides in the data directory of the repositories
for item in [[joinpaths(perseus_zip_dir,
              ["canonical-greekLit-master", "data"]), perseus_tmp_dir],
             [joinpaths(first1k_zip_dir,
              ["First1KGreek-master", "data"]), first1k_tmp_dir]]:
    copy_corpora(*item)
```

Output:

``` {.sourceCode .txt}
greek_text_perseus_tmp already exists. Either remove it and run again, or
just use the old one.

Copying greek_text_first1k_tmp -> greek_text_first1k
```

Depending on if the files have been downloaded already, the output may
differ.

### Collecting files

When the files has been downloaded and copied, it is time to read them
to the RAM (Random-Access Memory). At this point file paths are
collected to the greek\_corpora\_x variable that is used on later
iterators.

``` {.sourceCode .python}
from functions import init_corpora, perseus_dir, first1k_dir
# collect files and initialize data dictionary
greek_corpora_x = init_corpora([[perseus_tmp_dir, perseus_dir], [first1k_tmp_dir, first1k_dir]])
print(len(greek_corpora_x), "files found")
```

Output:

``` {.sourceCode .text}
1705 files found
```

Actual files found may differ by increasing over time, because Greek
corpora repositories are constantly maintained and new texts are added
by voluteer contributors.

### Processing files

Next step is to extract Greek content from the downloaded and selected
XML source files. Usually this task might take a lot of effort in NLP
(natural language processing). Python [NLTK](https://www.nltk.org/)[^17]
and [CLTK](https://github.com/cltk/cltk)[^18] libraries would be useful
at this point, but in my case I'm only interested of Greek words, that
is, text content encoded by a certain [Greek Unicode
letter](https://en.wikipedia.org/wiki/Greek_alphabet#Greek_in_Unicode)[^19]
block. Thus, I'm able to simplify this part by removing all other
characters from source files except Greek characters. Again, details can
be found from the [functions.py](https://git.io/vAS2Z) script.

Extracted content is saved to the corpora/author/work based directories.
Simplified uncial conversion is also made at the same time so that the
final data contain only plain uppercase words separated by spaces.
Pretty much in a format written by the ancient Greeks, except they
didn't even use spaces to denote individual words and phrases.

![Papyrus 47, Uncial Greek text without spaces. Rev
13:17-](P47.png){.align-center}

Next code execution will take several minutes depending on if you have
already run it once and have the previous temporary directories
available. Old processed corpora files are removed first, then they are
recreated by calling process\_greek\_corpora function.

``` {.sourceCode .python}
from functions import remove, all_greek_text_file, perseus_greek_text_file,\
                      first1k_greek_text_file, process_greek_corpora
# remove old processed temporary files
try:
    remove(all_greek_text_file)
    remove(perseus_greek_text_file)
    remove(first1k_greek_text_file)
except OSError:
    pass
# process and get greek corpora data to the RAM memory
greek_corpora = process_greek_corpora(greek_corpora_x)
```

{% include 'footnotes.md' %}
