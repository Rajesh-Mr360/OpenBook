Determining **time and space complexity in Java** isn’t about the language itself — it’s about analyzing **how your algorithm or code behaves as input size (n) grows**.  
Below is a step-by-step guide to help you evaluate complexity when looking at Java code.

# Time Complexity — How long it takes to run
Time complexity depends on:
- Number of operations a program performs
- Loops, recursion, nested loops
- Data structures used


| Code Pattern               | Example                  | Complexity   |
| -------------------------- | ------------------------ | ------------ |
| Single Loop                | `for(int i=0; i<n; i++)` | O(n)         |
| Nested Loops               | `for i... for j...`      | O(n²)        |
| Divide and Conquer         | Binary Search            | O(log n)     |
| Traverse array/list        | `.forEach()`             | O(n)         |
| HashMap get/put            | `map.get()`              | O(1) average |
| Sorting (e.g. Arrays.sort) | QuickSort/Timsort        | O(n log n)   |

# Space Complexity — How much extra memory it needs

Memory depends on:
- Extra variables
- Arrays, collections created inside functions
- Recursion stack

## Examples

**O(1) — constant space**
```Java
int max(int[] arr) {
    int max = arr[0]; // only 1 variable regardless of n
    for (int i = 1; i < arr.length; i++) {
        if (arr[i] > max)
            max = arr[i];
    }
    return max;
}
```

→ **Space = constant → O(1)**

---

**O(n) — linear space**
```Java
int[] copy(int[] arr) {
    int[] temp = new int[arr.length]; // new array of size n
    for (int i = 0; i < arr.length; i++)
        temp[i] = arr[i];
    return temp;
}
```
→ creates new array size **n** → **O(n)**

---
**Recursion space**

```Java
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
```

Recursion depth = **n**  
→ **Space = O(n)**  
→ **Time = O(2ⁿ)** (exponential without memorization)

---
## 💡 **Shortcut Tips**

- Most **collection operations:**
    - `ArrayList.get(i)` → **O(1)**
    - `LinkedList.get(i)` → **O(n)**
    - `HashMap get/put` → **O(1)** average, **O(n)** worst        
- Sorting almost always **O(n log n)**

---

## 🔹 **What does “O” mean in Big-O notation?**
`O` stands for **“Order of”** or **“Growth rate of”**.

Big-O tells us **how fast the time or space used by an algorithm increases as input size `n` grows**.

Example:
- **O(n)** → time increases **linearly** with input
- **O(n²)** → time increases **quadratically**
- **O(1)** → constant time, doesn’t grow with input

So **O(...)** is like a _wrapper_ that contains the **growth formula**.

> **Big-O = How your algorithm _scales_ when `n` becomes huge**

---
## 🔹 **What does “log” mean?**

`log` usually refers to **logarithm base 2** in computer science.
### **Logarithm meaning (simple)**
> **How many times can you divide something by 2 before it becomes 1?**

Examples:

| n         | log₂(n) | Explanation                 |
| --------- | ------- | --------------------------- |
| 8         | 3       | 8 → 4 → 2 → 1 (3 divisions) |
| 16        | 4       | 16 → 8 → 4 → 2 → 1          |
| 1,000,000 | ~20     | divide by 2 twenty times    |

So log grows very **slowly** even when numbers get huge — that’s why `O(log n)` is efficient.

---
## 🌳 **Why “log” appears in complexity?**

Because **binary search, trees, heaps, divide-and-conquer algorithms** keep **splitting the data in half**.

Example **binary search**
```
n = 16
step 1 -> check middle -> 16/2 = 8
step 2 -> check middle -> 8/2 = 4
step 3 -> check middle -> 4/2 = 2
step 4 -> check middle -> 2/2 = 1
```

→ Took **4 steps** = **log₂(16)**  
→ Complexity = **O(log n)**

## **Quick intuition**

| Complexity   | Meaning                       | Example             |
| ------------ | ----------------------------- | ------------------- |
| **O(n)**     | Check everything              | Scan list           |
| **O(log n)** | Cut problem in half each step | Binary search       |
| **O(n²)**    | Nested loops                  | Comparing all pairs |

## 🎯 Final takeaway

- **O(...)** → describes **growth rate**    
- **log n** → means **divide by 2 repeatedly** → very efficient
