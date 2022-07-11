# Data Overview

This dataset consists of several million 5-star ratings obtained from users of the online MovieLens movie recommendation service. The MovieLens dataset has long been used by industry and academic researchers to improve the performance of explicitly-based recommender systems, and now you get to as well!

For this Predict, we'll be using a special version of the MovieLens dataset which has enriched with additional data, and resampled for fair evaluation purposes.

## Source
The data for the MovieLens dataset is maintained by the GroupLens research group in the Department of Computer Science and Engineering at the University of Minnesota. Additional movie content data was legally scraped from IMDB

## Supplied Files
genome_scores.csv - a score mapping the strength between movies and tag-related properties. Read more here
genome_tags.csv - user assigned tags for genome-related scores
imdb_data.csv - Additional movie metadata scraped from IMDB using the links.csv file.
links.csv - File providing a mapping between a MovieLens ID and associated IMDB and TMDB IDs.
sample_submission.csv - Sample of the submission format for the hackathon.
tags.csv - User assigned for the movies within the dataset.
test.csv - The test split of the dataset. Contains user and movie IDs with no rating data.
train.csv - The training split of the dataset. Contains user and movie IDs with associated rating data.

### Additional Information

The below information is provided directly from the MovieLens dataset description files:

#### Ratings Data File Structure (train.csv)

All ratings are contained in the file train.csv. Each line of this file after the header row represents one rating of one movie by one user, and has the following format:

```userId, movieId, rating, timestamp```
The lines within this file are ordered first by userId, then, within user, by movieId.

Ratings are made on a 5-star scale, with half-star increments (0.5 stars - 5.0 stars).

Timestamps represent seconds since midnight Coordinated Universal Time (UTC) of January 1, 1970.

#### Tags Data File Structure (tags.csv)

All tags are contained in the file tags.csv. Each line of this file after the header row represents one tag applied to one movie by one user, and has the following format:

```userId,movieId,tag,timestamp```
The lines within this file are ordered first by userId, then, within user, by movieId.

Tags are user-generated metadata about movies. Each tag is typically a single word or short phrase. The meaning, value, and purpose of a particular tag is determined by each user.

Timestamps represent seconds since midnight Coordinated Universal Time (UTC) of January 1, 1970

#### Movies Data File Structure (movies.csv)

Movie information is contained in the file movies.csv. Each line of this file after the header row represents one movie, and has the following format:

```movieId,title,genres```
Movie titles are entered manually or imported from https://www.themoviedb.org/, and include the year of release in parentheses. Errors and inconsistencies may exist in these titles.

Genres are a pipe-separated list, and are selected from the following:

- Action
- Adventure
- Animation
- Children's
- Comedy
- Crime
- Documentary
- Drama
- Fantasy
- Film-Noir
- Horror
- Musical
- Mystery
- Romance
- Sci-Fi
- Thriller
- War
- Western
- (no genres listed)
Links Data File Structure (links.csv)
Identifiers that can be used to link to other sources of movie data are contained in the file links.csv. Each line of this file after the header row represents one movie, and has the following format:

``` movieId, imdbId, tmdbId```

