---
title: Data Description
prev: "/"
next: shelf-network
---

# **Dataset**
We use datasets from two different sources, the first source is [1](#sources), which have created the [Goodreads Dataset](https://sites.google.com/eng.ucsd.edu/ucsdbookgraph/home) dataset. This is a collection of users Goodreads shelves, telling us which books they own. We use two datasets from this source, *Goodreads_books* and *goodreads_interactions*, which we will call *Book Shelves* and *Book Interactions* respectively. The former contains data about the 1.5 million books, while the latter contains 876,145 users shelves. <br>
Because this first source does not contain descriptions of the books, we found a second source, the [Goodbooks](https://github.com/malcolmosh/goodbooks-10k-extended/blob/master/README.md) dataset, that contains book descriptions of 10 thousind books. We call this dataset *Book Descriptions*.
### **Dataset Biases** 
Our sources have scraped their data from [Goodreads](https://www.goodreads.com/), but do not inform further about which users they scraped the data from. However, Goodreads have published their [demographic](https://www.goodreads.com/author_blog_posts/14538341-who-is-the-average-goodreads-user-you-ll-be-surprised), in which we see that the majority of users are American. We also see that it is mostly young adults that use this service, and that slightly more women use it than men. We then have a quite large bias towards western culture, but for our purposes it means that our results should be interpreted only for structure of western readers. 
<br>
Another thing to consider is how Goodreads brands themselves. Are books of a certain type cheaper? Are certain books unavailable? We have not been able to find any sources expressing these topics, which the reader should keep in mind. 

# **Data Statistics** 
As mentioned we combine datasets from the two sources [Goodreads Dataset](https://sites.google.com/eng.ucsd.edu/ucsdbookgraph/home) and [Goodbooks](https://github.com/malcolmosh/goodbooks-10k-extended/blob/master/README.md) to create a dataset that contains both which books consumers own, the descriptions of the books and the genres. Below is a small table explaining the size of the datasets.
|                 | *Book Shelves*  | *Book Interactions* | *Book Descriptions* |
|---              | ---             | ---                 |  ---                | 
| Data Points     |    1,521,962    |     228,648,342     |       10,000        | 
| Storage         |     714.3 MB    |        4.2 GB       |       9.9 MB        | 
| Attributes      |       16        |          2          |          4          | 
| Attributes Used |       2         |          2          |          3          |

The *goodreads_interactions* dataframe contains 228,648,342 interactions (books on shelves), which is collapsed to 876,145 shelves. 

# **Merge Datasets** 
To combine the dataframes we match titles from *Book Shelves* and from *Book Descriptions*. Before we do this we drop all faulty elements in both dataframes that do not have a title. This, surprisingly, removes half of the books in *Book Shelves*, and leaves only 646,906 books in the *Book Shelves*.<br>
Next, the titles are compared, however, this is not as easy as it sounds as the titles in *Book Descriptions* often have added information in the titles, such as, *The Hunger Games (The Hunger Games, #1)*. 
Here the *(The Hunger Games, #1)* is the problem because it is not in the titles of *Book Shelves*. We therefore strip everything that is inside a parenthesis away, and remove all non-character symbols such as - or ^. 
In *Book Shelves* and *Book Descriptions* we have 7,690 matches after removing duplicates. In this way we create a dataframe *Book_df* that contains the *id, title, description, genres* of these 7,690 books.<br>

Next, the *Book Interactions* that does not concern these 7,690 books are dropped. This leaves us with 68,176,467 interactions, 818,569 shelves and 7676 unique books (14 was not in *Book Interactions*). 

# **TF-IDF of Books and Genres**
TF-IDF values for words in a document that is part of a corpus are great for detecting which words are important for that specific document (what distinguishes the document). We will use the TF-IDF values for the books in various ways. We will build a network where books are nodes and edges are created if the two books inner product between their normalized TF-IDF values based on their descriptions is above a certain threshold. We will also use the TF-IDF values for communities in both our graphs to generate word clouds describing the the communities. Here each document is the combination of all descriptions of books in that community. 
<br>
We will frequently use the TF-IDF values of different partitions of the books, but in all cases the entire corpus will consists of the descriptions of all the books. We therefore compute these TF values for each book and store them - all other TF values for different partitions can be made by adding together the books TF values. 
<br>
The IDF values needs to be recalculated each time we partition our books into different groupings, as the amount of documents changes. 
<br>
In our raw dataset each book have multiple genres. Later in our analysis we want a books genre simplified to one simple class. We make a new document by including the all books from that genre, then we calculate the TF-IDF values for each genre like this. This genre TF-IDF is normalized, as are the books TF-IDF's and we assign the book that of its genres that it has the largest TF-IDF normalized inner product with. These genres are stored in the *Book_df* dataframe, as *top_genre*. 


# **Sources**
- Mengting Wan, Julian McAuley, "Item Recommendation on Monotonic Behavior Chains", in RecSys'18.
- Mengting Wan, Rishabh Misra, Ndapa Nakashole, Julian McAuley, "Fine-Grained Spoiler Detection from Large-Scale Review Corpora", in ACL'19.