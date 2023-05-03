---
title: Shelf Network
prev: data-description
next: nlp-network
---
In the network books are nodes and edges are created if many consumers have both books on their shelves. 
# **Edges**
An edge is created in the graph if, 

$$e_{book_i, book_j} = \frac{C_{book_i, book_j}}{\min_{i, j}(C_{book_i}, C_{book_j})} \geq \frac{1}{2}$$

where $C_{book_i, book_j}$ is the number of shelves $book_i$ appears in which $book_j$ also appears in, likewise $C_{book_i}$ is the amount of shelves $book_i$ appears in. 
This way the maximal value of $e_{book_i, book_j}$ is 1, and the value represents the chance of $book_i$ being on a shelf given $book_j$ is on that shelf (here it is assumed that $C_{book_i} \geq C_{book_j}$, as the reverse is not true). <br>

The value 0.5 is chosen because we do not want a too densely connected graph, but we also want as many of the books to still be in the dataframe as possible. At last the value 0.5 also expresses that for an edge to be there, then the books must appear together at least in half of the shelves where the book that is in the least shelves appears.


## **Choice of threshhold**
[TODO put in a picture of a distribution here]()
There are 28,704,535 unique appearances together of the 7676 books, hence, if we did not create a threshhold the graph would have an average degree of 3740, which is half of the network size. We definitly need a threshhold to get a less connected graph.<br>
We explored three different weighings for the edges.
- Purely appearances together 
- Appearances together, divided by the square root of appearance counts of the two books. 
- Appearances together, divided by the smallest appearance count of the two books.
<br>
The first method has the issue that books that appear more often in the dataset will be more likely to have appeared more times with the other books, hence, books that appear little will not be removed entirely from the if we use the first method of weighing. Therefore, we needed something more addaptive. 
<br>
In the second method the edge weights are given by, 

$$e_{book_i, book_j} = \frac{C_{book_i, book_j}}{\sqrt{C_{book_i} \cdot C_{book_j}}}.$$

This introduces a new issue, which is that if a book $book_{i}$ always appear together with $book_{j}$, but $book_{j}$  is much more frequent in the dataset, then the edge between these two books is small. This means that books that frequently appear in the dataset will always have small edge weights, and thus, will be removed if we set a threshhold. This is not ideal either, as *The Hunger Games* should probably always appear in shelves that have *Catching Fire* (the second Hunger Games book), but the other way around is probably not true, as people might not had read that far yet. These two books should definitly have a strong connection, as must users look at both. 
<br>
The last method is the one we use. This is because all books have a chance of forming strong edges with all other books. 
To evaluate if 0.5 is a possible threshold we try it, along with other thresholds, and observe how many books are completely dropped, and we look at the degree distribution. In these findings a threshhold in the range 0.4-0.5 is optimal, as the graph has almost all books included (7665-7539), but does not have insanly high degrees (33-15). We choose 0.5, because we want to distinguish the graph into communitites that are not too large, and because of the nice property that the books appear togther at least half of the time the least frequent book appears. 


# **Network**
The network is implemented with *NetworkX* and [TODO write about attributes here](). [TODO write about Assortativity (genres and degree)]()

# **Communities**
We use the Louvain algorithm to partition our graph into communities. We get [TODO insert the number of communities](), where the largest community is quite big and has [TODO insert number of nodes in the largest community](). We calculate the modularity of this partition to be [TODO insert here](), and check if this is significant. To do this we utilize the double edge swap algorithm to create a new graph, but where each node has the same degree as the previous graph. We do this [TODO how many times?](), to check if the modularity of the true network is significantly different. Below you can see the histogram of modularities for the random networks, along with the modularity of the true network.
![](/images/dtu-logo.png) [TODO insert the correct figure here]()
We can see that the modularity of the true network is indeed an outlier, and we have likely found interesting communities. 

# **Genres**
Next is the most interesting analysis we make. We use the communities found with the Louvain algorithm along with the true genres of the books (found with NLP analysis) to create a heatmap of the communities and genres. The heatmap is seen below. 
![](/images/dtu-logo.png) [TODO insert the correct figure here (genre vs. shelf heatmap)]()
The number assigned to each cell is the number of books in that the corresponding community that also have the corresponding genre. The color of each cell is the ratio between the cells number and the sum of the column. This is to only highlight the cells that contain an entire genre. 
<br>
As can be seen in this figure, most of the gernes are encapsulated by one community, however, this is mostly due to the large community that contains roughly a third of the books. 
[TODO comment on this further when we have the data. Maybe highlight a few community genre pairs]()


# **Word Clouds**
[TODO comment on this when we have the data]()