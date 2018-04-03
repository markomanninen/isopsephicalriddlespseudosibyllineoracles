## Collecting and processing files

When the files have been downloaded and copied, it is time to read them to the
RAM (Random-Access Memory). At this point file paths are collected to the
`greek_corpora_x` variable that is used on later iterators.

```python
# import final extraction directory names and init function
from functions import init_corpora, perseus_dir, first1k_dir
# collect files and initialize data dictionary
greek_corpora_x = init_corpora([[perseus_tmp_dir, perseus_dir], [first1k_tmp_dir, first1k_dir]])
print(len(greek_corpora_x), "files found")
```

Output:

```txt
1705 files found
```

Actual files found may differ by increasing over time, because Greek corpora
repositories are constantly maintained and new texts are added by voluteer
contributors.

__Processing files__

Next step is to extract Greek content from the downloaded and selected XML
source files. Usually this task might take a lot of effort in NLP (Natural
Language Processing). Python NLTK<!-- cite author="nltk.org" title="NLTK - Natural Language ToolKit" date="" location="" type="website" href="https://www.nltk.org/" -->
and CLTK<!-- cite author="cltk.org" title="CLTK - The Classical Language ToolKit" date="" location="" type="website" href="https://github.com/cltk/cltk" --> libraries would be useful
at this point, but in my case I'm only interested of Greek words, that is, text
content encoded by a certain Greek Unicode letter block<!-- cite author="wikipedia.org" title="Greek in Unicode" date="" location="" type="website" href="https://en.wikipedia.org/wiki/Greek_alphabet#Greek_in_Unicode" -->. Thus,
I'm able to simplify this part by removing all other characters from source
files except Greek characters. Again, details can be found from the
`functions.py` script.

Extracted content is saved to the `corpora/author/work` based directories.
Simplified uncial conversion is also made at the same time so that the final
data contain only plain uppercase words separated by spaces. Pretty much in a
format written by the ancient Greeks, except that Greeks didn't even use spaces
to denote individual words and phrases. See the example of Ancient Greek text
written on papyrus:

![Papyrus 47, Uncial Greek text without spaces. Rev. 13:17-](/media/P47.png){caption=1}

Next code execution will take several minutes depending on if you have already
run it once and have the previous temporary directories available. The old
processed corpora files are removed first, then they are recreated by calling
`process_greek_corpora` function.

```python
# import helper functions and extract file names
from functions import remove, all_greek_text_file, perseus_greek_text_file, \
                      first1k_greek_text_file, process_greek_corpora
# remove old processed temporary files
try:
    remove(all_greek_text_file)
    remove(perseus_greek_text_file)
    remove(first1k_greek_text_file)
except OSError:
    pass
# process and get greek corpora data to the RAM
greek_corpora = process_greek_corpora(greek_corpora_x)
```

{% include 'footnotes.md' %}
