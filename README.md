Repository for Improvement of Girvan Newman community detection algorithm<a name="TOP"></a>
===================

- - - - 

# About the algorithm #


Girvan Newman is community detection algorithm that focuses on edge betweenness. Edges that have high betweenness in the graph is most likely to be a inter-community edge which connects communities in the graph. The algorithm computes  betweenness for all edges in the graph and removes the edge with the highest betweenness ,thus separating a community from the rest of the graph. The main issue of the algorithm is that its high execution time. It has time complexity of O(m2n) which is very expensive for community detection. Thus, we proposed two ideas to reduce execution time of the algorithm while not losing much quality:
  1. The algorithm computes edge betweenness in each loop which is very expensive move so we could remove multiple edges with one calculation from the top of the edge betweenness list.
  2. We don't need an exact value of edge betweenness but we need which edges have the highest one so we could use betweenness approximating algorithms instead of calculating it. We used Matteo Riondato et al. (2016) "Fast approximation of betweenness centrality through sampling" algorithm for the betweenness approximation.

We implmented these two approaches and measured its execution time along with quality.

# Advantages and disadvantages of the improved algorithm and further possible improvements #

1. GNM is the implementation of multiple edge removal proposal and in our implementation the number of one-time removal edge is r = square root(number of nodes). It certainly reduces the execution time by r but it's still inadequate and expensive computation as the main issue is in betweenness computation's execution time.
2. GNCquick is the implementation that covers our both ideas and improving GNM. Instead of exact calculation of betweennes, we used the BC approximation algorithm which we mentioned above. Though the improved algorithm's time complexity became much more optimal, the quality was the main issue. GNCquick does not check if the separating community has decent size or not so it can detect a node as a whole community because it was connected to multiple edges with high BC. Also, original Girvan Newman method does not tell the user how many communities are there but it divides the graph into given number. However, GNCquick is not guaranteed that it would divide the graph into exact number that user because it does not check if the graph is separated or not after removing an edge from the graph but checks if the graph is separated or not after removing multiple edges.


# File structure #

All implementations are in Python language and they're located in the implementation folder. We chose Jupyter Notebook as our environment due to its flexibility and advantages with testing and experimenting. Data used for the implementations are in the data folder.









