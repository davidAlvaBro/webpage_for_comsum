---
title: Data Description
prev: "/"
next: shelf-network
---

# **Dataset** 
As mentioned earlier we use two datasets for our investigation. The first is the [Goodreads Dataset](https://sites.google.com/eng.ucsd.edu/ucsdbookgraph/home) dataset were [TODO CITE](#) have collected users Goodreads shelves (which books they own). We use the two datasets *Goodreads_books* and *goodreads_interactions*, which we will call *Book Shelves* and *Book Interactions* respectively. The former contains data about the 2.36 million books, while the later contains 876,145 users shelves. <br>
Because this first dataset does not contain descriptions of the books, we found the [Goodbooks](https://github.com/malcolmosh/goodbooks-10k-extended/blob/master/README.md) dataset, that contains book descriptions of 10 thousind books. We call this dataset *Book Descriptions*.<br>
<br>
[TODO considerations of biases](#)


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
To combine the dataframes we match titles from *Book Shelves* and from *Book Descriptions*. Before we do this we drop all faulty elements in both dataframes that do not have a title. This, suprisingly, contains half of the books in *Book Shelves*, and leaves only 646,906 books in the *Book Shelves*.<br>
Next, the titles are compared, however, this is not as easy as it sounds as the titles in *Book Descriptions* often have added information in the titles, such as, *The Hunger Games (The Hunger Games, #1)*. 
Here the *(The Hunger Games, #1)* is the problem because it is not in the titles of *Book Shelves*. We therefore strip everything that is inside a parentasis away, and remove all non-character symbols such as - or ^. 
In *Book Shelves* and *Book Descriptions* we have 7,690 matches after removing duplicates. In this way we create a dataframe *Book_df* that contains the *id, title, description, genres* of these 7,690 books.<br>

Next, the *Book Interactions* that does not concern these 7,690 books are dropped. This leaves us with 68,176,467 interactions, 818,569 shelves and 7676 unique books (14 was not in *Book Interactions*). 

# **TF-IDF of Books and Genres**
[TODO Write this]()