movieId is an identifier for movies used by [this link](https://movielens.org). E.g., the movie Toy Story has the link [this link](https://movielens.org/movies/1).

imdbId is an identifier for movies used by [this link](http://www.imdb.com). E.g., the movie Toy Story has the link [this link](http://www.imdb.com/title/tt0114709/).

tmdbId is an identifier for movies used by [this link](https://www.themoviedb.org). E.g., the movie Toy Story has the link [this link](https://www.themoviedb.org/movie/862).

Use of the resources listed above is subject to the terms of each provider.

#### Tag Genome (genome-scores.csv and genome-tags.csv)

As described in this article, the tag genome encodes how strongly movies exhibit particular properties represented by tags (atmospheric, thought-provoking, realistic, etc.). The tag genome was computed using a machine learning algorithm on user-contributed content including tags, ratings, and textual reviews.

The genome is split into two files. The file genome-scores.csv contains movie-tag relevance data in the following format:

```movieId,tagId,relevance```

The second file, genome-tags.csv, provides the tag descriptions for the tag IDs in the genome file, in the following format:

```tagId,tag```

## Acessing the data 

There are many platforms that support importing this sort of data there are three listed below firstly we look at the data in its raw form "the way it is represented on github" and then we can also have a look at it in Microsoft Excel this will most likely be the default display of the data if it is downloaded from github. For our purposes with the data we are going to use it predominantly in a jupyter notebook in python. The goal of this text is to give you a better understanding of how the text is represented across the different systems and thus enable the reader to be able to replicate the notebook and/or make your own improvements.

### Github Raw

The data looks like this in github:

#### Train Data Github Raw

<img src="https://github.com/Classification-Team-CW5/Classification-Data/blob/main/pictures%20of%20train%20set%20raw/github%20view%20of%20data.jpg?raw=true" alt="Github train data" title="Github train data"  /> 

#### Test Data Github Raw

<img src="https://github.com/Classification-Team-CW5/Classification-Data/blob/main/pictures%20of%20train%20set%20raw/github%20view%20of%20the%20test%20data%20.jpg?raw=true" alt="Github test data" title="Github test data"  /> 

### MS Excel
When you download the data Microsoft Excel will most likely be the default app for opening the data on your device the pictures below show how these files will be represented by Microsoft Excel upon opening them using that app. 
>Please also note that there are a lot more rows in the files than the fourteen that are represented in the images below 

Excel it has the following representation:

#### Train Data MS Excel

<img src="https://github.com/Classification-Team-CW5/Classification-Data/blob/main/pictures%20of%20train%20set%20raw/Train%20excel.jpg?raw=true" alt="Excel train data" title="Excel train data"  /> 

#### Test Data MS Excel

<img src="https://github.com/Classification-Team-CW5/Classification-Data/blob/main/pictures%20of%20train%20set%20raw/Train%20excel.jpg?raw=true" alt="Excel test data" title="Excel test data" /> 

### Pandas Representation

We want to use this data in a way where we can make changes and alter it without changing the source data unlike in excel where the data is both stored locally and any saved change made alters the local source file. We would like to be able to call on the data and make our changes in the notebook there is no intent to save the data only the insights and predictions that can be made from it. For this we need to have on demand access to the data as multiple people will be working on one notebook from different machines and not make any alterations to the source file, thus pandas seems like the best choice for the task.

#### Setting up
 
 if pandas is not present on your jupyter notebook it can be installed with the following codes:
 ```python:
 # Install from PyPI
 pip install pandas
 ```
 
 ```python:
 #conda installation
 conda install pandas
 ```
You can read more about installing pandas [here](https://pandas.pydata.org/docs/getting_started/install.html).
 
 When you first startup your jupyter notebook please ensure that pandas is imported into your current notebook for importing pandas we use the following code:
 
 ```python:
 import pandas as pd
 ```
 in the code above we use the alias `pd` for pandas which is the standard in python coding.
 
We import this data into our juypiter notebook found here using the following code :
```python:
# Load train and test datasets
train = pd.read_csv("https://raw.githubusercontent.com/Classification-Team-CW5/Classification-Data/main/train.csv")
test = pd.read_csv("https://raw.githubusercontent.com/Classification-Team-CW5/Classification-Data/main/test_with_no_labels.csv")

```
In the code above the test data has been saved as pandas dataframes with the variables `test` and `train` respectively 

This data can be seen using the `.head()` function on a pandas data frame which by default displays the first five rows of the data by default :

#### Train Data in pandas

<img src="https://github.com/Classification-Team-CW5/Classification-Data/blob/main/pictures%20of%20train%20set%20raw/pandas%20view%20of%20the%20train%20data%20.jpg?raw=true" alt="Pandas train data" title="Pandas train data"  /> 

#### Test Data in pandas

<img src="https://github.com/Classification-Team-CW5/Classification-Data/blob/main/pictures%20of%20train%20set%20raw/pandas%20view%20of%20the%20test%20data%20.jpg?raw=true" alt="Pandas test data" title="Pandas test data" /> 

>Notice how due to the way the data has been imported an index has automatically been generated as highlighted in yellow on both the test and the train dataframes. 

The `test` data has two columns and the `train` data has three columns the `sentiment` column being the one that is present in the train data and not in the test data 

## Quick Overview of the data 

The data above has the following properties:

#### Train data:

- [The train data](https://raw.githubusercontent.com/Classification-Team-CW5/Classification-Data/main/train.csv) has three columns when imported in pandas namingly `sentiment`, `message` and `tweetid` please refer [here](https://github.com/Classification-Team-CW5/Classification-Data/blob/main/README.md#variable-definitions) for more detail on what these headings represent
-The train data consists of 15819 rows if working in pandas you can see this by using `.info()` function on the data 

#### Test data 
- [The test data](https://raw.githubusercontent.com/Classification-Team-CW5/Classification-Data/main/test_with_no_labels.csv) has two columns `message` and `tweetid` it does not contain a `sentiment` column as it is intended that you use the train data to make a model that will predict the `sentiment`
- The test data contains 10547 rows if working in pandas you can see this by using the `.info()` function on the data

[Back to the top](https://github.com/Classification-Team-CW5/Classification-Data#classification-data)

