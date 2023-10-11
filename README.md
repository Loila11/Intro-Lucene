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
