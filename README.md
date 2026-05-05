# Push_swap - Efficiency at its Core

<p align="center">
  <img src="https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=black" />
    <img src="https://img.shields.io/badge/42-000000?style=for-the-badge&logo=42&logoColor=white" />
      <img src="https://img.shields.io/badge/Algorithms-FF6F00?style=for-the-badge" />
        <img src="https://img.shields.io/badge/Optimization-00C853?style=for-the-badge" />
</p>p>

## Overview
The **Push_swap** project is a highly efficient sorting algorithm challenge from the 42 School curriculum. The goal is simple: sort a stack of integers using a second stack and a restricted set of operations, aiming for the **minimum number of moves**.

This implementation utilizes an optimized **Mechanical Turk** approach, achieving high-performance results that comfortably exceed the maximum requirements for a perfect score.

---

## Key Features
- **Highly Optimized**: Efficiently handles small (3, 5 elements) and large (100, 500 elements) stacks.
- - **Robust Error Handling**: Comprehensive validation for non-numeric input, duplicates, and integer overflows.
  - - **Clean Architecture**: Modular C code following the 42 Norm.
    - - **Bonus Included**: Features a custom `checker` to verify the sorting sequence.
     
      - ---

      ## Operations
      The algorithm manages two stacks, **A** and **B**, using the following operations:

      | Op | Description |
      | :--- | :--- |
      | `sa`/`sb` | Swap the first two elements of stack A/B. |
      | `ss` | `sa` and `sb` simultaneously. |
      | `pa`/`pb` | Push the top element of one stack to the other. |
      | `ra`/`rb` | Rotate stack (first element becomes last). |
      | `rr` | `ra` and `rb` simultaneously. |
      | `rra`/`rrb` | Reverse rotate (last element becomes first). |
      | `rrr` | `rra` and `rrb` simultaneously. |

      ---

      ## Performance Metrics
      My implementation consistently achieves the following benchmarks:
      - **3 elements**: Max 3 moves.
      - - **5 elements**: Max 12 moves.
        - - **100 elements**: < 700 moves (Average).
          - - **500 elements**: < 5500 moves (Average).
           
            - ---

            ## Usage

            ### Compilation
            ```bash
            make          # Compiles push_swap
            make bonus    # Compiles the checker
            ```

            ### Execution
            ```bash
            ./push_swap 3 2 5 1 4
            ```

            ### With Checker
            ```bash
            ARG="3 2 5 1 4"; ./push_swap $ARG | ./checker $ARG
            ```

            ---

            ## Algorithm Logic
            The algorithm follows a "greedy" strategy:
            1. **Push to B**: Elements are pushed from A to B based on their cost (total operations needed to place them in the correct position in B).
            2. 2. **Small Sort**: The last 3 elements in A are sorted using a hardcoded optimal sequence.
               3. 3. **Push back to A**: Elements are pushed back to A, ensuring they land in their final sorted position.
                  4. 4. **Final Rotation**: Stack A is rotated until the smallest element is at the top.
                    
                     5. ---
                    
                     6. ## Author
                     7. **Adil Bourji (adi7-x)**
                     8. - GitHub: [@adi7-x](https://github.com/adi7-x)
                        - - LinkedIn: [Adil Bourji](https://linkedin.com/in/adil-bourji)
                         
                          - ---
                          <p align="center">Made for the 42 Network</p>p>
                          
