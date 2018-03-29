## Downloading corpora

I'm going to use `Perseus` and `OpenGreekAndLatin` corpora for the study by
combining them into a single raw text file and unique words database.

The next code snippets will download hundreds of megabytes of Greek text to a
local computer for quicker access. `tqdm` downloader requires a stable internet
connection to work properly.

One could also download packed source ZIP files via browser and place them to
the same directory with the Jupyter notebook or where Python is optionally run
in shell mode. ZIP files must then be renamed as `perseus.zip` and
`first1k.zip`.

1\. Download packed ZIP files from their GitHub repositories:

```python
from functions import download_with_indicator, perseus_zip_file, first1k_zip_file
# download from perseus file source
fs = "https://github.com/PerseusDL/canonical-greekLit/archive/master.zip"
download_with_indicator(fs, perseus_zip_file)
# download from first1k file source
fs = "https://github.com/OpenGreekAndLatin/First1KGreek/archive/master.zip"
download_with_indicator(fs, first1k_zip_file)
```

Output:

```
Downloading: https://github.com/PerseusDL/canonical-greekLit/archive/master.zip
71.00MB [04:15, 211.08KB/s]
Downloading: https://github.com/OpenGreekAndLatin/First1KGreek/archive/master.zip
195.00MB [09:15, 201.54KB/s]
```

2\. Unzip (extract) files to the corresponding directories:

```python
from functions import perseus_zip_dir, first1k_zip_dir, unzip
# first argument is the zip source, second is the destination directory
unzip(perseus_zip_file, perseus_zip_dir)
unzip(first1k_zip_file, first1k_zip_dir)
```

3\. Copy only suitable Greek text XML files from `perseus_zip_dir` and
`first1k_zip_dir` to the temporary work directories. Original repositories
contain a lot of unnecessary files for the riddle solver which are skipped in
this process.

```python
from functions import copy_corpora, joinpaths, perseus_tmp_dir, first1k_tmp_dir
# important Greek text files resides in the data directory of the repositories
for item in [[joinpaths(perseus_zip_dir,
              ["canonical-greekLit-master", "data"]), perseus_tmp_dir],
             [joinpaths(first1k_zip_dir,
              ["First1KGreek-master", "data"]), first1k_tmp_dir]]:
    copy_corpora(*item)
```

Output:

```
greek_text_perseus_tmp already exists. Either remove it and run again, or just use the old one.

Copying greek_text_first1k_tmp -> greek_text_first1k
```

Depending on if the files have been downloaded already, the output may differ.

{% include 'footnotes.md' %}
