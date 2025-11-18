# Spectral Modularity for Community Detection
### DSC212 — Assignment 1

**DONE BY:**
* **VIKAS RAAJ V A**
* **ROLL NUMBER: IMS 24262**

---

## Overview

This repository contains the solution to **Assignment 1** of the DSC212 course. The assignment involves implementing a community detection algorithm from scratch using spectral modularity optimization on the classic Zachary's Karate Club graph.

## Context: The Karate Club Story

In the early 1970s, **Wayne W. Zachary**, a graduate student in anthropology, conducted a study on social interactions within a university karate club.

Over two years, he observed **34 members**, recording their friendships and interactions—such as training together, attending events, and socializing outside class.

From these observations, Zachary constructed a **social network** where:
* Each member is a **node**
* An **edge** connects two members if they frequently interacted

This network, now known as the **Zachary’s Karate Club Graph**, has become one of the most iconic examples in network science.

## The Split

During Zachary’s research, a dispute arose between:
* The **instructor** (“Mr. Hi”)
* The **club administrator** (the club president)

The disagreement—over how to spend club funds—eventually **split the club into two factions**.

Zachary later observed that **friendship patterns** strongly predicted this division: members tended to follow their close friends.

## Research Question

Given the network **before** the split, can a **community detection algorithm** recover the same division purely from the graph structure?

This makes the Karate Club network a perfect “Hello World” of community detection—small, interpretable, and historically significant.

## How It Works: The Algorithm

The project executes the following steps, following the spectral method of modularity maximization:

1.  **Initialization**: The algorithm begins with the entire Karate Club graph treated as a single, large community.
2.  **Compute Modularity Matrix**: For a given community $C$, a **restricted modularity matrix** $B^{(C)}$ is computed. This matrix represents the difference between the *actual* number of edges within the community and the *expected* number of edges in a random null model.
3.  **Find Leading Eigenpair**: The algorithm finds the **leading eigenvalue ($\lambda_1$)** and its corresponding **eigenvector ($u_1$)** for the matrix $B^{(C)}$.
4.  **Eigenvalue Stopping Criterion**:
    * If **$\lambda_1 \le 0$**, the community is considered **indivisible**. Splitting it would not increase modularity, so the algorithm stops for this branch.
    * If **$\lambda_1 > 0$**, a split is beneficial.
5.  **Spectral Bisection**: The community is split into two new sub-communities based on the *sign* of the entries in the leading eigenvector $u_1$.
6.  **Recursion**: This entire process (steps 2-5) is then applied recursively to the two new sub-communities.
7.  **Metric Tracking**: At each iteration, key node metrics (Degree, Betweenness, Closeness, and Clustering) are calculated for the *entire* graph and stored.
8.  **Visualization**: The final output includes "colorful charts" that plot the graph at each iteration (coloring nodes by community) and the evolution of the node metrics over time.

## 🚀 How to Run

1.  Clone this repository to your local machine:
    ```bash
    git clone [https://github.com/](https://github.com/)[Your-Username]/[Your-Repo-Name].git
    ```
2.  Navigate to the project directory:
    ```bash
    cd [Your-Repo-Name]
    ```
3.  Ensure you have the required libraries installed (see list below). You can install them using pip:
    ```bash
    pip install numpy networkx matplotlib scipy
    ```
4.  Open the `your-notebook-name.ipynb` file in a Jupyter environment (like Jupyter Notebook, JupyterLab, Google Colab, or VS Code).
5.  Select "Kernel" > "Restart & Run All" (or the equivalent "Run All" button) to execute all cells from top to bottom.
6.  The notebook will run the algorithm, print the iteration-by-iteration progress, and display all visualizations inline.

## 📦 Libraries Used

This project relies on the following core scientific Python libraries:

* **NumPy**: For all numerical operations and matrix computations (like $B^{(C)}$).
* **NetworkX**: For loading, manipulating, and analyzing the Karate Club graph.
* **Matplotlib**: For generating all the static and "colourfull" charts and visualizations.
* **SciPy**: Used specifically for `scipy.linalg.eigh`, a highly optimized function for finding eigenvalues and eigenvectors of symmetric matrices.

## Conclusions

* The algorithm successfully identifies multiple communities by recursively splitting the graph based on the spectral properties of the modularity matrix.
* The initial splits closely align with the known historical division of the club into two factions, demonstrating the method's effectiveness.
* Per the assignment, node metrics (Degree, Betweenness, Closeness, and Clustering) are calculated on the **global graph `G`** at each iteration.
* Because the underlying graph `G` itself is not modified during the splitting process, these **global metric values remain constant** across all iterations.
* Nodes **0 ("Mr. Hi") and 33 (the administrator)** are consistently identified as central nodes in the network, reflecting their roles as leaders of the two factions.

## Key Takeaway

The Karate Club network elegantly demonstrates how **mathematical structures in graphs** (like the eigenvectors of the modularity matrix) can reveal the **social dynamics** and fault lines that shape real-world communities.
