# assignmentdsc212
*created by Nandhana S------IMS24154*
Spectral Modularity Partitioning for Community Detection
Overview
This project implements a recursive spectral modularity partitioning algorithm for community detection in networks. The implementation is applied to the famous Zachary's Karate Club graph, demonstrating how modularity optimization can reveal the natural community structure in social networks.

Background
The Karate Club Story
In the early 1970s, Wayne W. Zachary studied social interactions among 34 members of a university karate club. He recorded friendship networks, creating what is now known as the Karate Club graph. During his study, the club split into two factions due to a conflict between the instructor ("Mr. Hi") and the club president. This dataset serves as a perfect case study for community detection algorithms.

Modularity Concept
Modularity is a quality function that compares the observed number of within-community edges against a random baseline. It measures whether a division is statistically surprising compared to chance, making it one of the most widely used measures for community detection.

Mathematical Foundation
Modularity Matrix
The modularity matrix B is defined as:

B = A - (𝐤𝐤ᵀ)/(2m)

Where:

A is the adjacency matrix

k is the degree vector

m is the total number of edges

Spectral Partitioning
The algorithm uses spectral methods to maximize modularity:

Relaxation: Instead of discrete ±1 assignments, we allow continuous values

Eigenvector Solution: The leading eigenvector of the modularity matrix provides the optimal continuous solution

Thresholding: Convert continuous values back to discrete community assignments

Recursive Bisection
The algorithm extends to multiple communities through recursive splitting:

Start with all nodes in one community

Compute the modularity matrix for the current community

Find the leading eigenpair (λ₁, u₁)

If λ₁ > 0, split the community by the sign of u₁

Recursively apply to each new community

Stop when no community can be split (λ₁ ≤ 0)

Implementation Features
Core Algorithm
Spectral modularity maximization

Recursive bipartitioning

Eigenvalue-based stopping criterion

Real symmetric matrix operations

Network Analysis Metrics
Degree Centrality: Measures direct connections

Betweenness Centrality: Identifies bridge nodes

Closeness Centrality: Measures reachability

Clustering Coefficient: Quantifies local connectivity

Visualization
Interactive community evolution plots

Network visualization with community coloring

Metrics evolution across iterations

Community size distribution

Installation & Requirements
bash
pip install networkx matplotlib numpy
Required Libraries
networkx: Graph operations and metrics

numpy: Linear algebra and matrix operations

matplotlib: Visualization and plotting

Usage
python
# Load the Karate Club graph
G = nx.karate_club_graph()

# Initialize and run analysis
analyzer = SpectralModularityPartitioning(G)
analyzer.run_analysis(max_iterations=6)

# Generate visualizations
analyzer.plot_metrics_evolution()
analyzer.analyze_central_nodes()
Code Structure
Main Class: SpectralModularityPartitioning
Key Methods:
compute_modularity_matrix(): Computes modularity matrix for node subsets

spectral_split(): Performs spectral bipartitioning

run_analysis(): Main analysis pipeline

visualize_communities(): Creates network visualizations

plot_metrics_evolution(): Tracks metric changes across iterations

Key Attributes:
communities_history: Stores community evolution

metrics_history: Tracks network metrics

partition_history: Records community assignments

Algorithm Parameters
Conservative Splitting Criteria
Minimum community size: 3 nodes

Eigenvalue threshold: λ > 0.1 required for splitting

Minimum split size: Communities must split into groups of at least 3 nodes

Maximum iterations: 6 (prevents over-splitting)

Expected Results
Final communities: 3-5 meaningful groups

Modularity: Optimized community structure

Interpretability: Socially meaningful partitions

Output Interpretation
Community Structure
The algorithm typically identifies:

Mr. Hi's core group (nodes 0, 1, 2, 3, etc.)

President's core group (nodes 33, 23, 24, etc.)

Intermediate/bridge communities (nodes connecting the factions)

Centrality Analysis
Key findings usually include:

Node 0 (Mr. Hi): Highest degree centrality

Node 33 (President): High betweenness centrality

Bridge nodes: High betweenness, connecting communities

Mathematical Proofs Included
The implementation is backed by formal mathematical proofs:

Proposition 1: Reality and symmetry of modularity matrix

Theorem 1: Real eigenvalues and orthonormal eigenbasis

Proposition 2: All-ones vector as eigenvector with eigenvalue 0

Theorem 2: Rayleigh-Ritz characterization

Theorem 3: Eigenvalue stopping criterion

Applications
This implementation demonstrates:

Social network analysis

Community detection in complex networks

Spectral graph theory applications

Modularity optimization techniques

Recursive algorithm design

References
Newman, M. E. J. (2006). "Modularity and community structure in networks", PNAS 103(23):8577-8582

Zachary, W. W. (1977). "An information flow model for conflict and fission in small groups"

Von Luxburg, U. (2007). "A tutorial on spectral clustering"
