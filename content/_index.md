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


# TODO list for content 
## Idea 
- Find social trends in which books people read - yes?
- Social vs NLP analysis - yes?

## Data 
- Where do we get the data from - yes?
    - Like the slides: Goodreads and random guy - yes?  
    - Specs (All the sizes) - little more? 
    - Biases?! TODO 

## Preprocessing 
- Collect datasets into one 
    - Match titles of books 
    - Clean dataset from duplicates and the likes 

## Preprocessing II - Generate networks 
- Shelves network 
    - Choice of weighting of edges
    - Chose threshhold 
    - Use NetworkX to create network
- TL-IDF 
    - Generate TL-IDF scores for each book
    - And for each Genre 
    - Chose top genre for each book with TF-IDF 
    - Make edges with TF-IDF inner products (normalized)
    - Generate network to have as many edges as the shelves one 

## Network Analysis 
- Communities 
    - Louvain to create networks
    - Check modularity to know if we form communities
    - Compare communities from the networks, and the genres
        - Create confusion matrices (do they find the same?)

- Assortativity 
    - Assortativity between genres 
    - Assortativity for degree? 

## NLP Analysis 
- Create word clouds for communities 

## Conclusion 
- Shelves better decides genre in communities 




# I am DAVID 
Donec posuere justo at risus [efficitur convallis](#). Donec enim nibh, aliquet vel risus id, tincidunt consectetur felis. Proin porttitor odio a orci accumsan bibendum id at risus. Sed a posuere odio, ac lobortis augue. Maecenas aliquet ipsum vel libero dignissim, non aliquet justo eleifend. Fusce mollis, ante eget tincidunt imperdiet, mi ligula venenatis ex, ut pulvinar nunc ipsum tempus eros. Aliquam erat volutpat. Sed id _iaculis arcu_, sit amet varius libero. Etiam quis nisl pretium, eleifend quam nec, rutrum sapien. **Donec rutrum accumsan orci.**


## Math formula


$$ x^n + y^n = z^n $$

## Code chunk

```
import pandas as pd

df = pd.DataFrame()
```

Sed id orci ullamcorper, commodo sapien in, scelerisque nunc. Duis posuere sed nisl in gravida. Pellentesque rutrum justo ut mi tempus dignissim. Ut pulvinar quis urna ut molestie. Pellentesque nec arcu metus. Vivamus non rutrum magna. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.

![](https://source.unsplash.com/random/?Copenhagen)

Phasellus viverra tellus viverra purus placerat, et lacinia mauris tristique. Nam semper venenatis lorem, nec ullamcorper tortor dignissim eget. Etiam non ipsum sed neque pharetra ullamcorper. Praesent ultrices ipsum varius dictum lacinia. Nulla placerat magna augue, volutpat rutrum nulla finibus sed. Phasellus maximus mi sit amet risus mattis, porta rhoncus elit dictum. Donec vel viverra lectus, vitae elementum arcu. Quisque quis molestie elit. Cras eget tellus vitae risus fermentum bibendum vitae ac turpis. Praesent mi eros, scelerisque sit amet sem at, hendrerit accumsan ligula.

> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam nec mauris aliquet, convallis ligula vel, mollis est. Fusce accumsan massa vel lectus dapibus, at vehicula elit auctor.



## [Explainer Notebook](explainer-notebook.html)

Aenean non augue vulputate, bibendum ligula ac, euismod arcu. Proin consequat, urna at lobortis sodales, ligula nulla molestie dolor, et interdum nulla arcu eu lacus. Aenean maximus mi vel augue blandit, quis vehicula libero egestas. In mollis nibh in turpis sodales, eget luctus sem pretium. Integer lobortis diam vel nisi laoreet, ut condimentum risus ultrices. Praesent diam risus, imperdiet at lorem in, hendrerit auctor ex.