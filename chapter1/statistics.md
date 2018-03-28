## Statistics

After the files have been downloaded and preprocessed, I'm going to
output the size of them:

``` {.sourceCode .python}
from functions import get_file_size

print("Size of the all raw text: %s MB" % get_file_size(all_greek_text_file))
print("Size of the perseus raw text: %s MB" % get_file_size(perseus_greek_text_file))
print("Size of the first1k raw text: %s MB" % get_file_size(first1k_greek_text_file))
```

Output:

``` {.sourceCode .txt}
Size of the all raw text: 347.76 MB
Size of the perseus raw text: 107.41 MB
Size of the first1k raw text: 240.35 MB
```

Then, I will calculate other statistics of the saved text files to
compare their content:

``` {.sourceCode .python}
from functions import get_stats

ccontent1, chars1, lwords1 = get_stats(perseus_greek_text_file)
ccontent2, chars2, lwords2 = get_stats(first1k_greek_text_file)
ccontent3, chars3, lwords3 = get_stats(all_greek_text_file)
```

Output:

``` {.sourceCode .txt}
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

### Letter statistics

I'm using DataFrame class from Pandas library to handle tabular data
and show basic letter statistics for each corpora and combination of
them. Native Counter class in Python is used to count unique elements in
the given sequence. Sequence in this case is the raw Greek text stripped
from all special characters and spaces, and elements are the letters of
the Greek alphabet.

This will take some time to process too:

``` {.sourceCode .python}
from functions import Counter, DataFrame
# perseus dataframe
df = DataFrame([[k, v] for k, v in Counter(ccontent1).items()])
df[2] = df[1].apply(lambda x: round(x*100/chars1, 2))
a = df.sort_values(1, ascending=False)
# first1k dataframe
df = DataFrame([[k, v] for k, v in Counter(ccontent2).items()])
df[2] = df[1].apply(lambda x: round(x*100/chars2, 2))
b = df.sort_values(1, ascending=False)
# perseus + first1k dataframe
df = DataFrame([[k, v] for k, v in Counter(ccontent3).items()])
df[2] = df[1].apply(lambda x: round(x*100/chars3, 2))
c = df.sort_values(1, ascending=False)
```

The first column is the letter, the second column is the count of the
letter, and the third column is the percentage of the letter contra all
letters.

``` {.sourceCode .python}
from functions import display_side_by_side
# show tables side by side to save some vertical space
display_side_by_side(Perseus=a, First1K=b, Perseus_First1K=c)
```

#### Table data

+-----------------------+-----------------------+-----------------------+
| Perseus               | FirstK1               | Both                  |
+=======================+=======================+=======================+
| > Letter Count        | > Letter Count        | > Letter Count        |
| > Percent             | > Percent             | > Percent             |
+-----------------------+-----------------------+-----------------------+
| ========= =========   | ========= =========   | ========= =========   |
| =========             | =========             | =========             |
+-----------------------+-----------------------+-----------------------+
| > Α 4182002 10.96     | > Α 26817705 10.76    | > Α 30999707 10.79    |
+-----------------------+-----------------------+-----------------------+
| > Ε 3678672 9.64      | > Ο 23687669 9.50     | > Ο 27351703 9.52     |
+-----------------------+-----------------------+-----------------------+
| > Ο 3664034 9.61      | > Ι 22665483 9.09     | > Ι 26279145 9.14     |
+-----------------------+-----------------------+-----------------------+
| > Ι 3613662 9.47      | > Ε 22498413 9.03     | > Ε 25909263 9.01     |
+-----------------------+-----------------------+-----------------------+
| > Ν 3410850 8.94      | > Ν 22121458 8.88     | > Ν 25800130 8.98     |
+-----------------------+-----------------------+-----------------------+
| > Τ 2903418 7.61      | > Τ 21698265 8.71     | > Τ 24601683 8.56     |
+-----------------------+-----------------------+-----------------------+
| > Σ 2830967 7.42      | > Σ 18738234 7.52     | > Σ 21569201 7.50     |
+-----------------------+-----------------------+-----------------------+
| > Υ 1776871 4.66      | > Υ 11384921 4.57     | > Υ 13161792 4.58     |
+-----------------------+-----------------------+-----------------------+
| > Ρ 1440852 3.78      | > Η 9776411 3.92      | > Η 11217263 3.90     |
+-----------------------+-----------------------+-----------------------+
| > Η 1392909 3.65      | > Ρ 9268111 3.72      | > Ρ 10661020 3.71     |
+-----------------------+-----------------------+-----------------------+
| > Π 1326596 3.48      | > Κ 8982955 3.60      | > Κ 10244628 3.56     |
+-----------------------+-----------------------+-----------------------+
| > Κ 1261673 3.31      | > Π 8290364 3.33      | > Π 9616960 3.35      |
+-----------------------+-----------------------+-----------------------+
| > Ω 1179566 3.09      | > Ω 7874161 3.16      | > Ω 9053727 3.15      |
+-----------------------+-----------------------+-----------------------+
| > Μ 1147548 3.01      | > Μ 7498489 3.01      | > Μ 1147548 3.01      |
+-----------------------+-----------------------+-----------------------+
| > Λ 1139510 2.99      | > Λ 6929170 2.78      | > Λ 8076718 2.81      |
+-----------------------+-----------------------+-----------------------+
| > Δ 932823 2.45       | > Δ 5757782 2.31      | > Δ 6690605 2.33      |
+-----------------------+-----------------------+-----------------------+
| > Γ 584668 1.53       | > Γ 4197053 1.68      | > Γ 4781721 1.66      |
+-----------------------+-----------------------+-----------------------+
| > Θ 501512 1.31       | > Θ 3440599 1.38      | > Θ 3942111 1.37      |
+-----------------------+-----------------------+-----------------------+
| > Χ 352579 0.92       | > Χ 2294905 0.92      | > Χ 2647484 0.92      |
+-----------------------+-----------------------+-----------------------+
| > Φ 325210 0.85       | > Φ 2115768 0.85      | > Φ 2440978 0.85      |
+-----------------------+-----------------------+-----------------------+
| > Β 220267 0.58       | > Β 1322737 0.53      | > Β 1543004 0.54      |
+-----------------------+-----------------------+-----------------------+
| > Ξ 152971 0.40       | > Ξ 951076 0.38       | > Ξ 1104047 0.38      |
+-----------------------+-----------------------+-----------------------+
| > Ζ 75946 0.20        | > Ζ 559728 0.22       | > Ζ 635674 0.22       |
+-----------------------+-----------------------+-----------------------+
| > Ψ 51405 0.13        | > Ψ 375266 0.15       | > Ψ 426671 0.15       |
+-----------------------+-----------------------+-----------------------+
| > Ϝ 349 0.00          | > Ϛ 5162 0.00         | > Ϛ 5171 0.00         |
+-----------------------+-----------------------+-----------------------+
| > Ϛ 9 0.00            | > Ϡ 259 0.00          | > Ϝ 505 0.00          |
+-----------------------+-----------------------+-----------------------+
| > Ϡ 4 0.00            | > Ϝ 156 0.00          | > Ϡ 263 0.00          |
+-----------------------+-----------------------+-----------------------+
| > Ϟ 3 0.00            | > Ϟ 111 0.00          | > Ϟ 114 0.00          |
+-----------------------+-----------------------+-----------------------+
| > 0 0.00              | > Ϙ 13 0.00           | > Ϙ 13 0.00           |
+-----------------------+-----------------------+-----------------------+

Greek corpora contains mathematical texts in Greek, which explains why
the rarely used digamma (Ϝ/Ϛ = 6), qoppa (Ϟ/Ϙ = 90), and sampi (Ϡ = 900)
letters are included on the table. You can find other interesting
differences between Perseus and First1k corpora, like the occurrence of
Ρ/Η, K/Π, and Ο/Ι/Ε which are probably explained by the difference of
the included text genres in corpora.

#### Bar chart

The next chart will show visually which are the most used letters and
the least used letters in the available Ancient Greek corpora.

![image](stats.png)

Vowels with N, S, and T consonants pops up as the most used letters. The
least used letters are Ζ, Ξ, and Ψ, if the exclusive numerals Ϛ, Ϟ, and
Ϡ are not counted.

#### Optional live chart

Uncomment the next part to output a new fresh graph from Plotly:

``` {.sourceCode .python}
#import plotly
#plotly.offline.init_notebook_mode(connected=False)

# for the fist time set plotly service credentials, then you can comment
# next line
#plotly.tools.set_credentials_file(username='MarkoManninen', api_key='xyz')

# embed plotly graphs
#plotly.tools.embed("https://plot.ly/~MarkoManninen/8/")
```

{% include 'footnotes.md' %}
