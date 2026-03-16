# AI Delivery Route Optimization

**Primary Contribution:** Implementation of the A* search algorithm for delivery route optimization.

This project explores how different optimization algorithms perform on a real-world inspired logistics routing problem modeled as the **Traveling Salesman Problem (TSP)**.

The objective is to compute the shortest delivery route that visits multiple addresses and returns to the warehouse while minimizing total travel distance.

The project compares several algorithmic approaches and evaluates their performance against **Google OR-Tools**, an industry-grade optimization framework.

---

## Results

| Method | Total Route Distance |
|------|------|
| Random Sampling (Baseline) | ~5081 km |
| Nearest Neighbor | ~952 km |
| Simulated Annealing | ~1602 km |
| A* Search | ~834 km |
| Google OR-Tools (Benchmark) | ~692 km |

All optimization algorithms significantly outperform random search. The A* implementation produced the **best-performing route among the algorithms implemented in this project**, achieving a total route distance of approximately **834 km**. The result approaches the optimized benchmark produced by Google OR-Tools (~692 km).

---

## Overview

Efficient delivery routing is critical for logistics companies such as Amazon, UPS, and FedEx. Delivery drivers often need to visit hundreds of addresses in a single shift. Without optimized route planning, drivers may revisit the same areas multiple times, increasing travel time, fuel consumption, and operational cost.

This project models a simplified delivery routing problem:

- A single warehouse
- 200 delivery locations
- Each location must be visited exactly once
- The route must return to the warehouse
- Total driving distance should be minimized

The problem is formulated as the **Traveling Salesman Problem (TSP)**.

---

## Dataset

The dataset is constructed using real geographic data from Orange County, California.

**Warehouse Location**  
2006 McGaw Ave, Irvine, CA

**Delivery Locations**  
200 randomly sampled addresses from the Orange County Public Works Address Dataset.

**Distance Calculation**  
A **201 × 201 driving distance matrix** was generated using the **Google Distance Matrix API**, representing real driving distances between each location.

---

## Algorithms Implemented

### Random Sampling (Baseline)

To establish a benchmark, the system generates **10,000 random delivery routes** and selects the shortest route found.

Because this approach does not consider any structure or heuristic, the resulting routes contain many inefficient overlaps. However, it provides a useful baseline for evaluating optimization algorithms.

---

### Nearest Neighbor Algorithm

The Nearest Neighbor algorithm is a **greedy search algorithm**.

At each step, the algorithm selects the unvisited location closest to the current location using Euclidean distance.

**Characteristics**

- Simple and fast
- Time complexity: `O(n²)`
- Produces locally optimal decisions

However, it cannot revise earlier decisions, which may lead to suboptimal global routes.

---

### Simulated Annealing

Simulated Annealing is a **probabilistic optimization algorithm** inspired by the physical annealing process in metallurgy.

The algorithm starts with a random route and iteratively improves it by swapping two randomly selected locations.

**Key properties**

- Can escape local minima
- Uses a temperature parameter to gradually reduce randomness
- Explores a wider solution space compared to greedy algorithms

---

### A* Search Algorithm

The **A\*** search algorithm evaluates nodes using the function:

```
f(n) = g(n) + h(n)
```

Where:

- `g(n)` = actual cost to reach the node  
- `h(n)` = heuristic estimate of remaining cost

In this implementation:

- `g(n)` is derived from the **driving distance matrix**
- `h(n)` uses **geodesic distance as a heuristic**

Because the heuristic is admissible, A* guarantees an optimal solution within the explored search space.

---

### Google OR-Tools Optimization (Benchmark)

To compare our results against an industry-grade solution, we used **Google OR-Tools**, a widely used optimization framework.

OR-Tools applies advanced optimization methods such as:

- Constraint Programming
- Mixed Integer Programming

This provides a strong benchmark for evaluating algorithm performance.

---

## Example Route Visualizations

*(Insert route visualization images here)*

Example image filenames:

- `images/random_route.png`
- `images/nearest_neighbor_route.png`
- `images/simulated_annealing_route.png`
- `images/a_star_route.png`

Visualizing routes highlights how different algorithms structure delivery paths and reduce route overlap.

---

## Technologies Used

- Python  
- NumPy  
- Matplotlib  
- Google Distance Matrix API  
- Google OR-Tools  

---

## Repository Structure

```
ai-delivery-route-optimization
│
├── data/
│   └── address_dataset.csv
│
├── algorithms/
│   ├── nearest_neighbor.py
│   ├── simulated_annealing.py
│   └── a_star_search.py
│
├── visualization/
│   └── route_plots.py
│
└── main.py
```

---

## My Contributions

My primary contribution to this project was the implementation of the **A\* search algorithm** used for delivery route optimization.

Specifically, I:

- Implemented the **A\* search algorithm** for solving the route optimization problem
- Constructed the algorithm's evaluation function using the formulation `f(n) = g(n) + h(n)`
- Used the **driving distance matrix** as the true cost `g(n)`
- Implemented a **geodesic distance heuristic** as `h(n)` to guide the search efficiently
- Built the **priority queue search structure** used to expand the most promising nodes first
- Developed the iterative process that applies A\* repeatedly to construct the complete delivery route
- Evaluated the performance of the A\* solution against other algorithms and the Google OR-Tools benchmark

The A\* implementation produced the **best-performing route among the algorithms implemented in the project**, achieving a total route distance of approximately **834 km**.

## Future Improvements

Potential future extensions include:

- Incorporating real-time traffic data
- Scaling the system to larger geographic areas
- Testing additional metaheuristic algorithms
- Multi-vehicle routing optimization
- Time-window constraints for delivery scheduling

---

## Authors

- Danny Suradja  
- Hyun Woo (Harry) Choi  
- Kenny Gao
