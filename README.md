# 🟡 Pacman Search AI (UC Berkeley CS188 – Project 1)

Implementation of classical **search algorithms** for the UC Berkeley **Pacman AI Project 1**.  
The Pacman agent finds paths through mazes — to reach a goal, visit all corners, or collect all food efficiently.

> ✅ Completed Tasks **Q1–Q8**: DFS, BFS, UCS, A\*, CornersProblem + heuristic, FoodSearchProblem + heuristic, ClosestDot.

---

## ✨ Features

- **DFS / BFS / UCS / A\*** — full graph search implementations (avoiding revisited states).
- **CornersProblem** — state `(position, visited_corners)`; expands valid successors with cost 1.
- **cornersHeuristic** — consistent, admissible heuristic using the max Manhattan distance to any unvisited corner.
- **FoodSearchProblem** — state `(position, foodGrid)`; collects all remaining dots.
- **foodHeuristic** — consistent heuristic based on the maze distance to the farthest remaining food.
- **ClosestDotSearchAgent** — greedy BFS-based agent that goes to the nearest food until none remain.

---

## 📂 Project Structure

├── search.py # DFS, BFS, UCS, A\*  
├── searchAgents.py # CornersProblem + heuristic, FoodSearchProblem + heuristic, ClosestDot  
├── util.py # Stack, Queue, PriorityQueue  
├── pacman.py # Runs the Pacman game  
├── layouts/ # Maze layouts  
├── test_cases/ # Autograder tests  
└── autograder.py # Autograder runner

---

## 🚀 Quick Start

```bash
# 1) Run the game
python pacman.py

# 2) Example commands
python pacman.py -l tinyMaze -p SearchAgent -a fn=dfs
python pacman.py -l mediumMaze -p SearchAgent -a fn=bfs
python pacman.py -l mediumMaze -p SearchAgent -a fn=ucs
python pacman.py -l bigMaze -p SearchAgent -a fn=astar,heuristic=manhattanHeuristic -z 0.5
```

---

## ✅ Autograder

Run all or a specific question:

```bash
python autograder.py
python autograder.py -q q1
python autograder.py -q q2
python autograder.py -q q3
python autograder.py -q q4
python autograder.py -q q5
python autograder.py -q q6
python autograder.py -q q7
python autograder.py -q q8
```

Useful flags:

- --graphics / --no-graphics

- -t test_cases/q7/food_heuristic_1

---

## 🧠 Implemented Logic Summary

### Q1–Q4: Core Search Algorithms

- DFS – uses Stack, marks visited after popping; returns action list.

- BFS – uses Queue, marks visited upon enqueue (guarantees shortest path in steps).

- UCS (Dijkstra) – uses PriorityQueue ordered by path cost g(n).

- A\* – PriorityQueue with priority f(n) = g(n) + h(n); optimal with consistent heuristic.

### Q5: CornersProblem

- State: ( (x, y), visited_corners_tuple[4] )

- Goal: all corners visited.

- Successors: four legal directions, cost = 1.

### Q6: Corners Heuristic

- Heuristic: max(Manhattan(current_position, unvisited_corner))

- Always admissible and consistent (triangle inequality).

### Q7: FoodSearchProblem

- State: (position, foodGrid)

- Heuristic: maze distance to the farthest remaining food, cached via problem.heuristicInfo.

### Q8: ClosestDotSearchAgent

- Goal test: self.food[x][y]

- Search: BFS (search.bfs(AnyFoodSearchProblem(gameState))).

---

## 🧪 Common Commands per Task

```bash
# Q1 – DFS
python pacman.py -l tinyMaze -p SearchAgent -a fn=dfs
python autograder.py -q q1

# Q2 – BFS
python pacman.py -l mediumMaze -p SearchAgent -a fn=bfs
python autograder.py -q q2

# Q3 – UCS
python pacman.py -l mediumMaze -p SearchAgent -a fn=ucs
python pacman.py -l mediumDottedMaze -p StayEastSearchAgent
python pacman.py -l mediumScaryMaze -p StayWestSearchAgent
python autograder.py -q q3

# Q4 – A\*
python pacman.py -l bigMaze -p SearchAgent -a fn=astar,heuristic=manhattanHeuristic -z 0.5
python autograder.py -q q4

# Q5/Q6 – Corners
python pacman.py -l tinyCorners -p SearchAgent -a fn=bfs,prob=CornersProblem
python pacman.py -l mediumCorners -p AStarCornersAgent -z 0.5
python autograder.py -q q5
python autograder.py -q q6

# Q7 – Food
python pacman.py -l testSearch -p AStarFoodSearchAgent
python pacman.py -l trickySearch -p AStarFoodSearchAgent -z 0.5
python autograder.py -q q7

# Q8 – ClosestDot
python pacman.py -l bigSearch -p ClosestDotSearchAgent -z 0.5
python autograder.py -q q8
```

---

## 🧩 Requirements

- Python 3.12+

- No external dependencies for algorithmic components (uses built-in Berkeley project files).

---

## 🏷 License & Attribution

This project builds on the official UC Berkeley CS188 Pacman Projects.
All original license and attribution notices remain intact in code headers.
Please do not publish or distribute full solutions for academic integrity reasons.

- Original authors: John DeNero, Dan Klein, and the CS188 team

- Modifications / implementations: Your Name Here

---

## 💡 Notes for Instructors

All implemented functions follow the graph-search paradigm (not tree search),
use the provided data structures (util.py), maintain minimal state representations,
and pass all autograder tests Q1–Q8.
