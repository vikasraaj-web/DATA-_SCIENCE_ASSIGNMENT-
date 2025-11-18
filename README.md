# Spectral Modularity for Community Detection

**DONE BY:**
* **VIKAS RAAJ V A**
* **ROLL NUMBER: IMS 24262**

---

## 📜 Project Summary

This project implements a community detection algorithm from scratch based on the principles of **spectral modularity maximization**. The core idea is to recursively partition a network into smaller and smaller communities, where each split is guided by the eigenvectors of the network's **modularity matrix**.

The algorithm stops splitting a community when doing so would no longer increase the network's overall modularity. This "stopping criterion" is elegantly determined by checking if the **leading eigenvalue** of the community's restricted modularity matrix is positive.

This implementation was built in a Jupyter Notebook and tracks the state of the network at each iteration, producing visualizations of both the community splits and the evolution of key node metrics.

## 🤖 How It Works: The Algorithm

The project executes the following steps:

1.  **Initialization**: The algorithm begins with the entire Karate Club graph treated as a single, large community.
2.  **Compute Modularity Matrix**: For a given community $C$, a **restricted modularity matrix** $B^{(C)}$ is computed. This matrix represents the difference between the *actual* number of edges within the community and the *expected* number of edges in a random null model.
3.  **Find Leading Eigenpair**: The algorithm finds the **leading eigenvalue ($\lambda_1$)** and its corresponding **eigenvector ($u_1$)** for the matrix $B^{(C)}$.
4.  **Eigenvalue Stopping Criterion**:
    * If **$\lambda_1 \le 0$**, the community is considered **indivisible**. Splitting it would not increase modularity, so the algorithm stops for this branch.
    * If **$\lambda_1 > 0$**, a split is beneficial.
5.  **Spectral Bisection**: The community is split into two new sub-communities based on the *sign* of the entries in the leading eigenvector $u_1$. All nodes with a positive entry form one group, and all nodes with a non-positive entry form the other.
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
