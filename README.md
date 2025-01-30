# Information Retrieval

There are 3 main steps for developing an information retrieval algorithm:
1. Normalize the data
2. Pick an indexing method
3. Choose the searching method that fits best for you

## Normalization

In Lucene the classes that do this are called _Analyzer_. Some examples include:
- _WhiteSpaceAnalyzer_ - tokenizes the text based on white spaces
- _SimpleAnalyzer_ - tokenizes the text based on no-letter characters, converts to lowercase
- _StandardAnalyzer_ - removes stopwords, converts to lowercase

You can also read how these classes are implemented and customize them or write your own analyzer from scratch. 

## Indexing

Lucene uses an inverted index (_IndexWriter_): instead of keeping the keywords for each documents, it stores the list of keywords and each keyword has a link to the documents that contain them, frequency and position.

For example, if we have the following list of documents:

| DocumentID | Document     |
|------------|--------------|
| 1          | To to be     |
| 2          | Or not to be |

The corresponding list of keywords would be:

| TermID | Term | Docs                     |
|--------|------|--------------------------|
| 1      | to   | 1:2:[1, 2] <br/> 2:1:[3] |
| 2      | be   | 1:1:[3] <br/> 2:1:[4]    |
| 3      | or   | 2:1:[1]                  |
| 3      | not  | 2:1:[2]                  |

Where each item in `Docs` means `<documentID:Frequency:ListOfPositions>`

## Search

The default searcher (_IndexSearcher_) accepts a series of [parsing symbols](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html) for a more specialized search. 
How many of these keywords work the same way on [Google Search](www.google.com)?

## Run from command line

```shell
mvn package
java -jar target/docsearch-1.0-SNAPSHOT.jar org.example.Main
```

# Assignment

Write a Romanian Information Retrieval System as presented in the course. 

Your project should respect the following structure:

```
<group>_<familyName>_<givenName>
|-- README.md
|-- pom.xml
|-- src
    |-- main
        |-- java
            |-- org
                |-- example
                    |-- Main.java
                    |-- other relevant files
```

Use the current project as an example for what your `pom.xml` should contain. **Do not change** the 
`groupID`, `artifactID`, `version` and `build`, or the automated judging will not work and your project will be scored 
with 0 points!

In the `README.md` you should shortly describe your contribution.

## Deliverables

**Do not upload** the local setup folders (eg: `.idea/`, `.target/` etc.) or the files you used for testing! You can 
look at the present .gitignore for a short list of files / folders that should not be uploaded.

Upload your final project with the exact file structure described above. The root directory should be named 
`<group>_<familyName>_<givenName>`, replacing `<group>` with your current group (506, 507 etc), `<familyName>` with your 
surname and `<givenName>` with your first name. For example, `502_Cena_John` is a valid directory name, while 
`503_John_Cena`, `503_CenaJohn`, `503`, `Project` etc. may all result in 0 points on your assignment.

## Judging

Judging will be done automatically using the following script for Java:

```shell
mvn package
java -jar target/docsearch-1.0-SNAPSHOT.jar -index -directory <path to docs>
java -jar target/docsearch-1.0-SNAPSHOT.jar -search -query <keyword>
```

EDIT: Removed `-directory <path to docs>` from searcher

Or for Python:
```shell
pip install -r requirements.txt
python main.py -index -directory <path to docs>
python main.py -search -query <keyword>
```

Where `<path to docs>` will be replaced with the path to the folder containing all files to be indexed / searched, and
`<keyword>` will be replaced with the word / sentence the program will search for.

The output will be an ordered list of top 5 documents that contain the given phrase. Only the document names will be 
printed, one on each line.

