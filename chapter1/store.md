## Store database

This is the single most important part of the chapter one. I'm saving all
parsed unique words in the CSV file that can be used as a database for the
riddle solver. After this you may proceed to the [CHAPTER II](#chapter-ii) or
the [riddle solver](https://git.io/vASrY)<!-- cite author="Marko Manninen" title="Solving riddles" date="2018" location="" type="website" href="https://git.io/vASrY" --> Jupyter notebook
document in interactive mode, if you prefer skipping optional inspections of
the database.

```python
# import csv file name variable
from functions import csv_file_name
# save data to CSV file without header row, and index column in utf8 format
df.to_csv(csv_file_name, header=False, index=False, encoding='utf-8')
```

Noteworth is that stored words are not stems nor any base forms of the
words but contain words in all possible inflected forms. Due to nature
of machine processed texts, one should also be warned about corrupted
words and other noise to occur in results. Programming tools are good
for extracting interesting content and filtering data that would be
impossible for a human to do because of its enormous size. But results
still need verification and interpretation.

The rest of the chapter is to investigate any interesting facts from the
processed corpora as well as detecting possible flaws in the procedure.

{% include 'footnotes.md' %}
