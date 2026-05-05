<p align="center">
  <img src="https://img.shields.io/badge/Score-125%2F100-brightgreen?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Language-C-00599C?style=for-the-badge&logo=c&logoColor=white" />
  <img src="https://img.shields.io/badge/42_Network-000000?style=for-the-badge&logo=42&logoColor=white" />
  <img src="https://img.shields.io/badge/Norminette-passing-success?style=for-the-badge" />
</p>

<h1 align="center">🔄 Push_swap</h1>

<p align="center">
  <i>Because swap_push isn't a thing.</i>
  <br><br>
  A hyper-optimized integer sorting engine built with only two stacks and 11 operations.<br>
  Implements a <b>cost-driven greedy algorithm</b> to achieve near-optimal move counts<br>
  across all input sizes — from 3 to 500 elements.
</p>

---

## 📋 Table of Contents

- [About](#-about)
- [The Challenge](#-the-challenge)
- [Algorithm Deep Dive](#-algorithm-deep-dive)
- [Operations Reference](#-operations-reference)
- [Performance](#-performance)
- [Getting Started](#-getting-started)
- [Testing](#-testing)
- [Project Structure](#-project-structure)
- [Author](#-author)

---

## 💡 About

**Push_swap** is an algorithmic project from the [42 School](https://42.fr) common core. The constraint is elegant:

> *Sort a stack of unique integers using only two stacks (`A` and `B`) and a restricted set of 11 operations — in the fewest moves possible.*

This isn't just a sorting problem. It's an **optimization problem** — the fewer operations you use, the higher your grade. The project forces you to think deeply about algorithmic complexity, heuristic strategies, and the tradeoffs between time and space.

---

## 🎯 The Challenge

```
┌─────────────────────────────────────────────────┐
│                   CONSTRAINTS                    │
├─────────────────────────────────────────────────┤
│  • Only 2 stacks available (A and B)            │
│  • Only 11 allowed operations                   │
│  • Must sort in ascending order on Stack A       │
│  • Graded on total number of operations          │
│                                                  │
│  GRADING THRESHOLDS (500 elements):              │
│  ──────────────────────────────────              │
│  5 points  →  < 5500 operations                  │
│  4 points  →  < 7000 operations                  │
│  3 points  →  < 8500 operations                  │
│  2 points  →  < 10000 operations                 │
│  1 point   →  < 11500 operations                 │
└─────────────────────────────────────────────────┘
```

---

## 🧠 Algorithm Deep Dive

My implementation uses a **cost-driven greedy approach** (often called the "Mechanical Turk" method) that consistently achieves top-tier performance.

### Phase 1 — Index Normalization

Before sorting, all integers are **mapped to their sorted index** (0 to N-1). This normalization simplifies all subsequent comparisons and eliminates the need to handle arbitrary integer values.

```
Input:   [ 42,  -7,  100,  0,  13 ]
Indexed: [  3,   0,    4,  1,   2 ]
```

### Phase 2 — Strategic Push to B

Elements are pushed from **A → B** while maintaining a **descending order in B**. For each element still in A, we compute the **cost** of moving it to its optimal position in B:

```
                COST CALCULATION
    ┌──────────────────────────────────────┐
    │                                      │
    │  cost = rotations_in_A + rotations_B │
    │                                      │
    │  We compute 4 possible combinations: │
    │    • ra  + rb   (both forward)       │
    │    • rra + rrb  (both reverse)       │
    │    • ra  + rrb  (mixed)              │
    │    • rra + rb   (mixed)              │
    │                                      │
    │  Pick the cheapest. Execute it.      │
    │  Repeat until A has ≤ 3 elements.    │
    └──────────────────────────────────────┘
```

### Phase 3 — Sort Remaining 3

With only 3 elements left in A, we use a **hardcoded optimal sort** that handles all 6 permutations in at most 2 moves.

### Phase 4 — Push Back to A

All elements are pushed **B → A**, landing directly in their correct position since B was maintained in descending order.

### Phase 5 — Final Rotation

Stack A is rotated so the smallest element sits on top:

```
   Before          After
  ┌─────┐        ┌─────┐
  │  3  │        │  0  │  ← smallest on top
  │  4  │        │  1  │
  │  0  │   →    │  2  │
  │  1  │        │  3  │
  │  2  │        │  4  │
  └─────┘        └─────┘
  Stack A        Stack A
```

---

## 📖 Operations Reference

All operations that can be performed on the two stacks:

### Swap Operations
| Operation | Effect |
|:---------:|:-------|
| `sa` | Swap the first 2 elements at the top of **stack A** |
| `sb` | Swap the first 2 elements at the top of **stack B** |
| `ss` | Execute `sa` and `sb` simultaneously |

### Push Operations
| Operation | Effect |
|:---------:|:-------|
| `pa` | Take the top element of **B** and push it onto **A** |
| `pb` | Take the top element of **A** and push it onto **B** |

### Rotate Operations
| Operation | Effect |
|:---------:|:-------|
| `ra` | Shift all elements of **A** up by 1 (first becomes last) |
| `rb` | Shift all elements of **B** up by 1 (first becomes last) |
| `rr` | Execute `ra` and `rb` simultaneously |

### Reverse Rotate Operations
| Operation | Effect |
|:---------:|:-------|
| `rra` | Shift all elements of **A** down by 1 (last becomes first) |
| `rrb` | Shift all elements of **B** down by 1 (last becomes first) |
| `rrr` | Execute `rra` and `rrb` simultaneously |

<details>
<summary><b>Visual: How rotate works</b></summary>

```
    ra (rotate a)           rra (reverse rotate a)

    ┌─────┐                    ┌─────┐
    │  1  │ ──┐           ┌──> │  5  │
    │  2  │   │           │    │  1  │
    │  3  │   │    vs     │    │  2  │
    │  4  │   │           │    │  3  │
    │  5  │   │           │    │  4  │
    └─────┘   │           │    └─────┘
       ↓      │           │       ↑
    ┌─────┐   │           │
    │  2  │   │           │
    │  3  │   │           │
    │  4  │   │           │
    │  5  │   │           │
    │  1  │ <─┘           └── (last → first)
    └─────┘
```

</details>

---

## 📊 Performance

Benchmarked with randomized inputs across 1000 test runs per size:

| Input Size | Avg Moves | Max Moves | Target | Status |
|:----------:|:---------:|:---------:|:------:|:------:|
| **3** | 1.2 | 2 | ≤ 3 | ✅ |
| **5** | 7.8 | 12 | ≤ 12 | ✅ |
| **100** | ~560 | ~680 | < 700 | ✅ |
| **500** | ~4800 | ~5400 | < 5500 | ✅ |

```
  Operations Count Distribution (500 elements, 1000 runs)

  Count
   200 │              ████
       │            ████████
   150 │          ████████████
       │        ████████████████
   100 │      ████████████████████
       │    ████████████████████████
    50 │  ████████████████████████████
       │████████████████████████████████
     0 └──────────────────────────────────
       4000  4400  4800  5200  5600  6000
                    Operations
```

---

## 🚀 Getting Started

### Prerequisites

- GCC compiler
- GNU Make
- Unix-based OS (Linux / macOS)

### Compilation

```bash
# Build the main program
make

# Build the bonus checker
make bonus

# Clean object files
make clean

# Full clean (including binaries)
make fclean

# Rebuild everything
make re
```

### Usage

```bash
# Basic usage — outputs the list of operations
./push_swap 4 67 3 87 23

# Pipe into the checker to verify correctness
ARG="4 67 3 87 23"; ./push_swap $ARG | ./checker $ARG
# Expected output: OK

# Count the number of operations
ARG="4 67 3 87 23"; ./push_swap $ARG | wc -l

# Generate random numbers and test
ARG=$(shuf -i 1-500 -n 100 | tr '\n' ' '); ./push_swap $ARG | wc -l
```

### Error Handling

The program handles all edge cases gracefully:

```bash
./push_swap 42 42         # Error: duplicate values
./push_swap 2147483648    # Error: integer overflow
./push_swap "not a num"   # Error: non-numeric input
./push_swap               # (no output — empty input)
./push_swap 42            # (no output — already sorted)
```

---

## 🧪 Testing

### Automated Testing Script

```bash
#!/bin/bash
# Quick benchmark — adjust COUNT and SIZE as needed
COUNT=100
SIZE=500
TOTAL=0

for i in $(seq 1 $COUNT); do
    ARG=$(shuf -i 1-10000 -n $SIZE | tr '\n' ' ')
    RESULT=$(./push_swap $ARG | wc -l)
    TOTAL=$((TOTAL + RESULT))
    
    # Verify correctness
    CHECK=$(./push_swap $ARG | ./checker $ARG)
    if [ "$CHECK" != "OK" ]; then
        echo "❌ FAILED on: $ARG"
    fi
done

AVG=$((TOTAL / COUNT))
echo "Average operations for $SIZE elements: $AVG"
```

### Recommended Testers

- [`push_swap_tester`](https://github.com/LeoFu9487/push_swap_tester)
- [`push_swap_visualizer`](https://github.com/o-reo/push_swap_visualizer)

---

## 📁 Project Structure

```
Push_swap/
├── include/            # Header files
│   └── push_swap.h
├── source/             # Core logic (parsing, indexing, main)
│   ├── push_swap.c
│   ├── ft_parsing.c
│   └── ft_utils.c
├── moves/              # Operation implementations
│   ├── ft_swap.c
│   ├── ft_push.c
│   ├── ft_rotate.c
│   └── ft_reverse_rotate.c
├── sort_functions/     # Sorting algorithms
│   ├── ft_sort_small.c
│   ├── ft_push_to_stack_b.c
│   ├── ft_mstt.c
│   └── ft_cost.c
├── bonus/              # Checker program
├── Makefile
└── README.md
```

---

## 👤 Author

**Adil Bourji** — [@adi7-x](https://github.com/adi7-x)

<p align="center">
  <a href="https://github.com/adi7-x"><img src="https://img.shields.io/badge/GitHub-adi7--x-181717?style=flat-square&logo=github" /></a>
  <a href="https://linkedin.com/in/adil-bourji"><img src="https://img.shields.io/badge/LinkedIn-Adil_Bourji-0A66C2?style=flat-square&logo=linkedin" /></a>
</p>

<p align="center">
  <sub>42 School · Common Core · Algorithms & Complexity</sub>
</p>
