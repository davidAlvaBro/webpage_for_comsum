---
title: Text analysis
prev: network-analysis
---


## Math formula
$$ x^n + y^n = z^n $$

## Code chunk

```
import pandas as pd

df = pd.DataFrame()
```

> Nulla in justo hendrerit, tincidunt mauris et, porta est. Donec in leo vitae est ultrices dapibus id nec tortor. Maecenas ut ipsum eu nisl cursus facilisis scelerisque eu ex. Aliquam euismod elementum libero, at vehicula ipsum.

<img src="/images/dtu-logo.png" width="200" /> 
![](/images/dtu-logo.png)
![](https://source.unsplash.com/random/?Copenhagen)

1. Lorem ipsum dolor sit amet
1. Lorem ipsum dolor sit amet
1. Lorem ipsum dolor sit amet




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
    - Match titles of books -> ye? 
    - Clean dataset from duplicates and the likes -> yes? 

## Preprocessing II - Generate networks 
- Shelves network -> yes? 
    - Choice of weighting of edges -> yes?
    - Chose threshhold -> yes? 
    - Use NetworkX to create network -> bit more here 
- TL-IDF 
    - Generate TL-IDF scores for each book
    - And for each Genre 
    - Chose top genre for each book with TF-IDF 
    - Make edges with TF-IDF inner products (normalized)
    - Generate network to have as many edges as the shelves one 

## Network Analysis 
- Communities 
    - Louvain to create networks -> yes but many todo's
    - Check modularity to know if we form communities -> Written but needs to be made
    - Compare communities from the networks, and the genres
        - Create confusion matrices (do they find the same?)

- Assortativity -> Needs to be made and written 
    - Assortativity between genres 
    - Assortativity for degree? 

## NLP Analysis 
- Create word clouds for communities 

## Conclusion 
- Shelves better decides genre in communities