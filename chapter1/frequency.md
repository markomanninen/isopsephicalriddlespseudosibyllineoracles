## Word frequency

So, I already know that there are certain words repeating very often,
for different reasons. But then there are words repeating once or few
times only. Thus, it is relevant to ask, how many percent of the whole
word base, the least repeated words actually take? For the task I'm
using groupby and count methods of the `Dataframe` object in Pandas.

```python
# length of the words database. taken to a variable to prevent unnecessary
# repetition in the next for loop
le = len(df)
# group words by occurrence and count grouped items, list the first 10 items
for x, y in df.groupby([1, 2]).count()[:10].T.items():
    print("words repeating %s time(s): " % x[0], round(100*y[0]/le, 2), "%")
```

Output:

```
words repeating 1 time(s):  44.95 %
words repeating 2 time(s):  15.86 %
words repeating 3 time(s):  7.48 %
words repeating 4 time(s):  4.84 %
words repeating 5 time(s):  3.32 %
words repeating 6 time(s):  2.5 %
words repeating 7 time(s):  1.92 %
words repeating 8 time(s):  1.59 %
words repeating 9 time(s):  1.28 %
words repeating 10 time(s):  1.11 %
```

Almost 45% of the wodrds in database occurs only once in a corpora. That
looks pretty high number which reason I have yet to resolved. Words that
repeat 1-4 times fills roughly 70% of the whole corpora.

{% include 'footnotes.md' %}
