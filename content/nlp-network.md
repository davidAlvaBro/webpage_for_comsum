---
title: NLP Network
prev: shelf-network
next: findings
---
In the network books are nodes and edges are created if many the normalized TF-IDF vectors have larger inner products than some threshold. This network is made to have the same amount of edges as the [shelf network](shelf-network) by choosing an appropriate threshold.
# **Edges**
We take the inner product of all pairs of normalized TF-IDF vectors found in the preprocessing part of the project to make the weight attributed to each edge in the graph. Then we chose a threshold, [TODO what is the threshold?](), that yields the same number of edges, [TODO how many is that?](), as the we have in the [shelf network](shelf-network). 

# **Network**
Again the network is implemented with *NetworkX* and [TODO write about attributes here](). [TODO write about Assortativity (genres and degree)]()

# **Communities**
The Louvain algorithm is again used to partition the graph into communities. We get [TODO insert the number of communities](). This graph has more uniformly distributed community sizes, as seen in the histogram below: 
<img src="/images/dtu-logo.png" width="200" />  [TODO insert the correct figure here]()

We check if the modularity of this partition is significant with the same method as used for the [shelf network](shelf-network). 
<img src="/images/dtu-logo.png" width="200" />  [TODO insert the correct figure here]()

We see that the modularity of the NLP network has is significantly different from the randomly created networks where nodes have the same degree. 

# **Genres**
In this section you see the heatmap generated to view if the communities from the NLP graph indeed incaptures something about the genre. 
<img src="/images/dtu-logo.png" width="200" /> [TODO insert the correct figure here (genre vs. shelf heatmap)]()
 
[TODO comment on this further when we have the data. Maybe highlight a few community genre pairs]()


# **Word Clouds**
[TODO comment on this when we have the data]()