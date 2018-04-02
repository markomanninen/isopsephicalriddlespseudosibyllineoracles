## Detect source texts

Statistics is nice, but it wouldn't be so useful, if there was no routine to find
out words from the corpora, where they actually occur.

The last part of the chapter one is to demonstrate the procedure how to find out
the exact places of the given words in the corpora. This is going to be useful on
the next chapters. I have provided the `search_words_from_corpora` function to
simplify this task. Again, the actual function code can be found from the
`functions.py` script.

__Longest words__

On the search result, the author and the text file is listed following with the
search term and how many hits there was on the text. Finally, a small excerpt is
fetched from the text around the search term. Excerpt has all the original
diacritics and letter case intact. The next step would be to search original
word from Google which will the most probably tell enought about the word and
the context. Even the reader uncabable to Greek can find out the meaning of the
word with a pretty small effort.

```python
from functions import search_words_from_corpora
# collect the plain text words from the already instantiated l variable
# l variable is a dataframe and the transpose (T) of it is used here
words = list(y[0] for x, y in l.T.items())
# pass words and directories in a list to search words from
# the third parameter specifies how many occurrences of the word is
# listed per author text in maximum
search_words_from_corpora(words, [perseus_dir, first1k_dir], 3)
```

Output:

```
+ Aristophanes, Lysistrata (tlg0019.tlg007.perseus-grc2.xml) =>

----- ΣΠΕΡΜΑΓΟΡΑΙΟΛΕΚΙΘΟΛΑΧΑΝΟΠΩΛΙΔΕΣ (1) -----
ὦ ξύμμαχοι γυναῖκες ἐκθεῖτ ἔνδοθεν ὦ σπερμαγοραιολεκιθολαχανοπώλιδες ὦ σκοροδοπανδοκευτριαρτοπώλιδες

+ Aristophanes, Wasps (tlg0019.tlg004.perseus-grc1.xml) =>

----- ΟΡΘΡΟΦΟΙΤΟΣΥΚΟΦΑΝΤΟΔΙΚΟΤΑΛΑΙΠΩΡΩΝ (1) -----
ς ἀκούειν ἡδἔ εἰ καὶ νῦν ἐγὼ τὸν πατέρ ὅτι βούλομαι τούτων ἀπαλλαχθέντα τῶν ὀρθροφοιτοσυκοφαντοδικοταλαιπώρων τρόπων ζῆν βίον γενναῖον ὥσπερ Μόρυχος αἰτίαν ἔχω ταῦτα δρᾶν ξυνωμότης ὢν καὶ φρονῶν

+ Athenaeus, Deipnosophistae (tlg0008.tlg001.perseus-grc3.xml) =>

----- ΠΥΡΒΡΟΜΟΛΕΥΚΕΡΕΒΙΝΘΟΑΚΑΝΘΟΥΜΙΚΤΡΙΤΥΑΔΥ (1) -----
τις ἃ Ζανὸς καλέοντι τρώγματ ἔπειτ ἐπένειμεν ἐνκατακνακομιγὲς πεφρυγμένον πυρβρομολευκερεβινθοακανθουμικτριτυαδυ βρῶμα τοπανταναμικτον ἀμπυκικηροιδηστίχας παρεγίνετο τούτοις

+ Athenaeus, TheDeipnosophists (tlg0008.tlg001.perseus-grc4.xml) =>

----- ΠΥΡΟΒΡΟΜΟΛΕΥΚΕΡΕΒΙΝΘΟΑΚΑΝΘΙΔΟΜΙΚΡΙΤΡΙΑΔΥ (1) -----
ἐπεί γ ἐπένειμεν ἐγκατακνακομιγὲς πεφρυγμένον πυροβρομολευκερεβινθοακανθιδομικριτριαδυ βρωματοπαντανάμικτον ἄμπυκι καριδίᾳ στιχὰς παρεγίνετο τούτοις σταιτινοκογχομαγὴς

+ Plato, Laws (tlg0059.tlg034.perseus-grc2.xml) =>

----- ΤΕΤΤΑΡΑΚΟΝΤΑΚΑΙΠΕΝΤΑΚΙΣΧΙΛΙΟΣΤΟΝ (1) -----
πεφευγότος ἀμφοτέρωθεν πρός τε ἀνδρῶν καὶ πρὸς γυναικῶν κληρονόμον εἰς τὸν οἶκον τοῦτον τῇ πόλει τετταρακοντακαιπεντακισχιλιοστὸν καταστῆσαι βουλευομένους μετὰ νομοφυλάκων καὶ ἱερέων διανοηθέντας τρόπῳ καὶ λόγῳ τοιῷδε ὡς οὐδεὶς

+ Plato, Republic (tlg0059.tlg030.perseus-grc2.xml) =>

----- ΕΝΝΕΑΚΑΙΕΙΚΟΣΙΚΑΙΕΠΤΑΚΟΣΙΟΠΛΑΣΙΑΚΙΣ (1) -----
τοῦ τυράννου ἀφεστηκότα λέγῃ ὅσον ἀφέστηκεν ἐννεακαιεικοσικαιεπτακοσιοπλασιάκις ἥδιον αὐτὸν ζῶντα εὑρήσει τελειωθείσῃ τῇ πολλαπλασιώσει τὸν δὲ τύραννον ἀνιαρότερον τῇ αὐτῇ ταύτῃ

+ AlexanderOfAphrodisias, InAristotelisMetaphysicaCommentaria (tlg0732.tlg004.opp-grc1.xml) =>

----- ΟΥΝΙΚΑΝΩΣΠΕΡΙΑΥΤΩΝΗΜΙΝΕΝΤΟΙΣΠΕΡΙ (1) -----
οιησά αενο τ ιστεύσομεν ρ Φ τεθεώρηται μὲν οὐνὶκανῶςπερὶαὐτῶνἡμῖνἐντοῖςπερὶ φύσεως ἰκαὶἱκανῶς φησί περὶτῶ ν ἀρχῶν τῶν φυσικῶν ἐν τοῖς περὶ φύσεως
```

