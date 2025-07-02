
# Push_swap

Push_swap is a sorting algorithm challenge from the 42 programming school. The goal is to sort a list of integers using only a specific set of stack operations. The program outputs the smallest number of operations required to sort the given list.

---

## 📌 Project Objective

You are given a list of integers and two stacks (`a` and `b`). The task is to sort stack `a` in ascending order using a limited set of instructions (push, swap, rotate, reverse rotate). The result should be an optimized sequence of instructions that sorts the numbers using the fewest operations.

---

## ⚙️ Allowed Operations

- `sa` / `sb` / `ss`: swap top two elements of `a`, `b`, or both.
- `pa` / `pb`: push top element from one stack to the other.
- `ra` / `rb` / `rr`: rotate stack up (first becomes last).
- `rra` / `rrb` / `rrr`: reverse rotate stack down (last becomes first).

---

## 🧠 Algorithm Explanation

### 🔹 1. `/push_swap__range`: Chunk-Based Sorting (Partitioning)

The file `push_swap` implements a **chunking algorithm**. Here's how it works:

- The unsorted list is copied and sorted to find "pivot values."
- Based on input size, the list is divided into `n` ranges or **chunks**.
- Elements from `stack a` are pushed to `stack b` if they fall within the current chunk.
- `ra` or `rra` is used to bring chunk elements to the top efficiently.
- Once a chunk is in `stack b`, it is reassembled into `a` using the best-move strategy.

**Why chunks?**
- Reduces the search space per loop.
- Prevents unnecessary rotations.
- More scalable for 100+ numbers.

> Example: For 100 elements, divide into 5 chunks of 20.

---

### 🔹 2. `/push_swap__best_move`: Cost Optimization Algorithm

Once numbers are in `stack b`, `push_swap` decides **which element to push back to `stack a` next** by computing move costs.

For each element in `stack b`:
- Calculate how many moves it takes to bring it to the top of `b` (using `rb` or `rrb`).
- Calculate how many moves are needed in `a` to prepare the correct position for that element.
- **Total cost = moves in b + moves in a.**

Then:
- Choose the element with the **lowest total cost**.
- Perform simultaneous rotations if possible (`rr`, `rrr`) to optimize steps.
- Push the element with `pa`.

This ensures the re-insertion into `stack a` is **as efficient as possible**.

---

## 🚀 How to Build & Run

```bash
git clone https://github.com/mouchtach/Push_swap.git
cd Push_swap
make
./push_swap 3 2 1 6 5 8
````

It will output a list of commands like:

```
pb
pb
sa
ra
pa
pa
```

---

## 📊 Efficiency Goals

| Stack Size | Max Instructions (bonus) |
| ---------- | ------------------------ |
| ≤ 3        | 2–3 moves                |
| ≤ 5        | \~10–12 moves            |
| 100        | ≤ 700–900 moves          |
| 500        | ≤ 5500–7000 moves        |

> Use `./checker` with the same arguments to validate sorting.

---

## ✅ Bonus Features (if implemented)

* `checker`: validates if a sequence of operations sorts the input.
* Visualization or step tracking.
* Optional flags (e.g., `-v` for verbose output).

---

## 🧪 Example

```bash
ARG="4 67 3 87 23"; ./push_swap $ARG | ./checker $ARG
# Output: OK
```

---

```

### Summary of Key Files:

| File         | Purpose                                               |
|--------------|-------------------------------------------------------|
| `range.c`    | Splits input into chunks; manages pushing from A to B |
| `best_move.c`| Computes optimal moves for pushing back from B to A   |

Would you like diagrams or pseudocode added for each step?
```
