<h1 align="center">🔄 Push_swap</h1>

<p align="center">
  <strong>Sorting Algorithm Optimizer — 42 School</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=black"/>
  <img src="https://img.shields.io/badge/42-000000?style=for-the-badge&logo=42&logoColor=white"/>
  <img src="https://img.shields.io/badge/Algorithms-FF6F00?style=for-the-badge"/>
</p>

---

## About

An algorithmic challenge: sort a stack of integers using two stacks and a limited set of operations, in the **fewest moves possible**. This project explores sorting algorithms, algorithm complexity, and optimization strategies.

## Operations

| Operation | Description |
|-----------|-------------|
| `sa` / `sb` | Swap the first two elements of stack A / B |
| `ss` | `sa` and `sb` simultaneously |
| `pa` / `pb` | Push top of B onto A / Push top of A onto B |
| `ra` / `rb` | Rotate stack A / B (first element becomes last) |
| `rr` | `ra` and `rb` simultaneously |
| `rra` / `rrb` | Reverse rotate stack A / B (last becomes first) |
| `rrr` | `rra` and `rrb` simultaneously |

## Performance

| Input Size | Operations | Target |
|-----------|-----------|--------|
| 3 elements | ≤ 3 | ≤ 3 |
| 5 elements | ≤ 12 | ≤ 12 |
| 100 elements | < 700 | < 700 |
| 500 elements | < 5500 | < 5500 |

## Usage

```bash
make
./push_swap 4 67 3 87 23
# Outputs the list of operations to sort the stack

# Verify with the checker
ARG="4 67 3 87 23"; ./push_swap $ARG | ./checker $ARG
```

---

<p align="center"><sub>42 School · Common Core · Algorithms & Complexity</sub></p>
