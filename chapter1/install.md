## Required components and installation

The first sub task is to get a big raw ancient Greek text to operate with. I
have implemented an importer interface with Taqadum (tqdm)<!-- cite author="tqdm" title="Taqadum progress bar" date="" location="" type="website" href="https://github.com/tqdm/tqdm" -->
library to the `Perseus`<!-- cite author="perseus.tufts.edu" title="Perseus digital library" date="" location="" type="website" href="http://www.perseus.tufts.edu/hopper/opensource/download" -->
and the `OpenGreekAndLatin`<!-- cite author="OpenGreekAndLatin" title="First 1000 Years of Greek" date="" location="" type="website" href="http://opengreekandlatin.github.io/First1KGreek" -->
 (shortly `First1K`) open source data sources in this chapter.

I'm using my own [Abnum](https://github.com/markomanninen/abnum3)<!-- cite author="Marko Manninen" title="Abnum" date="" location="" type="website" href="https://github.com/markomanninen/abnum3" -->
library to remove accents from the Greek words, remove non-alphabetical
characters from the corpora, as well as calculating the isopsephical
value of the Greek words. Greek accentuation<!-- cite author="jtauber" title="Greek accentuation" date="" location="" type="website" href="https://github.com/jtauber/greek-accentuation" -->
library is used to split words into syllables. This is required because the
riddles of my closest interest contain specific information about the syllables
of the words. Pandas<!-- cite author="pandas.pydata.org" title="Pandas - Python Data Analysis Library" date="" location="" type="website" href="http://pandas.pydata.org/" -->
library is used as an API (Application Programming Interface) to the collected
database. Plotly<!-- cite author="plot.ly" title="Plotly data visualization" date="" location="" type="website" href="https://plot.ly/" --> library and online infographic
service are used for the visual presentation of the statistics.

__Installation__

You can install these libraries by uncommenting and running the next install
line in the Jupyter notebook:

```python
import sys
#!{sys.executable} -m pip install tqdm abnum pandas plotly greek_accentuation
```

For the sake of convenience, I'm printing out my environment:

```python
# access system info via imported sys module
print("Python %s" % sys.version)
```

Output:

```
Python 3.6.1 | Anaconda 4.4.0 (64-bit) | (default, May 11 2017, 13:25:24)
[MSC v.1900 64 bit (AMD64)]
```

Note that Python 3.4+ is required for all examples to work properly. To find out
other ways of installing `PyPI` maintained libraries, please consult:
https://packaging.python.org/tutorials/installing-packages/

{% include 'footnotes.md' %}
