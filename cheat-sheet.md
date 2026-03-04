---
description: >-
  A concise and handy reference for frequently used Java coding patterns,
  utilities, and best practices
icon: scroll
---

# Cheat Sheet

## Java

### **Operator**

* `+` / `-` have **higher precedence** than `<<` / `>>`
  * So `2 << x - 1` is evaluated as `2 << (x - 1)`

### **Math**

* Modulo Distributive Property
  * $$(a+b)\%mod=((a\%mod)+(b\%mod))\%mod$$
  * $$(a-b)\%mod=(a-b+mod)\%mod$$
  * Taking the modulus early can sometimes help prevent overflow in problems with huge numbers.
*   Get the greatest common divisor (最大公约数)

    ```java
      private int gcd(int x, int y) {
          if (y == 0) {
              return x;
          }
          return gcd(y, x%y);
      }
    ```
* Get the least common multiple (最小公倍数)
  * $$lcm(a,b) * gcd(a,b) = a*b ⇒ lcm(a,b) = a/gcd(a,b)*b$$
  * ```
    核心原因：质因数分解。把两个数写成质因数形式。
    例如
    a = 2^3 * 3^1
    b = 2^1 * 3^2

    gcd 取较小指数。因为最大公约数要，两边都能整除。所以指数取 min。
    gcd(a,b) = 2^1 * 3^1

    lcm 取较大指数。因为最小公倍数要 同时包含两个数所有因子。所以指数取 max。
    lcm(a,b) = 2^3 * 3^2

    gcd * lcm
    = (2^1 * 3^1) * (2^3 * 3^2)
    = 2^(1+3) * 3^(1+2)
    = 2^4 * 3^3

    a*b
    = (2^3 * 3^1) * (2^1 * 3^2)
    = 2^(3+1) * 3^(1+2)
    = 2^4 * 3^3

    补充：如果某个质因数不存在，就认为它的指数是 0。
    a = 12 = 2^2 * 3^1 = 2^2 * 3^1 * 5^0
    b = 25 = 5^2       = 2^0 * 3^0 * 5^2
    gcd = 1
    lcm = 300
    ```
* Encode point(x,y), $$0 <= x,y <= 40000$$, to ensure **unique encoding** for all points
  * Encode Result: `40001 * x + y`
  * Proof: Ask ChatGPT why to save some space here. Basically, use **proof by contradiction**. When `40001*x1+y1 == 40001*x2+y2`, we must have `x1==x2 && y1==y2`
*   For a given array, randomly pick an element

    ```java
    Random random = new Random();
    T element = arr[random.nextInt(arr.length)]
    ```
* `1e-5 == 1 * 10^-5` (scientific notation for double)

### **Bit**

* 2^x
  * `2<<x`&#x20;
  * `Math.pow(2, x); // return type is double!`

### **Character**

* If `c` is not a letter, Java won't change it. `Character.toLowerCase(c)`

### **Array & ArrayList**

