# Pacman Search Project

**Course:** CAI 4002 — University of South Florida  
**Student:** Syed Abdullah M J Shah (U25670034)

---

## Overview

This project implements general-purpose search algorithms and applies them to Pacman navigation problems. The goal is for Pacman to find paths through mazes efficiently — reaching a target location, visiting all corners, or collecting all food.

---

## Files Modified

### search.py
Implements four search algorithms:

- **DFS** — Depth-first search using a LIFO stack. Explores deepest nodes first. Not guaranteed to find the shortest path.
- **BFS** — Breadth-first search using a FIFO queue. Guarantees the fewest-actions path.
- **UCS** — Uniform-cost search using a priority queue keyed by total path cost. Guarantees the least-cost path.
- **A\*** — A* search using a priority queue keyed by `g(n) + h(n)`, where `g` is the path cost and `h` is a heuristic estimate. Guarantees optimal path when the heuristic is consistent.

All four algorithms use graph search (visited state tracking) to avoid re-expanding already-seen states.

### searchAgents.py
Implements search problems and heuristics:

- **CornersProblem (Q5)** — State is `(position, visited_corners_tuple)` where the tuple tracks which of the four corners have been reached. Goal is when all four booleans are True.

- **corners_heuristic (Q6)** — Computes the Manhattan distance to the nearest unvisited corner plus the MST cost over all unvisited corners. Consistent and admissible.

- **food_heuristic (Q7)** — Computes the real maze distance to the nearest food plus the MST cost over all remaining food positions using cached BFS distances. Consistent and admissible. Expands ~255 nodes on trickySearch (extra credit tier).

- **AnyFoodSearchProblem (Q8)** — Goal test returns True if there is food at the current position.

- **path_to_closest_dot (Q8)** — Runs BFS on AnyFoodSearchProblem to find the shortest path to the nearest food dot.

---

## Engineering Process

The main implementation challenge was that the `util.py` in this project uses renamed data structures compared to the standard Berkeley version: `LIFO` instead of `Stack`, `FIFO` instead of `Queue`, and `.put()`/`.get()`/`.is_empty()` instead of `.push()`/`.pop()`/`.isEmpty()`. The search algorithms were written to match these names.

For the heuristics, an initial MST approach that included the current position as a node was found to be inconsistent — taking one step could reduce the heuristic by more than 1, violating the consistency condition `h(s) ≤ cost(s→s') + h(s')`. The fix was to separate the heuristic into two parts: distance from the current position to the nearest goal node, plus the MST cost over only the goal nodes themselves. This ensures each step reduces the heuristic by at most 1.

The food heuristic uses actual maze distances (computed via BFS) rather than Manhattan distances to get a tighter lower bound, which significantly reduces the number of nodes A* needs to expand.

---

## AI Use

I used AI assistance to help understand project instructions and debug general concepts. The final code implementation was written, tested, and verified by me. AI was also used to help improve the formatting and presentation of this README after I wrote an initial draft.


## Autograder Results

Provisional grades
==================
Question q1: 3/3 
Question q2: 3/3 
Question q3: 3/3 
Question q4: 3/3 
Question q5: 3/3 
Question q6: 3/3 
Question q7: 5/4 
Question q8: 3/3 
------------------
Total: 26/25

Your grades are NOT yet registered.  To register your grades, make sure
to follow your instructor's guidelines to receive credit on your project.

Abdullahs-MacBook-Pro:search-2 abdullahshah$ 

