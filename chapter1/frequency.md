## Word frequency

So, I already know that there are words repeating very often, for different
reasons. But then there are words repeating only once or few times. Thus it is
relevant to ask, how many percent of the whole word base, the least repeated
words actually take? For the task I'm using `groupby` and `count` methods of
`Dataframe` object in `Pandas` library.

```python
# group words by occurrence and count grouped items, list the first five items
for x, y in df.groupby([1, 2]).count()[:10].T.items():
    # occurrence y[0] is compared to the the number of all words i.e. lwords3
    print("words repeating %s time(s): " % x[0], round(100*y[0]/lwords3, 2), "%")
```

Output:

```
word(s) repeating 1 time(s):  1.13 %
word(s) repeating 2 time(s):  0.4 %
word(s) repeating 3 time(s):  0.19 %
word(s) repeating 4 time(s):  0.12 %
word(s) repeating 5 time(s):  0.08 %
```

1.13% the words in database occurs only once in a corpora. The words that 
repeat 1-4 times fills roughly 2% of the whole corpora.

{% include 'footnotes.md' %}