Aristophanes<!-- cite author="wikipedia.org" title="Aristophanes" date="" location="" type="website" href="https://en.wikipedia.org/wiki/Aristophanes" --> was a Greek
comic playwright and a word expert of a sort which explains many of the long
words occuring in his texts. Also, mathematical texts are filled with long
compound words for fractions, thus many of the longer words appear in
mathematical source books. Note that here we actually do rely on the word
tokening made by other human editors. Original text might not have separated
words with spaces as usually Greek text was continuous stream of alphabets
without any punctuation and spaces. Only the later editors and copyists have
done this job for us, which is good, but it is also possible that someone has
made mistakes or that the original intention of the word structure has never
really been understood by any other readers but the author of the text. To give
a hint of the complex issue involved on this topic, one may read a good article
from this blog post:

http://hellenisteukontos.blogspot.fi/2010/03/what-are-longest-words-of-greek.html

All the texts in the downloaded corpora can be found in online readable format
from these websites:

1. http://catalog.perseus.org/
2. http://cts.dh.uni-leipzig.de/
3. http://opengreekandlatin.github.io/First1KGreek/

__Highest isopsephy__

Finally, lets print out text sources and excerpts of the text containing the
biggest isopsephical values of the words:

```python
# collect the plain text words from the already instantiated m variable
words = list(y[0] for x, y in m.T.items())
search_words_from_corpora(words, [perseus_dir, first1k_dir])
```

Output:

