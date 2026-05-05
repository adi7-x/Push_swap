<p align="center">
  <img src="https://img.shields.io/badge/Score-125%2F100-brightgreen?style=for-the-badge" />
    <img src="https://img.shields.io/badge/Language-C-00599C?style=for-the-badge&logo=c&logoColor=white" />
      <img src="https://img.shields.io/badge/42_Network-000000?style=for-the-badge&logo=42&logoColor=white" />
        <img src="https://img.shields.io/badge/Norminette-passing-success?style=for-the-badge" />
</p>p>

<h1 align="center">Push_swap</h1>h1>

<p align="center">
  <i>Because swap_push isn't a thing.</i>i>
    <br><br>
      A hyper-optimized integer sorting engine built with only two stacks and 11 operations.<br>
        Implements a <b>cost-driven greedy algorithm</b>b> to achieve near-optimal move counts<br>
          across all input sizes -- from 3 to 500 elements.
</p>p>

---

## Table of Contents

- [About](#-about)
- - [The Challenge](#-the-challenge)
  - - [Algorithm Deep Dive](#-algorithm-deep-dive)
    - - [Operations Reference](#-operations-reference)
      - - [Performance](#-performance)
        - - [Getting Started](#-getting-started)
          - - [Testing](#-testing)
            - - [Project Structure](#-project-structure)
              - - [Author](#-author)
                -
                - ---
                -
                - ## About
                -
                - **Push_swap** is an algorithmic project from the 42 School common core. The constraint is elegant:
                -
                - > Sort a stack of unique integers using only two stacks (A and B) and a restricted set of 11 operations -- in the fewest moves possible.
                  >
                  > This isn't just a sorting problem. It's an optimization problem -- the fewer operations you use, the higher your grade.
                  >
                  > ---
                  >
                  > ## The Challenge
                  >
                  > Sort 500 elements in less than 5500 moves for a perfect score. Grading thresholds:
                  > - 3 elements: <= 3 moves
                  > - - 5 elements: <= 12 moves
                  >   - - 100 elements: < 700 moves
                  >     - - 500 elements: < 5500 moves
                  >       -
                  >       - ---
                  >       -
                  >       - ## Algorithm Deep Dive
                  >       -
                  >       - My implementation uses a cost-driven greedy approach (Mechanical Turk method):
                  >       -
                  >       - 1. Index Normalization -- Map all integers to their sorted index (0 to N-1)
                  >         2. 2. Strategic Push to B -- Push elements A->B maintaining descending order in B
                  >            3. 3. Cost Optimization -- For each element, calculate cheapest rotation combination (ra+rb, rra+rrb, ra+rrb, rra+rb)
                  >               4. 4. Sort Remaining 3 -- Hardcoded optimal sort for last 3 elements
                  >                  5. 5. Push Back to A -- All elements return to correct positions
                  >                     6. 6. Final Rotation -- Rotate until smallest element is on top
                  >                        7.
                  >                        8. ---
                  >                        9.
                  >                        10. ## Operations Reference
                  >                        11.
                  >                        12. ### Swap Operations
                  >                        13. | Operation | Effect |
                  >                        14. |:---------:|:-------|
                  >                        15. | sa | Swap first 2 elements of stack A |
                  >                        16. | sb | Swap first 2 elements of stack B |
                  >                        17. | ss | Execute sa and sb simultaneously |
                  >                        18.
                  >                        19. ### Push Operations
                  >                        20. | Operation | Effect |
                  >                        21. |:---------:|:-------|
                  >                        22. | pa | Push top of B onto A |
                  >                        23. | pb | Push top of A onto B |
                  >                        24.
                  >                        25. ### Rotate Operations
                  >                        26. | Operation | Effect |
                  >                        27. |:---------:|:-------|
                  >                        28. | ra | Rotate A up (first -> last) |
                  >                        29. | rb | Rotate B up (first -> last) |
                  >                        30. | rr | Execute ra and rb simultaneously |
                  >                        31.
                  >                        32. ### Reverse Rotate
                  >                        33. | Operation | Effect |
                  >                        34. |:---------:|:-------|
                  >                        35. | rra | Reverse rotate A (last -> first) |
                  >                        36. | rrb | Reverse rotate B (last -> first) |
                  >                        37. | rrr | Execute rra and rrb simultaneously |
                  >                        38.
                  >                        39. ---
                  >                        40.
                  >                        41. ## Performance
                  >                        42.
                  >                        43. | Input Size | Avg Moves | Max Moves | Target | Status |
                  >                        44. |:----------:|:---------:|:---------:|:------:|:------:|
                  >                        45. | 3 | 1.2 | 2 | <= 3 | OK |
                  >                        46. | 5 | 7.8 | 12 | <= 12 | OK |
                  >                        47. | 100 | ~560 | ~680 | < 700 | OK |
                  >                        48. | 500 | ~4800 | ~5400 | < 5500 | OK |
                  >                        49.
                  >                        50. ---
                  >                        51.
                  >                        52. ## Getting Started
                  >                        53.
                  >                        54. ### Compilation
                  >                        55.
                  >                        56. ```bash
                  >                            make          # Build the main program
                  >                            make bonus    # Build the bonus checker
                  >                            make clean    # Clean object files
                  >                            make fclean   # Full clean
                  >                            make re       # Rebuild
                  >                            ```
                  >
                  >                            ### Usage
                  >
                  >                            ```bash
                  >                            ./push_swap 4 67 3 87 23
                  >
                  >                            ARG="4 67 3 87 23"; ./push_swap $ARG | ./checker $ARG
                  >
                  >                            ARG="4 67 3 87 23"; ./push_swap $ARG | wc -l
                  >                            ```
                  >
                  >                            ---
                  >
                  >                            ## Testing
                  >
                  >                            Recommended testers:
                  >                            - push_swap_tester
                  >                            - - push_swap_visualizer
                  >                              -
                  >                              - ---
                  >                              -
                  >                              - ## Project Structure
                  >                              -
                  >                              - ```
                  >                                Push_swap/
                  >                                +-- include/          # Headers
                  >                                +-- source/           # Core logic
                  >                                +-- moves/            # Operations
                  >                                +-- sort_functions/   # Sorting algorithms
                  >                                +-- bonus/            # Checker program
                  >                                |-- Makefile
                  >                                +-- README.md
                  >                                ```
                  >
                  >                                ---
                  >
                  >                                ## Author
                  >
                  >                                Adil Bourji -- @adi7-x
                  >
                  >                                GitHub: https://github.com/adi7-x
                  >                                LinkedIn: https://linkedin.com/in/adil-bourji
                  >
                  >                                42 School . Common Core . Algorithms & Complexity
                  >                                </b></i>
