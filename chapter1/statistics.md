## Statistics

After the files have been downloaded and preprocessed, I'm going to output the
size of them with the help of the `get_file_size` function:

```python
from functions import get_file_size

print("Size of the all raw text: %s MB" % get_file_size(all_greek_text_file))
print("Size of the perseus raw text: %s MB" % get_file_size(perseus_greek_text_file))
print("Size of the first1k raw text: %s MB" % get_file_size(first1k_greek_text_file))
```

Output:

```
Size of the all raw text: 347.76 MB
Size of the perseus raw text: 107.41 MB
Size of the first1k raw text: 240.35 MB
```

Size may differ depending on the latest size of the downloaded and processed
corpora. Then, I will calculate other statistics of the saved text files to
compare their content. By passing text file name, e.g. `perseus_greek_text_file`
to the `get_stats` function, statistical variables are returned and at the same
time their values are printed:

```python
from functions import get_stats
ccontent1, chars1, lwords1 = get_stats(perseus_greek_text_file)
ccontent2, chars2, lwords2 = get_stats(first1k_greek_text_file)
ccontent3, chars3, lwords3 = get_stats(all_greek_text_file)
```

Output:

```
Corpora: perseus_greek_text_files.txt
Letters: 51411752
Words in total: 9900720
Unique words: 423428

Corpora: first1k_greek_text_files.txt
Letters: 113763150
Words in total: 23084445
Unique words: 667503

Corpora: all_greek_text_files.txt
Letters: 165174902
Words in total: 32985165
Unique words: 831308
```

{% include 'footnotes.md' %}
