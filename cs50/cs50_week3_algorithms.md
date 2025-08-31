# CS50 Week 3: Algorithms

## Searching

### Linear Search

- Check each element **one by one** until the target is found or the list ends.
- Worst case: target is at the end or not in the list at all.

### Binary Search

- Works only on **sorted data**.
- Process:
  1. Start in the **middle** of the list.
  2. If the target is smaller, search the **left half**.
  3. If the target is larger, search the **right half**.
  4. Repeat until found or no elements remain.

⚠️ **Important:** You cannot use binary search on unsorted data.

---

## Running Time

- **Running time** measures how long an algorithm takes to complete, relative to input size.

### Big O Notation (Upper Bound)

- Describes the **worst-case performance** of an algorithm.
- Common complexities:
  - `O(n)` → linear time
  - `O(n/2)` → still linear, constants are ignored, so this is **O(n)**
  - `O(log n)` → logarithmic time (binary search)

### Capital Ω (Omega) Notation (Lower Bound)

- Describes the **best-case performance** of an algorithm.

### Asymptotic Notation

- Describes the behavior of algorithms as inputs grow very large.
- Helps compare **scalability and efficiency** rather than exact timing.

---

## Strings in C

- Direct comparison using `==` **does not work** on strings.
- Use the `strcmp()` function from **`string.h`**:

  ```c
  strcmp(strings[i], s) == 0
  ```

- This compares the **contents** of the strings, not their memory addresses.

---

## Structs in C

- There is no built-in `person` data type.

- You must define your own with `typedef struct`:

  ```c
  typedef struct {
      string name;
      string number;
  } person;
  ```

- Example:

  ```c
  person people[];
  ```

---

## Sorting Algorithms

### Selection Sort

- Find the **smallest element** and swap it with the first.
- Repeat for the rest of the list.
- Time complexity: **O(n²)**.

### Bubble Sort

- Repeatedly **swap adjacent elements** if they are out of order.
- Largest values "bubble" to the end.
- Time complexity: **O(n²)**.

---

## Summary

- **Searching:** Linear (O(n)) vs Binary (O(log n))
- **Sorting:** Selection and Bubble (both O(n²))
- **Notations:** Big O (upper bound), Ω (lower bound), asymptotic analysis
- **Strings:** Must use `strcmp()` instead of `==`
- **Structs:** Define custom data types with `typedef struct`
