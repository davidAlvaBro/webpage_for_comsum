---
title: Shelf Network
prev: data-description
next: nlp-network
---
In the network books are nodes and edges are created if many consumers have both books on their shelves. 

*(The inline math fields do not work on all browsers, this may result in $ instead of latex)*
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
The network is implemented with *NetworkX* and has 7539 nodes and 109,627 edges. The edges has the weights described above and the nodes are given following attributes: *genres* (containing all genres that the book has been assigned), *title* and the *top_genre*. 

### **Assortativity**
We are insterested in the structure of which books users choose to read together, therefore we investigate the assortativity of the genre in the *Shelf Graph*. We look at the assortativity of the *top_genre*. This test might not be that informative, because *top_genre* per construction simplifies the genre of a book to one genre. However, two genres might overlap or even be a sub-category of each other, such as *religon* and *christian*. If a *christian* book links to a *relgion* book in the above test, this will count towards disassortativity, however, from a genre perspective these two are very related. 

Because of this we also check the another form for mixing pattern, this time using all of a books genres, such that when two books $book_i$ and $book_j$ link we check if the set of their genres have any overlap. This will yield a larger fraction when checking, for each book, the amount of neighbours that meets the requirement. This measure descripes how many books are connnected to ones with at least one matching genre, and are not as restricted as the assortativity measure mentioned above. But as seen in the results below this mixing pattern measure gets very large which probably is due to the books having a lot of genres.

The assortativity for the *top_genre* is 0.17 and the mixing pattern with all genres have an average of 0.92. This means that books are not that likely to be connect to ones with the same *top_genre* but are almost garenteed to be connected to ones that share at least one of their genres. However we see that when randomly assigning nodes attributes, the results of the mixing pattern measure does not change, indicating that each book has many genres and the overlap are therefor very likely regardless of the structure of the network. The assortativity for the *top_genre* does change to -0.0035, with a very small standard deviation (0.001), thus we conclude that the graph captures the *top_genre* better than it would at random. 


Books that have a high degree, also known as hubs, imply that many books are likely to be on the same shelf as they are, or that the high degree book is likely to be on a shelf given one of the neighbors are. We look at the assortativity for *high* or *low* degrees, to see if hubs connect to many hubs or they instead connect to many solitary books. We check different threshold that define when a degree is *high* or *low*. As seen on the figure below, there is a negative assortativity between hubs, which means that the hubs mostly connect to solitary books, and solitary books connect mostly to hubs. 
<img src="/images/shelf_assortativity_degree.png" width="500" /> 


# **Communities**
We use the Louvain algorithm to partition our graph into communities. We get 34, where the largest community is quite big and has 2905. The distribution of the sizes of the communities are seen in the histogram below. 
<img src="/images/shelf_louvain_community_distribution.png" width="500" /> 

We calculate the modularity of this partitioning to be 0.53, and check if this is significant. To do this we utilize the double edge swap algorithm to create a new graph, but where each node has the same degree as the previous graph. We do this 100 times, to check if the modularity of the true network is significantly different. Below you can see the histogram of modularities for the random networks, along with the modularity of the true network (in red).
<img src="/images/shelf_modularity_histogram.png" width="500" />  
We can see that the modularity of the true network is indeed an outlier, and we have likely found interesting communities.

Furthermore, we investigate if the *top_genre* partitions of the Shelf Graph will yield significant modularities (have found communities). The modularity for the *top_genre* partition is 0.17 which is not quite as large as the modularity for the Louvain communities, but still interesting. This indicate that there is some genre structure to the network. We cannot conclude if the Louvain communities and the genre partitions overlap yet, which is why we investigate their mixing matrices below. 


# **Genres**
We use the communities found with the Louvain algorithm along with the *top_genre* to create a mixing matrices of the communities and genres. This is visualized with a heatmap, see below. 
<img src="/images/mixing_shelves_genres.png" width="800" />  
The number assigned to each cell is the number of books in the corresponding community that also have the corresponding genre. The color of each cell is the ratio between the cells number and the sum of the column. This is to only highlight the cells that contain an entire genre. 


As can be seen in this figure, most of the gernes are encapsulated by one community, however, this is mostly due to the large community that contains roughly a third of the books. Another issue with this visualization is the issue that closely related genres are viewed as completely seperated entities. Because of this we go through each genre and visualize the mixing matrix of having this genre or not having this genre, by using *genres* instead of *top_genre*. In the below figure we showcase some of these mixing matrices. Generally these mixing matrices are much more disjunct. This means that given a book has a certain genre we can be confident that it is not contained in some communities, while we can be fairly certain it is from others. This is not true in all case - such as *poetry* showed below. In these cases no information about the community is gained from the genre.  
<img src="/images/business.png" width="800" />
<img src="/images/horror.png" width="800" /> 
<img src="/images/fantasy.png" width="800" /> 
<img src="/images/mystery.png" width="800" /> 
<img src="/images/poetry.png" width="800" /> 

The most informative genres are *busniness* and *horror* (view in the top of the above plot). Here nearly the entire genre is incapsulated in a community that does not contain much else. There are of course books from the gerne that are not in the community, especially noticable is the giant community (0) that has about a third of the dataset. <br>
The genres *fantasy* and *mystery* are both quite large and span many communities, however, either a community consists of the genre and not much else, or it does not contain it at all. This again express quite a lot of information, because you can be sure that you do not have a book from community 5 if the genres do not contain *fantasy*. <br> 
At last there are the genres that have absolutly no causality with the communities, here *poetry* is an example. 

# **Visualization of the Network**
Below we visualize the network with the netwulf library. In the first plot the colors correspond to Louvain communities, while the second plot shows the network colored by *top_genre*. The seperations into communities is very crisp in the community plot, but a lot more muddled in the *top_genre* plot. This corresponds well to our findings with the mixing matrices. 
<img src="/images/shelf_network_community.png" width="800" />
<img src="/images/shelf_network_top_genre.png" width="800" />

# **Word Clouds**
<img src="/images/shelf_wordcloud_0.png" width="500" />
<img src="/images/shelf_wordcloud_4.png" width="500" />
<img src="/images/shelf_wordcloud_32.png" width="500" />
Most of the communities do not have specific topic that are easy to distinguish, as examplified with our giant community 0, that has a lot of words about books. 
Community 4 clearly has contains comics (with words like batman, joker, robin, gotham, superman ect.). 
A funny coincidence for us was when we discovered community 32 is all danish. Granted, it only consists of two books, but we still found it a funny coincidence. 
