# Custom-Spotify-Playlist-Generator
This repository contains code to generate customized Spotify playlists tailored to the user's track library. 

The code utilizes the Spotify API and K-Medoids clustering to identify clusters of similar songs in a user's track library and generates a unique playlist for each cluster present in the library. This process if fully automated requiring the user to only input which Spotify account they want to use, a desired level of track popularity they wish to filter the final playlists, and a distance filter which filters the final playlist on similarity to the cluster center.

In order to access the API (and run the code) you need to register you Spotify account as a developer. This is free and takes only a few minutes. The link with instructions can be found here: https://developer.spotify.com/documentation/web-api/quick-start/ (you only need to do everything before the Preparing your Environment section). Once you have set up your developer account and registered your application, you need to go to the developer dashboard, click on your application, click on edit settings, and enter the URI: http://localhost:8888/callback in the Redirect URIs section. Now you can run the code and create customized playlist.

The general methodology is as follows:
1. Pull in the tracks in a user’s Spotify library and their associated audio features

2. Partition the tracks into clusters using K-Medoids clustering
    
    a. The optimal ‘K’ number of clusters is automatically selected from the range of 2-10 by taking the K that produces the highest            average Silhouette Score
    
    b. The clustering is re-run using the optimal K number of clusters
    
    c. The closest 3 songs to each cluster medoid are returned to help explain the clusters

3. Identify tracks that are similar to each cluster and not already in the user’s library
    
    a. All relevant artists are pulled for each artist in each cluster
    
    b. The top 10 tracks and their audio features for each new artist are found
    
    c. The list of new tracks are filtered to only include those that are within a specified Euclidean distance of the medoid of the            cluster they are associated with
    
    d. The list of new tracks are filtered to only include those that meet a specified popularity score

4. Upload the Playlists to Spotify
    
    a. Create a new playlist for each cluster
    
    b. Add the tracks to the appropriate playlist
