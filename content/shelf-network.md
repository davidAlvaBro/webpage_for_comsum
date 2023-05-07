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
This way the maximal value of $e_{book_i, book_j}$ is 1, and the value represents the chance of $book_i$ being on a shelf given $book_j$ is on that shelf, 
$$e_{book_i, book_j} \approx \mathbb{P}(book_i | book_j), C_{book_i} \geq C_{book_j}.$$
Here $\mathbb{P}(book_i | book_j)$ is the probability of $book_i$ being on a shelf, given $book_j$ is on that shelf. This only holds when $C_{book_i} \geq C_{book_j}$, because we only divide with the minimum of the two. In the opposite case, $ C_{book_j} \geq C_{book_i}$, the edge respresents $\mathbb{P}(book_j | book_i)$.  <br>

The value 0.5 is chosen because we do not want a too densely connected graph, but we also want as many of the books to still be in the dataframe as possible. At last the value 0.5 also expresses that for an edge to be there, then the books must appear together at least in half of the shelves where the book that is in the least shelves appears.


## **Choice of threshold**
There are 28,704,535 unique appearances together of the 7676 books, hence, if we did not create a threshold the graph would have an average degree of 3740, which is half of the network size. Thus, we need a threshold to get a less connected graph.<br>
We explored three different weighings for the edges.
- Purely appearances together 
- Appearances together, divided by the square root of appearance counts of the two books. 
- Appearances together, divided by the smallest appearance count of the two books.


Here you see the distribution of the pairs of books appearing together. 
<img src="/images/distribution_of_books_appearing_together.png" width="500" /> 
This distribution is fairly close to a power law distribution (it is almost a straight line on a log-log scale), thus if we remove edges with low amount of appearences we will remove a lot of edges. This first method has the issue that books that appear more often in the dataset will be more likely to have appeared more times with the other books, hence, books that appear few times will be removed entirely, if we use the first method of weighing. Therefore, we needed something more adaptive.
<br><br>
In the second method the edge weights are given by, 
$$e_{book_i, book_j} = \frac{C_{book_i, book_j}}{\sqrt{C_{book_i} \cdot C_{book_j}}}.$$
This introduces a new issue, which is that if a book $book_{i}$ always appear together with $book_{j}$, but $book_{j}$  is much more frequent in the dataset, then the edge between these two books is given a low weight. This means that books that frequently appear in the dataset will always have small edge weights, and thus, will be removed if we set a threshold. This is not ideal either, as *The Hunger Games* should probably always appear in shelves that have *Catching Fire* (the second Hunger Games book), but the other way around is probably not true, as people might not had read that far yet. These two books should definitly have a strong connection, as most users look at both. 
<br><br>
The last method is the one we use. This is because all books have a chance of forming strong edges with all other books. 
To evaluate if 0.5 is a possible threshold we try it, along with other thresholds, and observe how many books are completely dropped, and we look at the degree distribution. In these findings a threshold in the range 0.4-0.5 is optimal, as the graph has almost all books included (7665-7539), but does not have insanly high degrees (33-15). We choose 0.5, because we want to distinguish the graph into communitites that are not too large, and because of the nice property that the books appear togther at least half of the time the least frequent book appears. 


# **Network**
The network is implemented with *NetworkX* and has 7539 nodes and 109,627 edges. The edges has the weights described above and the nodes are given following attributes: *genres* (containing all genres that the book has been assigned), *title* and the *top_genre*. [TODO write about Assortativity (genres and degree)]()

### **Assortativity**
We are insterested in the structure of which books users choose to read together, therefore we investigate the assortativity of the genre in the *Shelf Graph*. We look at the assortativity of the *top_genre*. This test might not be that informative, because *top_genre* per construction simplifies the genre of a book to one genre. However, two genres might overlap or even be a sub-category of each other, such as *religon* and *christian*. If a *christian* book links to a *relgion* book in the above test, this will count towards disassortativity, however, from a genre perspective these two are very related. 

Because of this we also check the another form for mixing pattern, this time using all of a books genres, such that when two books $book_i$ and $book_j$ link we check if the set of their genres have any overlap. This will yield a larger fraction when checking, for each book, the amount of neighbours that meets the requirement. This measure descripes how many books are connnected to ones with at least one matching genre, and are not as restricted as the assortativity measure mentioned above.
 But as seen in the results below because we are interested in the relationship between the structure of the graph and the *top_genres*. To see if this assortat

# **Communities**
We use the Louvain algorithm to partition our graph into communities. We get 34, where the largest community is quite big and has [TODO insert number of nodes in the largest community](). We calculate the modularity of this partitioning to be [TODO insert here](), and check if this is significant. To do this we utilize the double edge swap algorithm to create a new graph, but where each node has the same degree as the previous graph. We do this [TODO how many times?](), to check if the modularity of the true network is significantly different. Below you can see the histogram of modularities for the random networks, along with the modularity of the true network.
<img src="/images/dtu-logo.png" width="200" />  [TODO insert the correct figure here]()
We can see that the modularity of the true network is indeed an outlier, and we have likely found interesting communities. 

# **Genres**
Next is the most interesting analysis we make. We use the communities found with the Louvain algorithm along with the true genres of the books (found with NLP analysis) to create a heatmap of the communities and genres. The heatmap is seen below. 
<img src="/images/dtu-logo.png" width="200" />  [TODO insert the correct figure here (genre vs. shelf heatmap)]()
The number assigned to each cell is the number of books in that the corresponding community that also have the corresponding genre. The color of each cell is the ratio between the cells number and the sum of the column. This is to only highlight the cells that contain an entire genre. 
<br>
As can be seen in this figure, most of the gernes are encapsulated by one community, however, this is mostly due to the large community that contains roughly a third of the books. 
[TODO comment on this further when we have the data. Maybe highlight a few community genre pairs]()


# **Word Clouds**
[TODO comment on this when we have the data]()