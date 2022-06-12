Repository for Improvement of Girvan Newman community detection algorithm<a name="TOP"></a>
===================

- - - - 

# About the algorithm #


Girvan Newman is a community detection algorithm that focuses on edge betweenness. Edges that have high betweenness in the graph are most likely to be an inter-community edge that connects communities in the graph. The algorithm computes betweenness for all edges in the graph and removes the edge with the highest betweenness, thus separating a community from the rest of the graph. The main issue of the algorithm is its high execution time. It has a time complexity of O(m2n) which is very expensive for community detection. Thus, we proposed two ideas to reduce the execution time of the algorithm while not losing much quality:
  1. The algorithm computes edge betweenness in each loop which is a very expensive move so we could remove multiple edges with one calculation from the top of the edge betweenness list.
  2. We don't need an exact value of edge betweenness but we need which edges have the highest one so we could use betweenness approximating algorithms instead of calculating it. We used Matteo Riondato et al. (2016) "Fast approximation of betweenness centrality through sampling" algorithm for the betweenness approximation.

We implemented these two approaches and measured their execution time along with quality.

# Advantages and disadvantages of the improved algorithm and further possible improvements #

1. GNM is the implementation of a multiple edge removal proposal and in our implementation, the number of one-time removal edges is r = square root(number of nodes). It certainly reduces the execution time by r but it's still inadequate and expensive computation as the main issue is in the betweenness computation execution time.
2. GNCquick is the implementation that covers both ideas and improves GNM. Instead of the exact calculation of betweenness, we used the BC approximation algorithm which we mentioned above. Though the improved algorithm's time complexity became much more optimal, the quality was the main issue. GNCquick does not check if the separating community has a decent size or not so it can detect a node as a whole community because it was connected to multiple edges with high BC. Also, the original Girvan Newman method does not tell the user how many communities are there but it divides the graph into a given number. However, GNCquick is not guaranteed that it would divide the graph into exact numbers of communities because it does not check if the graph is separated or not after removing an edge from the graph but checks if the graph is separated or not after removing multiple edges.
3. GNC resolved the issues in the GNCquick by checking the separating community if it has decent size (square root of node number) or not and if the community does not qualify the requirement it adds the edge back and proceeds with the edge BC list. Also, it makes sure that the graph is not separated while removing edges. The time complexity of the GNC is a bit slower than GNCquick but it's still in optimal range while maintaining much higher quality than GNCquick.

Further possible improvements:
We noticed that some inter-community edges' BC would be lower because many inter-community edges connecting one community to another may exist. Thus, the BC approximation algorithm may not return a hundred percent desirable output to the user and if we use the second proposed algorithm in the same paper we mentioned that approximates top-k BC, the algorithm may return an even more accurate output.

# File structure #

All implementations are in Python language and they're located in the implementation folder. We chose Jupyter Notebook as our environment due to its flexibility and advantages for testing and experimenting. Data used for the implementations are in the data folder.

# About dataset #
All data is from:
 https://snap.stanford.edu/data/index.html
 https://networkrepository.com/

# How to use #
1. It's not necessary to use a notebook to use the algorithm but it's recommended
2. Install the following packages (copy the command below and execute it on the terminal of the environment you are using):
  ```
  pip install networkx numpy networkit matplotlib
  ```
3. Change the path of the implementation to your local path of the data file.
4. Execute the implementations








