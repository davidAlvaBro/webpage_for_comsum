---
title: Social Graph of Books
layout: single
next: data-description
---
This webpage investigates the relationship between which books people read, their genres and their contents. 
[TODO Explain further?](#)

# **Idea** 
In this webpage we investigate the question;

> Do people tend to read the same genre of books? 

To answer this question we look at a social graph of books, where nodes are books and edges between books are created if the two books are both owned by the same user enough times. We use this graph to cluster books together in communities. We compare these communities with the true genres of the books, to see if there is a correlation. <br>
We also create another network where edges are created if the inner product between the normalized TF-IDF vector for each books description is larger than a certain threshhold. We imagine this network encaptures the [budskab](#Help cant translate) of the books. We compare this network with the social one to see if the two networks has roughly the same communities. 

# **Table of Contents** 
- [Social Graph of Books](/)
    - [Idea](#idea)
    - [Short Conclusion](#short-conclusion) 
- [Data Description](data-description) [TODO rename Data Decription](#)
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
    - [In Depth Conclusions](findings#in-depth-conclusions)

# Short Conclusion 
[TODO implement this](#) 

## [Explainer Notebook](explainer-notebook.html)

