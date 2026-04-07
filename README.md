# EDA Algorithm Visualizer

> **Interactive web-based simulator for VLSI Partitioning and Placement algorithms**
> Built for Assignment 1 & 2 — Physical Design of VLSI Circuits

**Live Demo →** https://diveydoescode.github.io/eda-viz/

---

## Algorithms Implemented

### Assignment 1 — Partitioning
| Algorithm | Description |
|-----------|-------------|
| Kernighan–Lin (KL) | Min-cut graph partitioning via iterative node-pair swaps |
| Fiduccia–Mattheyses (FM) | Hypergraph partitioning via single-cell moves with gain buckets |

### Assignment 2 — Floorplanning
| Algorithm | Description |
|-----------|-------------|
| Cluster Growth | Area-sorted module placement minimizing bounding box |

---

## Features

- **Step-by-step animation** — play, pause, step forward/back through every algorithm decision
- **Speed control** — adjustable playback from 0.2s to 2.4s per step
- **Clickable step log** — jump to any step instantly
- **KL / FM** — live graph with nodes sliding between partitions, cut edges highlighted in red, D-values and gains shown at each step
- **Cluster Growth** — animated block placement with axis labels, bounding box, and spring-physics block entrance animation
- **Preset examples** — 2 presets per algorithm, matching the assignment problem sets
- **Progress scrubber** — click anywhere on the progress bar to seek

---

## Project Structure

```
eda-viz/
│
├── index.html    ← Entire application — all algorithms, UI, and animations
└── README.md
```

Everything runs in a single self-contained HTML file. No frameworks, no build step, no dependencies.

---

## How to Run

Open `index.html` in any modern browser — that's it.

```bash
# macOS
open index.html

# Windows
start index.html

# Linux
xdg-open index.html
```

Or visit the **live demo** linked above.

---

## Algorithm Details

### Kernighan–Lin (KL)

Operates on a weighted undirected graph. At each pass:
1. Computes **D-values**: `D[v] = external_cost(v) − internal_cost(v)`
2. Greedily selects the unlocked pair `(a, b)` from opposite partitions maximizing `gain = D[a] + D[b] − 2·c(a,b)`
3. Locks the pair and repeats until all nodes are locked
4. Finds the prefix of swaps with maximum cumulative gain and applies only those
5. Repeats passes until no improvement is found

**Complexity:** O(n² log n) per pass

### Fiduccia–Mattheyses (FM)

Extends KL to **hypergraphs** (nets connecting multiple cells). At each pass:
1. Moves one cell at a time to the partition that maximizes gain
2. Gain = reduction in number of cut nets
3. Locks moved cells; finds the best prefix of moves
4. Repeats until convergence

**Key improvement over KL:** handles multi-pin nets directly; O(p) per pass where p = total pins

### Cluster Growth (Floorplan)

1. **Linear ordering** — sorts modules by area, largest first
2. **Greedy placement** — for each module, evaluates all candidate positions (corners of already-placed modules)
3. Places at the position minimizing **bounding box area**, with aspect ratio as a tiebreaker

---

## Example Results

### KL — 6-node Weighted Graph
- Initial: `{1,2,3} | {4,5,6}`, Cut = 5
- After KL: Cut = **4**

### FM — 6-cell Hypergraph
- Initial: `{a,b,c} | {d,e,f}`, Cut = 3
- After FM: Cut = **0**

### Cluster Growth — 6 Modules
```
M1(4×3), M2(2×5), M3(3×3), M4(2×2), M5(4×2), M6(1×4)
Bounding Box: 7 × 8 = 56 u²
```

---

## Deployment

Deployed on GitHub Pages. To run locally, just open `index.html` in any browser.

---

## Submission Details

| | |
|---|---|
| **Name** | Divey Pradhan |
| **Roll No.** | 23FE10EVL00003 |
| **Program** | B.Tech Electronics Engineering (VLSI Design & Technology) |
| **University** | Manipal University Jaipur |
| **Subject** | VLSI Physical Design |
| **Assignments** | 1 (KL, FM Partitioning) and 2 (Cluster Growth Floorplan) |
