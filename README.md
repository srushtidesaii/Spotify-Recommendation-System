# Spotify-Recommendation-System

Click [here](https://github.com/srushtidesaii/Spotify-Recommendation-System/blob/main/Spotify%20(4).ipynb) to check out the whole Jupyter Notebook for the implementation of Spotify Recommendation System using Machine Learning (Content Based Filtering) in Python. <br>
Generate recommendations for any one of the spotify playlists. The following parts will be covered:

## Data Expolaration/Preprocessing 

Download datasets here: https://www.kaggle.com/vatsalmavani/music-recommendation-system-using-spotify-dataset/data

## Feature Generation

* Conducting featuring engineering to process the data into a form (that is by generating One hot encoded feautures)that could be fed into the content-based filtering 
algorithm as well as the similarity measure used.

* One-hot encoding, a common technique to transform categorized data into machine-readable features. This is done by converting each category into a column so that 
each category can be represented as either True or False (that is 0 or 1) using pandas.get_dummies() function.

* The genres in Spotify are not balanced distributed with some genres more prevalent while others are more obscure. In addition, one artist or track could be 
associated with multiple genres. Hence, we need to weigh the importance of each genre to combat overweighing specific genres while underestimating others.
Therefore, TF-IDF measures are introduced and applied to the genre data. TF-IDF, also known as Term Frequency-Inverse Document Frequency, is a tool to quantify 
words in a set of documents. We are calculating the most prominent genre in each song and their prevalence across songs to determine the weight of the genre. 
This is much better than simply one-hot encoding since there are no weights to determine how important and widespread each genre is, leading to overweighting 
on uncommon genres. To implement this, we used the TfidfVectorizer() function from scikit learn.
 
* For popularity data, I used treated as a continuous variable and only normalizing it into a range between 0 and 1. The idea is songs that are popular are likely 
to be heard by people who like popular songs, while songs that are less popular are likely to be heard by people who have the same taste. This was done via the 
MinMaxScaler() function in scikit learn. 


## Content-based Filtering Recommendation

* Content-based filtering uses the features of each item to find the similarities items. By assigning a score to how similar each item is, we can recommend an item based
on how similar it is to all other items in the dataset.
In the context of Spotify playlists, we use the features (loudness, tempo, genre etc.) of each song in a playlist to find the average score of the whole playlist
( that is the Final playlist vector). Then, we recommend a song that has a score similar to the playlist but is not in the playlist. 

* After retrieving the playlist summarized vector and the non-playlist songs, we can find the similarity between each individual song in the database and the playlist.
The similarity metric chosen is cosine similarity. The comparison is done between the Final Playlist vector and each row of the feature set (complete_feature_set_nonplaylist)
which is considered to be a song.


## Recommendation for a specific playlist which is extracted from Spotipy API.

* Spotfiy API Acquisition 
For this we use various keys for authentication, and the send requests. The first is getting keys to use. For this, we need a 
(Spotify for developers:https://developer.spotify.com/) account. This is the same as a Spotify account, and doesn’t require Spotify Premium. 
From here, go to the dashboard and “create an app”. Now, we can access a public and private key, needed to use the API.

* Spotify Credentials Storage and Access (Useful links: https://spotipy.readthedocs.io/en/2.16.1/) 
Now that we have an app, we can get a client ID and a client secret for this app. Both of these will be required to authenticate with the Spotify web API for our
application, and can be thought of as a kind of username and password for the application. 





