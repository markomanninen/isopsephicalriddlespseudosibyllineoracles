## Most repeated words

For a confirmation of the succesful task, I will show the total number
of the unique words, and five of the most repeated words in the
database:

```python
# import display html helper function
from functions import display_html
# sort and limit words, select columns by index 1, 2, and 3
words = df.sort_values(1, ascending=False).head(n=5).iloc[:,0:3]
# label columns
words.columns = ['Word', 'Count', 'Percent']
# output total number of the words from df object
print("Total records: %s" % len(df))
# index=False to hide index column and output table by using to_html method
display_html(words.to_html(index=False), raw=True)
```

Total records: 833817

| Word | Count   | Percent |
|:----:|:-------:|:-------:|
| ΚΑΙ  | 1781528 | 5.38    |
| ΔΕ   | 778589  | 2.35    |
| ΤΟ   | 670952  | 2.03    |
| ΤΩΝ  | 487015  | 1.47    |
| Η    | 483372  | 1.46    |

`KAI`, the word denoting
[and-conjuction](http://www.perseus.tufts.edu/hopper/text?doc=Perseus:text:1999.04.0057:entry=kai/1)[^20],
is well known as the most repeated word in the Ancient Greek. Above
statistics says that `KAI` word takes almost 5.4% of the all words.

This can be explained easily because KAI serves for many fundamental
functions in text, such as an indicator of a new chapter or a paragraph,
list copulative of two or more items, etc., basicly in a place, where we
would use punctuation nowadays. From the other words, Η stands for a
paraphrase and ΔΕ for a disconjunction. All these three words
characterises Ancient Greek as fundamentally based on logical
constructors, one could argue. Maybe even early type of list processing
structures have been developed in a form of natural language. It would
be an interesting excurse to compare the propositional logic and the
list processing features of the Ancient Greek rhetorics to the modern
LISP language or similar programming paradigm, but that is definitely
beyond the scope of the investigation of this study.

Naturally, articles and particles (`ΤΟ`, `ΤΩΝ`) belong to the most repeated
words as well. One could use the knowledge of the certain word rate as
one of the indicators of the text genre, or even quess the author of the
text.

{% include 'footnotes.md' %}
