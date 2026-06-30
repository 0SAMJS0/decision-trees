# Pacman Search Project





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

---

## Engineering Process

The main implementation challenge was that the `util.py` in this project uses renamed data structures compared to the standard Berkeley version: `LIFO` instead of `Stack`, `FIFO` instead of `Queue`, and `.put()`/`.get()`/`.is_empty()` instead of `.push()`/`.pop()`/`.isEmpty()`. The search algorithms were written to match these names.

For the heuristics, an initial MST approach that included the current position as a node was found to be inconsistent — taking one step could reduce the heuristic by more than 1, violating the consistency condition `h(s) ≤ cost(s→s') + h(s')`. The fix was to separate the heuristic into two parts: distance from the current position to the nearest goal node, plus the MST cost over only the goal nodes themselves. This ensures each step reduces the heuristic by at most 1.

The food heuristic uses actual maze distances (computed via BFS) rather than Manhattan distances to get a tighter lower bound, which significantly reduces the number of nodes A* needs to expand.

---

Abdullahs-MacBook-Pro:search-2 abdullahshah$ 

