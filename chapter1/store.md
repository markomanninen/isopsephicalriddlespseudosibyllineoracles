## Store database

This is the single most important part of the chapter one. I'm saving all
simplified unique words as a CSV file that can be used as a database for the
riddle solver. After this you may proceed to the [CHAPTER II](#chapter-ii) or
the [riddle solver](https://git.io/vASrY) Jupyter notebook document in
interactive mode, if you prefer skipping optional inspection of the database.

```python
from functions import csv_file_name
# save dataframe to CSV file
df.to_csv(csv_file_name, header=False, index=False, encoding='utf-8')
```

Noteworth is that stored words are not stems or any base forms of the
words but contain words in all possible inflected forms. Due to nature
of machine processed texts, one should also be warned about corrupted
words and other noise to occur in results. Programming tools are good
for extracting interesting content and filtering data that would be
impossible for a human to do because of its enormous size. But results
still need verification and interpretation. Also, procedures can be fine
tuned and developed in many ways.

{% include 'footnotes.md' %}
