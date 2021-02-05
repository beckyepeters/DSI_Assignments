## Becky's Solutions to Unix Assignment, Week 1 RPP2 

# Part 1: Set up a Directory for DSI

* `mkdir dsi_galvanize`
* `mkdir assignments`
* `cd assignments`
* `touch readme.md`
* `git clone https://github.com/GalvanizeDataScience/unix`
* `mkdir capstones`
* `cd capstones`
* `mkdir capstone1 capstone2 capstone 3`
* `touch readme.md`
* `cd ..`
* `git clone https://github.com/GalvanizeDataScience/lectures`
* `touch requirements.txt`
* `mkdir resources`
* `cd resources`
* `touch readme.md`

_________________________

# Part 2: Unix & CLI

1. `cd unix/data/`
2. `less 2015_sp100.csv`
3. `grep "GOOG" > 2015_goog.csv`
4. `sort t, 2015_goog.csv > 2015_goog_sorted.csv`
5. `python plot_stock_prices.py < 2015_goog_sorted.csv`
6. `grep "GOOG" | sort t, > 2015_goog_sorted.csv | python plot_stock_prices.py < 2015_goog_sorted.csv`


-------------------------

# Part 3: Wikipedia data: 

1. First I had to install wget with `brew install wget`; then `wget https://dumps.wikimedia.org/enwiki/latest/enwiki-latest-pages-articles1.xml-p1p41242.bz2` into my assignments/unix/data directory. Looks like `curl` command does the same thing but would only do the url in the command,  nothing recursive like wget would download. (For reference, site [here](https://daniel.haxx.se/docs/curl-vs-wget.html) with differences)
2. File type = `bzip2 compressed data`. Command to ascertain = `file enwiki-latest-pages-articles1.xml-p1p41242.bz2`. To decompress, I used `bzip2 <filename>`. Now (using `file` again) the type is HTML document text. 
3. Number of lines = 6349157 (found with `wc -l` command); size of file = 900297543 (found with `mdls` command; not sure if that is in bytes? So, 900 MB?); uncompressed version is HTML. 
4. Seems it would not be a good idea because of its large size. 
5. Here's what I got when executing the `head` command to look at the beginning of the file: 
```
    <mediawiki xmlns="http://www.mediawiki.org/xml/export-0.10/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.mediawiki.org/xml/export-0.10/ http://www.mediawiki.org/xml/export-0.10.xsd" version="0.10" xml:lang="en">
  <siteinfo>
    <sitename>Wikipedia</sitename>
    <dbname>enwiki</dbname>
    <base>https://en.wikipedia.org/wiki/Main_Page</base>
    <generator>MediaWiki 1.36.0-wmf.27</generator>
    <case>first-letter</case>
    <namespaces>
      <namespace key="-2" case="first-letter">Media</namespace>
      <namespace key="-1" case="first-letter">Special</namespace>
```
5 continued.... Used `tail` command to find this for the end of the file: 

```
*{{Intitle|horns}}
*{{Intitle|horn}}
*[[Hoorn (disambiguation)]]
*[[Horner (disambiguation)]]

{{disambiguation}}</text>
      <sha1>9yuddnvjgmgx7qpqba66te86c2qa9ca</sha1>
    </revision>
  </page>
</mediawiki>% 
```
6. I used the `less` command to peek at the first few pages of the file; in the pages were descriptions of Anarchism and Autism. I honestly can't ascertain much about the structure of the file from this code. There are a bunch of lines at the start specifying something about 'namespace' and then it launches into the anarchism text. 

7. `head -636120 enwiki-latest-pages-articles1.xml-p1p41242 | tail -n 20`

8. I used `grep -wc "/contributor" enwiki-latest-pages-articles1.xml-p1p41242` to find the count of the '/contributor' instance and it said there are `27444`. 

9. Command: `grep -wc "<username>" enwiki-latest-pages-articles1.xml-p1p41242`; Answer: 114. Then I did `grep "<username>" enwiki-latest-pages-articles1.xml-p1p41242 > username_data.csv` to put the username results into a csv file. Using `less` command to see what's inside, it looks like a lot more than 114 though. So for fun I looked at the same command with `"username"` (24772), `<username>` (77), and `"</username>` (114) to compare. So I still don't know the actual answer... 

10. I'm running up on my 2 hour time limit for this assignment; I see that `Monkbot` is the most common (2968 counts) by looking at the results from `sort username_data.csv | uniq -c` but couldn't figure out how to do it so it would just give me that number and name, I just scrolled through the results. 

11. Apparently the grep -E flag "Treats pattern as an extended regular expression (ERE)" but I don't really  know what that means. I did `grep -wc -E "[B\b][O\o][T\t]" enwiki-latest-pages-articles1.xml-p1p41242 > unique_bots.csv` and then uniq -c unique_bots.csv and it gave me 8571. 