* Initialize `List` with values: `... = Arrays.asList(0, 1, 2);`
* Sort array: `Arrays.sort(nums);`
  * This function does **NOT** support custom `Comparator` if `nums` is **primitive** type e.g.`int[]`. Need to make it as `Integer[]` here instead because `Comparator` is only supported for reference types (e.g., `Integer[]`, `String[]`, etc.)
  * However, `int[][]` can work, The key here is that while `int[]` itself is a primitive array, `int[][]` is not. `int[][]` is treated as an array of **references**, where each **reference** points to a 1D array (int\[])
  * Reference: [https://leetcode.com/discuss/feedback/2183318/lambda-in-java-sort-broken](https://leetcode.com/discuss/feedback/2183318/lambda-in-java-sort-broken)
* Sort List: `Collections.sort(list);`
* Reverse `List` using method: `Collections.reverse(result);`
  * This method modifies `List` in place and return `void`.
* Convert `List<Integer>` to `int[]`:&#x20;
  * 自动拆箱: `list.stream().mapToInt(i->i).toArray();`&#x20;
  * 显式拆箱: `list.stream().mapToInt(Integer::intValue).toArray();`
*   Convert `List<String>` to `String[]`

    ```java
    // Approach 1
    // Passing new String[0] is a common idiom to avoid pre-allocating the array size. 
    // The method internally determines the correct size and allocates a new array if needed.
    strArray = strList.toArray(new String[0]);
    // Approach 2
    strArray = strList.toArray(new String[strList.size()]);
    ```
* Convert `List<int[]>` to `int[][]`: `list.toArray(new int[list.size()][]);`
* Fill and initialize an array with a specific value: `Arrays.fill(c, '.');`
* Get the sum of the int array: `Arrays.stream(nums).sum();`
*   Sort an int array using the absolute value (small to large)

    ```java
     nums = IntStream.of(nums)
           .boxed()
           .sorted((o1, o2) -> Math.abs(o1) - Math.abs(o1))
           .mapToInt(Integer::intValue).toArray();
    ```
*   Sort a 2d int array `int[][]` by the first element of each element (LC406)

    ```java
    Arrays.sort(array, (a, b)->{
      if (a[0]==b[0]) {
        return a[1]-b[1];
      }
      return b[0]-a[0];
    });
    ```
* Sort 2d array using just 1 attr of each element: `Arrays.sort(points, (a, b) -> Integer.compare(a[0], b[0]));`
  * Use `Integer.compare` to **AVOID OVERFLOW**
* Compare the values of 2 lists of `ArrayList<Integer>`: `list1.equals(list2)`
* Remove all items from `ArrayList`: `ArrayList.clear()`
* Encode `int[]` to `String`: `Arrays.toString(arr)`&#x20;
* For Java `Arrays.sort(arr)` , TC: $$O(n*logn)$$, SC: $$O(logn)$$

### **Linked List**

* New linked list which contains an array: `List<int[]> linkedList = new LinkedList<>();`
* `LinkedList` add: `linkedList.add(index, element);`
* Convert `LinkedList` to array: `linkedList.toArray(new int[array.length][elementArrayLength]);`&#x20;
*   Add to the head of `LinkedList`

    ```java
    List list = new LinkedList<>();
    list.addFirst(10); // add to head
    ```

### **Type Conversion**

* Type promotion rules, **operands of different types** are **automatically promoted** to the **same type** based on the following **hierarchy (order matters)**:
  * If either operand is `double`, the other operand is promoted to `double`, and the result is of type `double`.
  * If no operand is `double` but one is `float`, the other operand is promoted to `float`, and the result is of type `float`.
  * If neither is `double` or `float`, but one is `long`, the other operand is promoted to `long`, and the result is of type `long`.
  * Otherwise, both operands are promoted to `int`, and the result is of type `int`.
* Convert int to long: `(long) var`
* Convert String to int `int num = Integer.parseInt(s)`
* Convert int to String `Integer.toString(num)` or `String.valueOf(num)`
* Convert `List<int[]> list` to `int[][] array`: `list.toArray(new int[list.size()][])`
* Convert `List<T>` to `Set<T>`: `Set<T> set = new HashSet(list);`&#x20;
* Convert values of `Map<String, List<String>>` to `List<List<String>>`&#x20;
  * ```
    Map<String, List<String>> map = new HashMap<>();
    ......
    // map.values() returns Collection<List<String>> type
    List<List<String>> = new ArrayList<>(map.values());
    ```

### **Stack and Queue**

* Queue / Stack: `Deque<Integer> queue = new ArrayDeque<>();`
  * Useful methods: `offerFirst(), offerLast(), pollFirst(), pollLast(), size(), isEmpty()`
* Convert `Deque<Character>` to `String`

```java
    StringBuilder builder = new StringBuilder();
    while (!deque.isEmpty()) {
        builder.append(deque.pollFirst());
    }
```

```java
    String s = String.valueOf(deque);
```

### **Heap**

* Heap (`PriorityQueue`)
  * For `Comparator` (a,b)
    * return negative means that a comes before b
    * return 0 means that a is equal to b
    * return positive means that b comes before a

```java
/*
*  Min Heap
*  a < b -> a - b < 0
*      return -1
*  a == b ...
*  a > b -> a - b > 0
*      return 1
*/
PriorityQueue<Integer> minHeap = new PriorityQueue<>((a,b) -> a - b);

/*
*  Max Heap
*  a < b -> b - a > 0
*     return 1
*  a == b ...
*  a > b -> b - a < 0
*     return -1
*/
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a,b) -> b - a);
```

### **Character**

* Change character `c` to lowercase: `Character.toLowerCase(c)`
* Check if character `c` is an alphanumeric: `Character.isLetterOrDigit(c)`

### **String**

* `StringBuilder`
  * Create using existing `String` var: `new StringBuilder(s);`
  * `length`: `int length = builder.length();`
  * `insert`: `builder.insert(index, '.');`
  * `deleteCharAt`: `builder.deleteCharAt(index);`
* When you need to build a `String` **from the end**
  * **Use `StringBuilder.append()`** to build strings efficiently from the end, as it operates in $$O(1)$$ (amortized time) without shifting characters. After appending, use **`StringBuilder.reverse()`** in $$O(n)$$ to reverse the result in one step if needed.
  * Avoid using **`insert(0, ...)`**, which has $$O(n²)$$ complexity due to repeated character shifts.
* When you need to return a string, also check if you can use `startIndex` and `resLen` to store temporary results in the middle of the calculation.
* Create `Strin` using `char[]`:
  * Use entire `char[]`: `String s = new String(charArray);`
  * Use part of `char[]`: `String s = new String(charArray, startIndex, len);`
  * Other ways: `String.copyValueOf(charArray);`

### **Map**

* `TreeMap`: It uses a Red-Black Tree internally to store key-value pairs. This ensures that the map is sorted by its keys, either in natural order (if the keys implement Comparable) or by a custom comparator provided when creating the TreeMap.
  * `descendingMap()`: TC $$O(1)$$, The `descendingMap()` method does **NOT create a new copy** of the TreeMap. Instead, it returns a view of the **original map in reverse order**.
  * `floorKey(k)`: Returns the greatest key less than or equal to the given key, or null if there is no such key.&#x20;
    * TC: $$O(logN)$$
  * `subMap(K fromKey, boolean fromInclusive, K toKey, boolean toInclusive)` : Returns a view of the portion of this map whose keys range from fromKey to toKey.
    * Any changes (e.g., `put`, `remove`, or `clear`) made to the view **directly affect the original `TreeMap`**, and vice versa. It operates on the **same underlying data structure**.
    * TC: $$O(logN)$$
* `getOrDefault()`: If the key exists, get its value. Otherwise, get the default value. For example, `map.getOrDefault(key, defaultValue)`;
* `size()`: Returns the number of key-value mappings in this map.
* `remove()`: Removes the mapping for the specified key from this map if present.
*   If you want to record the count of each char in a string, you can use `int[]` directly

    ```java
    // ASCII is a 7-bit character set having 128 characters, i.e., from 0 to 127.
    int[] map = new int[128];
    for (char c : s.toCharArray()) {
        map[c]++;
    }
    ```
* `computeIfAbsent(key, mappingFunction)`
  * Use case: For example, `Map<Integer, List<Integer>>`. When the key does **NOT** exist, we want to **create** a `List` first and then add the **first** element into `List`; When the key exists, we want to **get the existing list** and **append** a new element to that `List`. **This is frequently used in building adjacency lists using `Map` in the graph topic.**
  * Syntax example: `map.computeIfAbsent("key", k -> new ArrayList<>()).add("value1");`

| Feature                          | `putIfAbsent`                                    | `computeIfAbsent`                                                    |
| -------------------------------- | ------------------------------------------------ | -------------------------------------------------------------------- |
| **Purpose**                      | Adds a key-value pair if the key is absent.      | Computes the value if the key is absent and adds the key-value pair. |
| **Input Value**                  | Requires a precomputed value to insert.          | Computes the value dynamically using a mapping function.             |
| **Usage of Function**            | No function support; only direct values.         | Accepts a mapping function to compute the value if needed.           |
| **When Value is Present**        | Does **NOTHING** if the key already has a value. | Returns the **existing value** without computing.                    |
| **Return Value**                 | Returns the existing value or `null` if absent.  | Returns the existing value or the newly computed value.              |
| **Complex Value Initialization** | Not suitable for lazy or dynamic initialization. | Suitable for lazy or expensive computations.                         |

### **Set**

* Initialize `Set` with values: `Set<Character> set = new HashSet<>(Arrays.asList('a', 'A'));`
* `LinkedHashSet`
  * Use case: **LFU** !!!
  * Get the first item: `set.iterator().next()`
* `Set` implementations comparison

| Feature                  | **HashSet**             | **TreeSet**                 | **LinkedHashSet**        |
| ------------------------ | ----------------------- | --------------------------- | ------------------------ |
| **Underlying Structure** | Hash Table              | Red-Black Tree              | Hash Table + Linked List |
| **Order**                | Unordered               | Sorted                      | Insertion Order          |
| **Null Elements**        | Allows 1 `null`         | Not Allowed                 | Allows 1 `null`          |
| **Time Complexity**      | $$O(1)$$ for add/remove | $$O(log n)$$ for add/remove | $$O(1)$$ for add/remove  |
| **Duplicates**           | Not Allowed             | Not Allowed                 | Not Allowed              |

### Custom Class with Comparator

```java
// Class to store the height and coordinates of a cell in the grid
private static class Cell implements Comparable<Cell> {
    int height;
    int row;
    int col;

    // Constructor to initialize a cell
    public Cell(int height, int row, int col) {
        this.height = height;
        this.row = row;
        this.col = col;
    }

    // Overload the compareTo method to make the priority queue a min-heap based on height
    @Override
    public int compareTo(Cell other) {
        // Min-heap comparison
        return Integer.compare(this.height, other.height);
    }
}
```

## Techniques

### **Collapse alternating steps into a fixed-stride loop**

When an iteration’s “next index” alternates between two gaps (`stride = offset1 + offset2`) `offset1, offset2, offset1, offset2, …`, avoid toggling the step size. Instead:

* Loop with a **fixed step** `i += stride` .
* Inside the loop, do up to two “taps” within the cycle:
  * Work at `i` (the cycle starts).
  * If valid and non-duplicate, also work at `i + offset1`.
* Handle edge cases where `offset1 == 0` or `offset2 == 0` to avoid duplicates.

### Space-Efficient Character Lookup Tables

Commonly used tables are:

* `int[26]` for Letters 'a' - 'z' or 'A' - 'Z'
* `int[128]` for ASCII
* `int[256]` for Extended ASCII

### Phase (Split) linear scan.&#x20;

When different subranges require different logic, and simple predicates can partition the array, split a single `for` loop into several consecutive `while` loops. Each phase advances the same index and handles one segment (e.g., “before”, “during”, “after”).

Example question: LC 57. Insert Interval

### When to use Counting Sort

Counting sort operates by counting the number of objects that have each distinct key value, and using arithmetic on those tallies to determine the **positions** of each key value in the output sequence. Its running time is **LINEAR** in the number of items and the difference between the maximum and minimum keys, so it is only suitable for direct use in situations where the variation in keys is not significantly greater than the number of items.

