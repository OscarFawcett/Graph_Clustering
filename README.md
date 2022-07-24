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
* Kmeans
* Ncut
* Louvain
* Nonnegative Matrix Factorization Using Graph Random Walk (NMFR)

Now, we'll go over some basic information regarding each graph clustering method.

## Label Propagation

The basic idea behind the label propagation method is to assign each node to the cluster that is most prevelent amongst its neighbors. It was developed by Xiaojin Zhu and Zoubin Ghahramani in 2002 [1]. The basic algorithm can be described as follows:
1) Initialize the graph so each node has its own cluster.
2) Arrange all the nodes in the graph in a random order.
3) For each node in that order, assign it to the cluster that is most common amongst its neighbors. Ties are broken uniformly randomly.
4) If every node is in the cluster that the maximum number of their neighbors have, then stop the algorithm. Else, go to (2).

## Kmeans

## Ncut

## Louvain

## NMFR

# References

[1] Xiaojin Zhu and Zoubin Ghahramani, Learning from labeled and unlabeled data with label propagation (2002), Technical Report CMU-CALD-02–107, Carnegie Mellon University
