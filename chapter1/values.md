## Biggest isopsephical value

So, which words have the biggest isopsephical value in the database? We
can find it out by sorting words database by the fourth column, that is
the isopsephical value of the word.

```python
# sort by the isopsephy column and get the first 20 items
m = df.sort_values(4, ascending=False).head(n=20)
# select columns by indices
m = m[[0, 1, 4]]
# relabel selected columns
m.columns = ['Word', 'Count', 'Isopsephy']
# remove the index column and output table
HTML(m.to_html(index=False))
```

| Word                                         | Count | Isopsephy |
|----------------------------------------------|:-----:|:---------:|
| ΛΕΟΝΤΑΤΥΦΛΩΣΩΝΣΚΩΛΩΨΔΕΤΟΥ                    | 1     | 6865      |
| ΟΡΘΡΟΦΟΙΤΟΣΥΚΟΦΑΝΤΟΔΙΚΟΤΑΛΑΙΠΩΡΩΝ            | 1     | 5186      |
| ΒΡΥΣΩΝΟΘΡΑΣΥΜΑΧΕΙΟΛΗΨΙΚΕΡΜΑΤΩΝ               | 2     | 5122      |
| ΟΡΘΟΦΟΙΤΟΣΥΚΟΦΑΝΤΟΔΙΚΟΤΑΛΑΙΠΩΡΩΝ             | 2     | 5086      |
| ΓΛΩΣΣΟΤΟΜΗΘΕΝΤΩΝΧΡΙΣΤΙΑΝΩΝ                   | 1     | 5056      |
| ΚΑΙΤΟΝΑΡΙΣΤΑΡΧΟΝΑΣΜΕΝΩΣΤΗΝΓΡΑΦΗΝΤΟΥ          | 1     | 4969      |
| ΑΡΣΕΝΙΚΩΝΟΝΟΜΑΤΩΝΣΤΟΙΧΕΙΑΕΣΤΙΠΕΝΤΕ           | 1     | 4768      |
| ΛΛΗΣΤΗΣΑΝΩΘΕΝΘΕΡΜΟΤΗΤΟΣΑΤΜΙΔΟΥΜΕΝΟΝΦΕΡΕΤΑΙ   | 1     | 4754      |
| ΕΠΙΣΚΟΠΩΚΩΝΣΤΑΝΤΙΝΟΥΠΟΛΕΩΣ                   | 1     | 4701      |
| ΚΩΔΩΝΟΦΑΛΑΡΑΧΡΩΜΕΝΟΥΣ                        | 1     | 4642      |
| ΕΜΟΥΟΙΑΠΕΦΕΥΓΑΧΕΙΡΑΣΛΥΠΗΣΑΣΜΕΝΟΥΔΕΝΑΟΥΔΕΝ    | 1     | 4579      |
| ΔΥΝΑΤΟΝΔΕΤΟΑΙΤΙΑΙΗΣΓΕΝΕΣΕΩΣΚΑΙΤΗΣΦΘΟΡΑΣ      | 1     | 4481      |
| ΤΩΟΡΘΩΕΚΑΣΤΑΘΕΩΡΩΝ                           | 1     | 4370      |
| ΣΥΝΥΠΟΧΩΡΟΥΝΤΩΝ                              | 1     | 4370      |
| ΟΠΡΩΤΟΣΑΝΘΡΩΠΩΝΥΠΟΔΕΙΞΑΣ                     | 1     | 4340      |
| ΟΥΝΙΚΑΝΩΣΠΕΡΙΑΥΤΩΝΗΜΙΝΕΝΤΟΙΣΠΕΡΙ             | 1     | 4285      |
| ΩΡΙΣΜΕΝΩΝΠΡΟΣΩΠΩΝ                            | 1     | 4235      |
| ΑΡΙΣΤΑΡΧΟΣΚΑΙΟΙΑΠΟΤΗΣΣΧΟΛΗΣΦΑΣΙΝ             | 1     | 4221      |
| ΤΟΥΤΟΥΣΛΕΓΟΝΤΕΣΩΣΠΡΟΣΤΗΝ                     | 1     | 4211      |
| ΨΥΧΟΓΟΝΙΜΩΤΑΤΩΝ                              | 1     | 4194      |

These are very rare words, as was the case with the longest words too. It can be
seen that the longest words and the biggest isopsephical words are just partly
overlapping. Isopsephical value of the word does not depend on the length of
the word, but it is depending on the fact, how many times the latter part of the
letters in the alphabet occus in the word, because they have the biggest value.
In the word `ΛΕΟΝΤΑΤΥΦΛΩΣΩΝΣΚΩΛΩΨΔΕΤΟΥ` letters Τ, Φ, Ω, and Σ are repeated several
times so that the sum of the alphabetic numerals in the word, i.e. the isopsephical
value, adds up to 6865. The value gap between the first and the second word is rather
big, 1679 and after that the gap is between one and two hundred and decreasing.
Results like these are interesting because they may tell about the deliberate
construction of the words, which statistician wants to detect from the vast sample
of coincidental hits.

Before going to the last useful procedure of spotting the exact location of the words
in the corpora, lets see a special statictic about the frequency of the words.

{% include 'footnotes.md' %}
