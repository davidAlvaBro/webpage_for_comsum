---
title: Social Graph of Books
layout: single
next: data-description
---
This webpage investigates the relationship between which books people read, their genres and their contents. 
# **Idea** 
We would like to investigate this question;

> Is there a structure to the books that people read? 

To answer this question we look at a social graph of books, where nodes are books and edges are present between books if the two books are both owned by the same user enough times. We use this graph to cluster books together in communities. We compare these communities with the genres of the books, to see if there is a correlation. <br><br>
We also create another network where edges are created if the inner product between the normalized TF-IDF vector for each books description is larger than a certain threshhold. We imagine that the structure of this network resembels how the descriptions of the books are related. We compare this network with the social one to see if the two networks have roughly the same communities.

# **Table of Contents** 
- [Social Graph of Books](/)
    - [Idea](#idea)
    - [Short Conclusion](#short-conclusion) 
- [Data Description](data-description)
    - [Dataset](data-description#dataset) 
    - [Data Statistics](data-description#data-statistics)
    - [Merge Datasets](data-description#merge-datasets)
    - [TF-IDF of Books and Genres](data-description#TF-IDF-of-Books-an-Genres)
- [Shelf Network](shelf-network)
    - [Edges](shelf-network#edges)
    - [Network](shelf-network#network)
    - [Communities](shelf-network#communities)
    - [Genres](shelf-network#genres)
    - [Word Clouds](shelf-network#word-clouds)
- [NLP Network](nlp-network)
    - [Edges](nlp-network#edges)
    - [Network](nlp-network#network)
    - [Communities](nlp-network#communities)
    - [Genres](nlp-network#genres)
    - [Word Clouds](nlp-network#word-clouds)
- [Findings](findings)
    - [Network Comparison](findings#network-comparison)
    - [Conclusions](findings#conclusions)

# Short Conclusion 
We find that there is indeed structure to the Shelf Network generated and thus, what books people read. However, this does not capture the *top_genres* found with NLP. The genres of the books seperates the communities quite well, when looked at individually as seen in [shelf network - Genres](shelf-network#genres) the bottom plots. We also found that NLP graph does not find the same tendencies as a the Shelf Graph. 

A large problem with our approach of using TF-IDF vectors for book descriptions is that names will be the most important words. This does mostly not capture anything about the contents of the book. This also means that our wordclouds are less interesting to look at. 

At last for further research it could be interesting to look at entire books to capture the true content of these books. This might make interesting NLP Graphs, and would definitly yield interesting wordclouds. Especially if names are removed with clever filtering. 

Another idea, is to use reviews to capture sentiment about books. Then we could investigate which books are popular, what people like, and maybe express what each individual likes in books (requring people kept track of *liked books*). 
## [Explainer Notebook](https://github.com/davidAlvaBro/comsocsci_final_proj/blob/main/Explainer_notebook.ipynb)

