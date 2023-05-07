---
title: Shelf Network
prev: nlp-network
---
# **Network Comparison**
When comparing the two networks we create a mixing matrix of their Louvain communities. This is seen below. 
<img src="/images/mixing_shelf_nlp.png" width="800" /> 
In this image we see that the mixing matrices are almost uniformly distributed with respect to the rows, hence, given the community of a book with respect to one of the graphs, we gain almost no knowledge about the community of the book with respect to the other graph. 

When comparing the two graphs the distinction between the social graph Shelf Graph, and the mathematical graph NLP Graph is stricking. The hairball structure of the NLP Graph is quite visable, while the structure of the Shelf Graph is more segmented and has hubs with large degrees. 

The natural language processing graph was created based on the descriptions of the books, however, as seen in the word clouds, these descriptions contain more information about authors and characters then about the contents of the book. This is problematic because we don't get books that are similar based on the contents, but instead have similar descriptions. This could be interesting, but in our case we compared these with genres, and the character and author names are not relevant for this. 

We see that the communities found with the Louvain algorithm with the two graphs are not correlated in terms of members. This suprised us at first, because we figured we could capture the same information with the social graph as the natural language processing graph, however, in hind sight these would only correlate if people read books with similar book descriptions (which sounds repetiative). <br>
Neither of the graphs are highly correlated with the *top_genre* either.
 


# **Conclusions**
We find that there is indeed structure to the Shelf Network generated, and thus, which books people read. However, this does not capture the *top_genres* found with NLP. The genres of the books seperates the communities quite well, when looked at individually as seen in [shelf network - Genres](https://davidalvabro.github.io/webpage_for_comsum/shelf-network#genres) the bottom plots. We also found that NLP does not find the same tendencies as a the shelf graph. 

A large problem with our approach of using TF-IDF vectors for book descriptions is that names will be the most important words. This does mostly not capture anything about the contents of the book. This also means that our wordclouds are less interesting to look at. 

At last for further research it could be interesting to look at entire books to capture the true content of these books. This might make interesting NLP Graphs, and would definitly yield interesting wordclouds. Especially if names are removed with clever filtering. 

Another idea, is to use reviews to capture sentiment about books. Then we could investigate which books are popular, what people like, and maybe express what each individual likes in books (requring people kept track of *liked books*). 

