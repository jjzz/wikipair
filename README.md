## About Wikipair

Wikipair is to download and parse wiki dump sql files and produce
a simple bilingual title-pair dsl-format dict automatically.

Wikipair only use common shell commands. No database environment is required.

There is no detailed interpretation about these entries in the produced
dsl dict. For example, in en-zh dsl, looking up "Halfmoon Bluff" will
only give "半月海崖", or vice versa.

Default language is English, the second language should be specified as
the position argument of the script.

Some powerful numbers:
* en-fr dsl has 1260k pairs
* en-es dsl has  896k pairs
* en-ru dsl has  760k pairs
* en-zh dsl has  538k pairs

Requirements:
* \~2GB downloads, fast internet connection
* \~3GB temporary free disk space totally, but the final dsl is only 20\~60MB

Usage:
```bash
wikipair zh --langname Chinese
# After downloading, everything else will be done in ~20 minutes.
```

The dsl-format is supported by many software, including GoldenDict.

## Useful Links

* Offline Wikipedia in zim format,

    http://www.kiwix.org

    http://download.kiwix.org/zim/

* GoldenDict,

    https://github.com/goldendict/goldendict

* Wiki Dump,

    https://dumps.wikimedia.org/backup-index-bydb.html

    https://dumps.wikimedia.org/enwiki/latest/

* Wiki Dump Schema,

    https://www.mediawiki.org/wiki/Manual:Database_layout

    https://www.mediawiki.org/wiki/Category:MediaWiki_database_tables

    https://www.mediawiki.org/wiki/Manual:Page_table

    https://www.mediawiki.org/wiki/Manual:Langlinks_table

* List of ISO 639-1 codes (2-letter language code),

    https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes

* DSL Dictionary format,

    http://lingvo.helpmax.net/en/troubleshooting/dsl-compiler/your-first-dsl-dictionary/

## More on Data Source/Output, as of 2017.12.10,

#### data source: page.sql.gz

```text
# data entry example
# id, namespace, page-title-en, ...
29554612,0,'Halfmoon Bluff','',0,0,0,0.973692123679,'20171129113218','20171117050404',691742441,708,'wikitext',NULL
```

There are total 43,750,316 entries, including 13,607,099 main articles in the main namespace.

Only 40% of the main articles are real articles, 60% of them are redirects

*Note*: If you use the kiwix offline Wikipedia, you'll notice that the zim files contain those pages in namespace 0/8/12 (main/mediawiki/help) only. Here We'll limit our processing in main namespace.

#### data source: langlinks.sql.gz

```text
# data entry example
# id, lang-code, page-title
29554612,'de','Halfmoon Bluff'
29554612,'nn','Halfmoon Bluff'
29554612,'zh','半月海崖'
```

There are 26,323,171 entries from 300+ different languages

Languages with 100k+ entries in langlinks dump are listed below.

```text
1491578 fr  643360 ar   352434 hu          224223 bg      131035 hr
1247102 de  631855 ja   344565 ro          214952 he      126654 lt
1123058 it  559802 vi   343837 cs          214455 da      126325 be
1096328 es  548230 uk   318618 war         207458 sk      125728 gl
 975983 ru  496731 ceb  288857 id          166912 simple  124681 ka
 918314 sv  444557 ko   285366 sr          164774 nn      123934 az
 906950 nl  435212 ca   277800 eu          162444 hy      120928 et
 906105 pl  432300 no   260450 sh          154094 sl      119569 vo
 900508 pt  376754 ur   253142 ms          146250 el      111734 mk
 866408 fa  368088 tr   230774 eo          144059 la      111606 kk
 703217 zh  360848 fi   227606 zh-min-nan  131526 th      101220 uz
```

For any specific language, around 80% of the entries could be matched in main
namespace with English Wikpedia, and then built into the final dsl.

For a full list of all available languages, run `wikipair --stat-lang`

#### Output

The .dsl is the final dictionary file, loaded by dictionary software.

```text
Halfmoon Bluff
	<<半月海崖>>
半月海崖
	<<Halfmoon Bluff>>
```

The .txt is an intermediate file, kept for your reference.

```text
29554612|Halfmoon Bluff|半月海崖
```

The .ann/.bmp created automatically are supplementary and optional.

## END

License: MIT

Author: jjzz