```
+ Appian, TheCivilWars (tlg0551.tlg017.perseus-grc2.xml) =>

----- ΣΥΝΥΠΟΧΩΡΟΥΝΤΩΝ (1) -----
καὶ ἡ σύνταξις ἤδη παρελέλυτο ὀξύτερον ὑπεχώρουν καί τῶν ἐπιτεταγμένων σφίσι
δευτέρων καὶ τρίτων συνυποχωρούντων μισγόμενοι πάντες ἀλλήλοις ἀκόσμως
ἐθλίβοντο ὑπὸ σφῶν καὶ τῶν πολεμίων ἀπαύστως αὐτοῖς ἐπικειμένων

+ Aristophanes, Wasps (tlg0019.tlg004.perseus-grc1.xml) =>

----- ΟΡΘΡΟΦΟΙΤΟΣΥΚΟΦΑΝΤΟΔΙΚΟΤΑΛΑΙΠΩΡΩΝ (1) -----
ς ἀκούειν ἡδἔ εἰ καὶ νῦν ἐγὼ τὸν πατέρ ὅτι βούλομαι τούτων ἀπαλλαχθέντα τῶν
ὀρθροφοιτοσυκοφαντοδικοταλαιπώρων τρόπων ζῆν βίον γενναῖον ὥσπερ Μόρυχος
αἰτίαν ἔχω ταῦτα δρᾶν ξυνωμότης ὢν καὶ φρονῶν

+ Athenaeus, Deipnosophistae (tlg0008.tlg001.perseus-grc3.xml) =>

----- ΒΡΥΣΩΝΟΘΡΑΣΥΜΑΧΕΙΟΛΗΨΙΚΕΡΜΑΤΩΝ (1) -----
τῶν ἐξ Ἀκαδημίας τις ὑπὸ Πλάτωνα καὶ Βρυσωνοθρασυμαχειοληψικερμάτων πληγεὶς
ἀνάγκῃ ληψολιγομίσθῳ τέχνῃ σ

+ Athenaeus, TheDeipnosophists (tlg0008.tlg001.perseus-grc4.xml) =>

----- ΒΡΥΣΩΝΟΘΡΑΣΥΜΑΧΕΙΟΛΗΨΙΚΕΡΜΑΤΩΝ (1) -----
Βρυσωνοθρασυμαχειοληψικερμάτων πληγεὶς ἀνάγκῃ ληψιλογομίσθῳ τέχνῃ

+ AlexanderOfAphrodisias, InAristotelisMetaphysicaCommentaria (tlg0732.tlg004.opp-grc1.xml) =>

----- ΟΥΝΙΚΑΝΩΣΠΕΡΙΑΥΤΩΝΗΜΙΝΕΝΤΟΙΣΠΕΡΙ (1) -----
οιησά αενο τ ιστεύσομεν ρ Φ τεθεώρηται μὲν οὐνὶκανῶςπερὶαὐτῶνἡμῖνἐντοῖςπερὶ
φύσεως ἰκαὶἱκανῶς φησί περὶτῶ ν ἀρχῶν τῶν φυσικῶν ἐν τοῖς περὶ φύσεως

+ ApolloniusDyscolus, DeConstructione (tlg0082.tlg004.1st1K-grc1.xml) =>

----- ΚΑΙΤΟΝΑΡΙΣΤΑΡΧΟΝΑΣΜΕΝΩΣΤΗΝΓΡΑΦΗΝΤΟΥ (1) -----
ἠλογῆϲθαι φαϲ δὲ καίτὸνἈρίϲταρχονἀϲμένωϲτὴνγραφὴντοῦ Δικαιάρχουπαραδέξαϲθαι
ἐνγὰρἁπάϲαιϲ ν τὸ εὲῇ ἐν πατρίδι γαί ὑπολαβόντα τὸ ἑαυτῆϲ νοεὶϲθαι ἐκ το

----- ΑΡΣΕΝΙΚΩΝΟΝΟΜΑΤΩΝΣΤΟΙΧΕΙΑΕΣΤΙΠΕΝΤΕ (1) -----
τ τὸ ᾶ τελικόν ἐϲτιν κτλ Τελικὰ ἀρϲενικῶνὸνομάτωνϲτοιχεῖάἐϲτιπέντε
θηλυκῶνδὲ ὸκτώ ᾶη ωνξΒ ψ οὐδετέ ρων δὲ ἐ ῦ εραίαν

----- ΑΡΙΣΤΑΡΧΟΣΚΑΙΟΙΑΠΟΤΗΣΣΧΟΛΗΣΦΑΣΙΝ (1) -----
αὐτῇ Ϲ θϲτή εϲι Β καθότ Ϲ καθ ϲ ὁ Ἀρίϲταρχοϲκαὶοίἀπὸτῆϲϲχολῆϲφαϲιν οὶϲ οὐ
ϲυγκαταθετέον ε φαϲίν οὐκ ὀρθῶϲ

+ ApolloniusDyscolus, DePronominibus (tlg0082.tlg001.1st1K-grc1.xml) =>

----- ΩΡΙΣΜΕΝΩΝΠΡΟΣΩΠΩΝ (1) -----
ι καὶ τὰ ἀναφερύμενα γνῶϲιν ἐπαγγέλλεται προῦφεϲτῶϲαν ὅ ἐϲτι πάλιν πρόϲωπον
ὡριϲμένον ὀρθῶϲ ἄρα ὡριϲμένωνπροϲώπων παραϲτατικὴ ἡ ἀντωνυμία

+ Aristotle, MagnaMoralia (tlg0086.tlg022.1st1K-grc1.xml) =>

----- ΤΩΟΡΘΩΕΚΑΣΤΑΘΕΩΡΩΝ (1) -----
καὶ μὴ διεψεῦσθαι τῷ λόγῳ ἔστιν δὲ καὶ ὁ φρόνιμός τοιοῦτος ὁτῷ λόγῳ
τῷὀρθῷἕκασταθεωρῶν πότερον δ ἐνδέχεταιτὸν φρόνιμον ἀκρατῆ εἶναι ἢ οὔ
ἀπορήσειε γὰρ ἄν τις τὰ εἰρημένα ἐὰν δὲ πα ρ
```

That's all for the Greek corpora processing and basic statistics. One could
further investigate, categorize, and compare individual texts, but for me this
is enough and it is time to jump to the second big task that is defining
procedures for the riddle solver.

{% include 'footnotes.md' %}
