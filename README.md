# Introduction

The purpose of this repository is to help anyone who wishes to find the communities present in a given graph. This resource should streamline the implementation process as well as provide basic information about each graph clustering method. Since not all coding environments have implementations of each method, this repository will also provide packages and pre-written code for Python, R, and MATLAB when available.

# Defining the Problem

Let $G = (V, E)$ be a graph, where *V* is the set of vertices or nodes, and $E$ is the set of connections or edges such that $E \subset V \times V$. Below is a visualization of a famous graph known as Zachary's Karate Club, which contains 34 club members with each edge indicating whether a member interacted with another outside of the club. 

![Graph Example](images/karate_club.PNG)

Usually, this data will be given in what is known as an adjacency matrix. The adjacency matrix $A$ is an $n \times n$ matrix, where $n$ represents the number of nodes in the graph. Element $A$<sub>ij</sub> equals 1 if an edge exists between nodes $i$ and $j$, and 0 otherwise. For large graphs, using a sparse matrix will speed up the run time.

For graph clustering, also known as community detection, can be informally defined as trying to group nodes together, typically by maximizing the number of intra-edges while minimizing the number of inter-edges. Unfortunately, this problem is NP-hard, meaning that this problem doesn't (or possibly, can't) have a way of solving it quickly. Therefore, we have to implement algorithms that we hope give good approximations for the optimal solution.

# Clustering Algorithms

This repository contains code or direction to packages that run various different graph clustering algorithms, including:

* Label Propagation
* K-means
* Normalized Spectral Clustering (Ncut)
* Louvain
* Nonnegative Matrix Factorization Using Graph Random Walk (NMFR)

Now, we'll go over some basic information regarding each graph clustering method.

## Label Propagation

The basic idea behind the label propagation method is to assign each node to the cluster that is most prevelent amongst its neighbors. It was developed by Xiaojin Zhu and Zoubin Ghahramani in 2002 [1]. The basic algorithm can be described as follows:

1) Initialize the graph so each node has its own cluster.
2) Arrange all the nodes in the graph in a random order.
3) For each node in that order, assign it to the cluster that is most common amongst its neighbors. Ties are broken uniformly randomly.
4) If every node is in the cluster that the maximum number of their neighbors have, then stop the algorithm. Else, go to (2).

What is nice about the label propagation method is that it is easy to implement and quick to run. Label Propagation also does not require any prior knowledge to run, unlike some other methods to be discussed.

## K-means

Though it is usually applied to euclidean data, the k-means clustering method has adaptations to graphs. This is done by embedding the graph into another, low-dimensional space, then applying the typical k-means methodology [2]. The basic algorithm can be described as follows:

1) Embed the graph into a lower-dimensional space using any desired method.
2) Initialize $k$ centroids randomly, where $k$ is the number of clusters in the graph.
3) Assign each node to the nearest centroid in the newly embedded space.
4) Recalculate the positions of the centroids to be in the center of their associated nodes.
5) Repeat steps (3) and (4) until no changes are made.

Once the graph has been embedded into a lower-dimensional space where distance measures can be calculated, k-means is an easy-to-use method that only requires a preset number of clusters to calculate. However, determining the best method to embed the graph tends to be the tricky part. There are also other adaptations of k-means to graphs, such as the algorithms proposed by Sami Sieranoja & Pasi Fränti [3]. 

## Ncut

The normalized spectral clustering method relies on two things: the Laplacian matrix, which is a transformation of the adjacency matrix discussed earlier, and eigenvalues, which are special scalars associated with a given matrix. It will then use the k-means algorithm to cluster using the gathered eigenvalues, so in a sense ncut is a special case of k-means. The basic algorithm for ncut can be described as follows:

1) Compute the Laplacian matrix $L$.
2) Compute the normalized Laplacian matrix $L$<sub>norm</sub>.
3) Calculate the first $k$ eigenvectors $u_1, . . ., u_k$ of $L$<sub>norm</sub>, where $k$ is the number of clusters.
4) Let $U$ be the matrix containing $u_1, . . ., u_k$ as columns.
5) Form matrix $T$ by normalizing the rows of $U$ to norm 1.
6) For $i = 1, . . . , n$, let $y_i$ be the vector corresponding to the $i$-th row of $T$.
7) Cluster the points $(y_i)$<sub>i=1,...,n</sub> with the k-means algorithm into clusters $C_1, . . . , C_k$.

The Ncut method is a very powerful clustering tool that runs quickly and doesn't make strong assumptions on the formation of clusters [4]. 

## Louvain

The Louvain method is based on optimizing for $modularity$ [5]. Though there are a few different versions of $modularity$, the main principle is that for a graph to have a good modularity, there should be many edges within a given cluster, while the graph should be split up into many clusters with a small total amount of edges in each. The basic algorithm for the Louvain method can be described as follows:

1) Initialized each node to be in its own cluster.
2) Pick a node $u$ at random.
3) Remove $u$ from its cluster and compute the removal gain in $modularity$ $\Delta Q$.
4) For each cluster prevelent amongst $u$'s neighbors, calculate the add gain in $modularity$ $\Delta Q'$.
5) If the highest total gain is positive ($\Delta Q' - \Delta Q > 0$), then move the node to that cluster.
6) Repeat steps 2 - 5 for each node in the graph.

Much like the label propagation method, Louvain is easy to implement, quick to run, and doesn't require any prior information about the graphs. 

## NMFR

# References

[1] Xiaojin Zhu and Zoubin Ghahramani (2002), *Learning from labeled and unlabeled data with label propagation*, Technical Report CMU-CALD-02–107, Carnegie Mellon University

[2] Thomas Bonald, Nathan de Lara, Quentin Lutz, Bertrand Charpentier (2020), *Scikit-network: Graph Analysis in Python*. Journal of Machine Learning Research, http://jmlr.org/papers/v21/20-412.html

[3] Sieranoja, S., Fränti, P. (2022), *Adapting k-means for graph clustering*. Knowl Inf Syst 64, 115–142. https://doi.org/10.1007/s10115-021-01623-y

[4] Ulrike von Luxburg (2007), *A Tutorial on Spectral Clustering*, Max Planck Institute for Biological Cybernetics, Statistics and Computing, https://people.csail.mit.edu/dsontag/courses/ml14/notes/Luxburg07_tutorial_spectral_clustering.pdf

[5] Vincent D. Blondel, Jean-Loup Guillaume, Renaud Lambiotte, Etienne Lefebvre (2008) *Fast unfolding of communities in large networks*. Department of Mathematical Engineering, Universit́e catholique de Louvain, avenue Georges Lemaitre, B-1348 Louvain-la-Neuve, Belgium.
