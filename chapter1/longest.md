## Longest words

For a curiosity, let's also see the longest words in the database:

```python
from functions import HTML
# load result to the temporary variable for later usage
# sort by length, limit to 20 items
l = df.sort_values(3, ascending=False).head(n=20)
# take column index 0, 1, and 3. this is the second way of selecting
# certain columns. see iloc method in the previous example
l = l[[0, 1, 3]]
# label columns
l.columns = ['Word', 'Count', 'Length']
# output table without the index column
HTML(l.to_html(index=False))
```

| Word                                          | Count | Length |
|-----------------------------------------------|:-----:|:------:|
| ΠΑΡΕΓΕΝΟΜΕΝΟΜΕΝΟΣΗΝΚΑΙΕΤΙΕΚΤΗΣΛΕΣΒΟΥΟΥΦΑΜΕΝ | 1   | 43   |
| ΛΛΗΣΤΗΣΑΝΩΘΕΝΘΕΡΜΟΤΗΤΟΣΑΤΜΙΔΟΥΜΕΝΟΝΦΕΡΕΤΑΙ  | 1   | 42   |
| ΕΜΟΥΟΙΑΠΕΦΕΥΓΑΧΕΙΡΑΣΛΥΠΗΣΑΣΜΕΝΟΥΔΕΝΑΟΥΔΕΝ   | 1   | 41   |
| ΠΥΡΟΒΡΟΜΟΛΕΥΚΕΡΕΒΙΝΘΟΑΚΑΝΘΙΔΟΜΙΚΡΙΤΡΙΑΔΥ    | 1   | 40   |
| ΔΥΝΑΤΟΝΔΕΤΟΑΙΤΙΑΙΗΣΓΕΝΕΣΕΩΣΚΑΙΤΗΣΦΘΟΡΑΣ     | 1   | 39   |
| ΠΥΡΒΡΟΜΟΛΕΥΚΕΡΕΒΙΝΘΟΑΚΑΝΘΟΥΜΙΚΤΡΙΤΥΑΔΥ      | 1   | 38   |
| ΚΑΙΙΚΕΛΗΧΡΥΣΗΑΦΡΟΔΙΤΗΚΑΙΟΙΣΕΚΟΣΜΗΣΕ         | 1   | 35   |
| ΚΑΙΤΟΝΑΡΙΣΤΑΡΧΟΝΑΣΜΕΝΩΣΤΗΝΓΡΑΦΗΝΤΟΥ         | 1   | 35   |
| ΕΝΝΕΑΚΑΙΕΙΚΟΣΙΚΑΙΕΠΤΑΚΟΣΙΟΠΛΑΣΙΑΚΙΣ         | 1   | 35   |
| ΑΡΣΕΝΙΚΩΝΟΝΟΜΑΤΩΝΣΤΟΙΧΕΙΑΕΣΤΙΠΕΝΤΕ          | 1   | 34   |
| ΟΤΙΤΟΥΜΗΔΙΑΠΡΟΤΕΡΩΝΟΡΙΖΕΣΘΑΙΤΡΕΙΣ           | 1   | 33   |
| ΟΡΘΡΟΦΟΙΤΟΣΥΚΟΦΑΝΤΟΔΙΚΟΤΑΛΑΙΠΩΡΩΝ           | 1   | 33   |
| ΟΡΘΟΦΟΙΤΟΣΥΚΟΦΑΝΤΟΔΙΚΟΤΑΛΑΙΠΩΡΩΝ            | 2   | 32   |
| ΟΥΝΙΚΑΝΩΣΠΕΡΙΑΥΤΩΝΗΜΙΝΕΝΤΟΙΣΠΕΡΙ            | 1   | 32   |
| ΗΔΙΚΗΜΕΝΟΝΔΕΑΠΕΡΡΙΜΜΕΝΟΝΠΕΡΙΟΡΑΣ            | 1   | 32   |
| ΑΡΙΣΤΑΡΧΟΣΚΑΙΟΙΑΠΟΤΗΣΣΧΟΛΗΣΦΑΣΙΝ            | 1   | 32   |
| ΤΕΤΤΑΡΑΚΟΝΤΑΚΑΙΠΕΝΤΑΚΙΣΧΙΛΙΟΣΤΟΝ            | 1   | 32   |
| ΑΥΤΟΜΑΤΟΙΔΕΟΙΘΕΟΙΑΠΑΛΛΑΣΣΟΜΕΝΟΙ             | 1   | 31   |
| ΣΠΕΡΜΑΓΟΡΑΙΟΛΕΚΙΘΟΛΑΧΑΝΟΠΩΛΙΔΕΣ             | 3   | 31   |
| ΚΑΝΤΩΝΕΠΙΤΑΙΣΔΥΝΑΜΕΣΙΠΑΡΑΒΑΙΝΗ              | 1   | 30   |

A bit later I'm searching exact place of these words from the corpora,
but lets first find out, what words have the biggest isopsephical value.

{% include 'footnotes.md' %}
