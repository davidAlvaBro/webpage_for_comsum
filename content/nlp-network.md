---
title: NLP Network
prev: shelf-network
next: findings
---
In the network books are nodes and edges are created if many the normalized TF-IDF vectors have larger inner products than some threshold. This network is made to have the same amount of edges as the [shelf network](shelf-network) by choosing an appropriate threshold.

*(disclaimer this page refers a lot to [shelf network](shelf-network), as the analysis made here is very similar. Read that page first!)*
# **Edges**
We take the inner product of all pairs of normalized TF-IDF vectors found in the preprocessing part of the project to make the weight attributed to each edge in the graph. Then we chose a threshold, 0.056, that yields the same number of edges, 109,627, as the we have in the [shelf network](shelf-network). 

# **Network**
Again the network is implemented with *NetworkX* and the nodes have the same attributes. 

### **Assortativity** TODO check this BODY
The same analysis done for the Shelf Graph is made here. The assortativity for the network with respect to genres is 0.19, which is slightly larger than for the Shelf Graph. 

The assortativity with respect to degree with varying thresholds is shown in the figure below. We see that links between high degree nodes and links between low degree nodes are more common in this network. This is due to the nature of creating a mathematical network where most nodes have the same likelihood of making a connections, while in the Shelf Graph we have a social network that is dependent on the human user.
<img src="/images/nlp_assortativity_degree.png" width="500" /> 

# **Communities**
The Louvain algorithm is again used to partition the graph into communities. We get 37 communities with the largest one having 721 members. This graph has more uniformly distributed in community sizes than the Shelf Graph, as seen in the histogram below: 
<img src="/images/nlp_louvain_community_distribution.png" width="500" /> 

We check if the modularity of this partition is significant with the same method as used for the [shelf network](shelf-network). 
<img src="/images/nlp_modularity_histogram.png" width="500" /> 

We see that the modularity of the NLP network has is significantly different from the randomly created networks where nodes have the same degree. 

# **Genres**
In this section we see the mixing matrix generated to inspect if the communities from the NLP graph indeed incaptures something about the genre. 
<img src="/images/mixing_nlp_genres.png" width="800" /> 
In this heatmap of the mixing matrix we see that there is really no correlation between *top_genre* and the communities of the NLP Graph. We can see this easily because the rows are almost uniformly distributed. In specific outlier is community 7 and the genre *cooking*, as 43 of the 45 *cooking* books are in this community. There are a lot more elements, but it is the dominating *genre*.

# **Visualization of the Network**
Below we visualize the network with the netwulf library. In the first plot the colors correspond to Louvain communities, while the second plot shows the network colored by *top_genre*. It is very difficult to see the communities and the genres in the plots below in the middle of the graphs. In the edges some communities form (mostly in the top plot - the community plot). This is again expected as this is not a social graph, and because the degree distribution is not extremely skewed, like it is for the Shelf Graph. 
<img src="/images/nlp_network_community.png" width="800" />
<img src="/images/nlp_network_top_genre.png" width="800" />


# **Word Clouds**
<img src="/images/nlp_wordcloud_7.png" width="500" />
<img src="/images/nlp_wordcloud_10.png" width="500" />
Most of the wordclouds for the communities captures names, either of authors or characters, but do not have much substance besides this. 
This is examplified with community 10 shown above. 
Community 7 does, however, seem to encapture cooking books which again shows that this genre have been completly captured by community 7.