# Parallel Ant Colony Optimization for Mountain Climbing Pathfinding

This project implements a **Parallel Ant Colony Optimization (ACO)** algorithm to find the shortest path for mountain climbing, based on the research paper titled *"Parallel Ant Colony Optimization Algorithm for Finding the Shortest Path for Mountain Climbing"* by Esra’a Alhenawi et al., published in IEEE Access (DOI: 10.1109/ACCESS.2022.3233835). The implementation includes both sequential and parallel versions of the ACO algorithm, optimized for navigating a 3D mountain terrain while avoiding obstacles.

## Project Overview

The project simulates a mountain terrain using a 3D surface defined by a mathematical function (`sin(sqrt(x^2 + y^2))`). Random points are generated on this surface to represent valid waypoints, with a subset designated as obstacles. The ACO algorithm is used to find the shortest path between a randomly selected start and end point, considering terrain slopes, distances, and pheromone trails. The parallel version leverages Python's `multiprocessing` module to distribute ant tasks across multiple CPU cores, improving performance.

### Key Features
- **Sequential ACO**: A standard implementation of the ACO algorithm for pathfinding.
- **Parallel ACO**: A parallelized version using Python's `multiprocessing.Pool` to speed up computation.
- **3D Visualization**: Uses Matplotlib to plot the mountain terrain, valid points, obstacles, and the optimal path.
- **Performance Comparison**: Measures and compares execution times of sequential and parallel implementations.
- **Obstacle Avoidance**: Incorporates obstacles in the terrain that the algorithm must navigate around.

## Prerequisites

To run this project, you need the following dependencies:
- Python 3.8 or higher
- Required Python packages:
  - `numpy`
  - `matplotlib`
  - (Optional) `plotly` and `jupyter-dash` for alternative visualizations (not used in the provided code)

You can install the required packages using pip:
```bash
pip install numpy matplotlib
```

## Project Structure

- **main.py**: The main script containing the implementation of both sequential and parallel ACO algorithms, terrain generation, and visualization logic.
- **README.md**: This file, providing an overview and instructions for the project.

## Usage

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/parallel-aco-mountain-climbing.git
   cd parallel-aco-mountain-climbing
   ```

2. **Run the Script**:
   Execute the main script to run both the sequential and parallel ACO algorithms and visualize the results:
   ```bash
   python main.py
   ```

3. **Output**:
   - The script will:
     - Generate a 3D mountain terrain with random points and obstacles.
     - Run the sequential ACO algorithm and display the best path and its length.
     - Run the parallel ACO algorithm and display the best path and its length.
     - Show execution times for both versions and calculate the speedup (sequential time / parallel time).
     - Display 3D plots for both algorithms, showing the terrain, points, obstacles, and the computed paths.

## Algorithm Details

### Sequential ACO
- **Input**: 3D terrain (`X`, `Y`, `Z`), valid points, obstacles, start/end indices, number of ants, iterations, and ACO parameters (`alpha`, `beta`, `evaporation_rate`, `Q`).
- **Process**:
  - Each ant constructs a path from the start to the end point, guided by pheromone levels and edge values (based on slope and distance).
  - Pheromone trails are updated after each iteration, with evaporation applied to prevent premature convergence.
  - The best path (shortest valid path) is tracked across iterations.
- **Output**: The best path (list of point indices) and its total length.

### Parallel ACO
- **Input**: Same as the sequential version.
- **Process**:
  - Uses `multiprocessing.Pool` to parallelize ant path construction across 4 CPU cores.
  - Each ant task runs independently, and results are collected to update pheromone trails.
  - Similar pheromone update and evaporation logic as the sequential version.
- **Output**: The best path and its length, typically computed faster than the sequential version.

### Parameters
- `n_ants = 5`: Number of ants per iteration.
- `n_iterations = 50`: Number of iterations for the algorithm.
- `alpha = 1`: Pheromone influence factor.
- `beta = 1`: Distance influence factor.
- `evaporation_rate = 0.5`: Rate at which pheromones evaporate.
- `Q = 1`: Pheromone deposit constant.

## Visualization
The project uses Matplotlib to create 3D plots:
- **Terrain**: A semi-transparent surface plot of the mountain.
- **Points**: Red dots for valid waypoints, black dots for obstacles.
- **Path**: Green lines connecting the best path points, with green and blue markers for start and end points, respectively.
- **Annotations**: Labels for start and end points.

## Example Output
```
Running Sequential ACO...
Best path: [12, 45, 78, 23, 99]
Path length: 15.2345
Sequential Execution Time: 2.3456 seconds

Running Parallel ACO...
Best path: [12, 46, 79, 24, 99]
Path length: 15.1234
Parallel Execution Time: 0.7890 seconds

Speedup (Sequential / Parallel): 2.97x
```
Two 3D plots will be displayed, one for each algorithm, showing the terrain and the computed paths.

## Research Paper Reference
This project is based on the following paper:
- **Title**: Parallel Ant Colony Optimization Algorithm for Finding the Shortest Path for Mountain Climbing
- **Authors**: Esra’a Alhenawi, Ruba Abu Khurma, Ahmad A. Sharieh, Omar Al-Adwan, Areej Al Shorman, Fatima Shannaq
- **Publication**: IEEE Access, 2022
- **DOI**: [10.1109/ACCESS.2022.3233835](https://ieeexplore.ieee.org/document/10004949)
- **Summary**: The paper proposes a parallel ACO algorithm for finding optimal paths in mountain climbing scenarios, accounting for terrain slopes and obstacles. This project implements the described algorithms and visualizes the results in a 3D environment.

## Limitations
- The parallel version assumes a fixed number of processes (4). Adjust based on your system's CPU cores for optimal performance.
- The random nature of ACO may lead to slightly different paths and lengths between runs.
- The terrain is a simplified mathematical function; real-world applications may require more complex terrain data.

## Future Improvements
- Add support for dynamic obstacle placement or real-world terrain data (e.g., from GIS datasets).
- Implement interactive visualizations using Plotly or Jupyter Dash (as hinted by the commented imports).
- Optimize the parallel implementation for larger datasets or distributed systems.
- Experiment with adaptive ACO parameters to improve convergence.

## Contributing
Contributions are welcome! Please fork the repository, create a new branch, and submit a pull request with your changes. Ensure that any modifications align with the research paper's methodology and include appropriate documentation.


## Contact
For questions or feedback, please open an issue on GitHub or contact the repository maintainer.

---
*This project was developed as a Python implementation of the parallel ACO algorithm described in the referenced IEEE paper, with a focus on clarity, reproducibility, and visualization.*
