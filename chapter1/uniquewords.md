## Unique words database

Now it is time to collect unique Greek words to the database and show certain
specialties of the word statistics. I'm reusing data from the `greek_corpora`
variable that is in the memory already rather than recollecting words from the
files. `syllabify` function and `Abnum` object are utilized to retrieve
additional necessary information about the words.

Running the next code will take a minute or two depending on the processor
speed of your computer:

```python
from functions import syllabify, Abnum, greek, vowels
# initialize greek Abnum object for calculating isopsephical value of the words
g = Abnum(greek)
# count unique words statistic from the parsed greek corpora
# rather than the plain text file. it would be pretty hefty work to find
# out occurence of the all over 800000 unique words from the text file that
# is hundreds of megabytes big!
unique_word_stats = {}
for item in greek_corpora:
    for word, cnt in item['uwords'].items():
        if word not in unique_word_stats:
            unique_word_stats[word] = 0
        unique_word_stats[word] += cnt
# init dataframe
df = DataFrame([[k, v] for k, v in unique_word_stats.items()])
# add column for the occurrence percentage of the word
# lwords3 variable is the length of the all words list
df[2] = df[1].apply(lambda x: round(x*100/lwords3, 2))
# add column for the length of the individual word
df[3] = df[0].apply(lambda x: len(x))
# add isopsephical value column
df[4] = df[0].apply(lambda x: g.value(x))
# add syllabified word column
df[5] = df[0].apply(lambda x: syllabify(x))
# add length of the syllables in the word as a column
df[6] = df[5].apply(lambda x: len(x))
# count vowels in the word as a column
df[7] = df[0].apply(lambda x: sum(list(x.count(c) for c in vowels)))
# count consonants in the word as a column
df[8] = df[0].apply(lambda x: len(x)-sum(list(x.count(c) for c in vowels)))
```

{% include 'footnotes.md' %}
