# ☕ Java DSA Interview Cheat Sheet

<p align="center">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original.svg" width="80" alt="Java Logo" />
</p>

<p align="center">
  <b>A quick reference to essential Java APIs, collections, and coding patterns for DSA and technical interviews.</b>
</p>

---

## 📚 Table of Contents

- [1. HashMap](#1-hashmap)
- [2. HashSet](#2-hashset)
- [3. PriorityQueue](#3-priorityqueue)
- [4. ArrayDeque](#4-arraydeque)
- [5. Collections.sort()](#5-collectionssort)
- [6. Arrays.sort()](#6-arrayssort)
- [7. Arrays.binarySearch()](#7-arraysbinarysearch)
- [8. StringBuilder](#8-stringbuilder)
- [9. String](#9-string)
- [10. Enhanced For Loop](#10-enhanced-for-loop)
- [11. Fast Input](#11-fast-input)
- [12. Must-Know Methods](#12-must-know-methods)

---

## 1. HashMap

```java
import java.util.HashMap;
import java.util.Map;
import java.util.ArrayList;

HashMap<Integer, String> map = new HashMap<>();
```

### Insert

```java
map.put(key, value);
map.putIfAbsent(key, value);
```

### Access

```java
map.get(key);
map.getOrDefault(key, defaultValue);
map.containsKey(key);
map.containsValue(value);
```

### Remove

```java
map.remove(key);
map.remove(key, value);
map.clear();
```

### Update and Compute

```java
map.replace(key, value);
map.replace(key, oldValue, newValue);

map.computeIfAbsent(key, k -> new ArrayList<>());
map.computeIfPresent(key, (k, v) -> v + 1);

map.merge(key, 1, Integer::sum);
```

### Traversal

```java
for (Map.Entry<Integer, String> entry : map.entrySet()) {
    int key = entry.getKey();
    String value = entry.getValue();
}
```

**DSA tip:** Use `getOrDefault()` for frequency counting and `merge()` to increment counts concisely.

```java
map.merge(num, 1, Integer::sum);
```

## 2. HashSet

```java
import java.util.HashSet;

HashSet<Integer> set = new HashSet<>();
```

```java
set.add(x);
set.contains(x);
set.remove(x);

set.size();
set.isEmpty();
set.clear();
```

**DSA tip:** `HashSet` is useful for duplicate detection and membership checks. Basic operations are \(O(1)\) on average.

## 3. PriorityQueue

### Min Heap

```java
import java.util.PriorityQueue;

PriorityQueue<Integer> pq = new PriorityQueue<>();
```

### Max Heap

```java
import java.util.Collections;
import java.util.PriorityQueue;

PriorityQueue<Integer> maxHeap =
    new PriorityQueue<>(Collections.reverseOrder());
```

### Common Operations

```java
pq.offer(x);       // Insert
pq.add(x);         // Insert; may throw if insertion fails
pq.peek();         // View minimum/maximum
pq.poll();         // Remove and return head
pq.remove(x);      // Remove a specific element
pq.contains(x);
pq.size();
pq.isEmpty();
```

**Complexity:** `offer()` and `poll()` are \(O(\log n)\); `peek()` is \(O(1)\).

**DSA tip:** Use heaps for top-K problems, Kth-largest elements, and merging sorted lists.

## 4. ArrayDeque

```java
import java.util.ArrayDeque;

ArrayDeque<Integer> deque = new ArrayDeque<>();
```

### Insert

```java
deque.offerFirst(x);
deque.offerLast(x);

deque.push(x);     // Insert at front
deque.offer(x);    // Insert at end
```

### Remove

```java
deque.pollFirst();
deque.pollLast();

deque.pop();       // Remove from front
deque.poll();      // Remove from front
```

### Access

```java
deque.peekFirst();
deque.peekLast();
deque.peek();
deque.size();
deque.isEmpty();
```

**DSA tip:** Use `ArrayDeque` as a stack or queue. Prefer it over the legacy `Stack` class for most stack problems.

Note: `ArrayDeque` does not permit `null` elements.

## 5. Collections.sort()

```java
import java.util.Collections;
import java.util.Comparator;
import java.util.List;
```

### Ascending and Descending

```java
Collections.sort(list);
Collections.sort(list, Collections.reverseOrder());
```

### Custom Comparator

```java
list.sort((a, b) -> Integer.compare(a.age, b.age));
```

### Multiple Fields

```java
list.sort(
    Comparator.comparing(Person::getAge)
              .thenComparing(Person::getName)
);
```

**Tip:** Prefer `Integer.compare(a, b)` over `a - b` to avoid integer overflow in comparators.

## 6. Arrays.sort()

```java
import java.util.Arrays;
```

### Basic Sorting

```java
Arrays.sort(arr);
Arrays.sort(arr, from, to);
```

The range `from` to `to` is half-open: `from` is included and `to` is excluded.

### Sorting 2D Arrays

```java
Arrays.sort(matrix, (a, b) -> Integer.compare(a[0], b[0]));
```

### Sorting Strings in Reverse Order

```java
Arrays.sort(strings, Collections.reverseOrder());
```

Note: Reverse-order sorting works with object arrays, such as `String[]`, not primitive arrays such as `int[]`.

## 7. Arrays.binarySearch()

```java
Arrays.binarySearch(arr, target);
Arrays.binarySearch(arr, from, to, target);
```

**Important:** The array must be sorted before using binary search for predictable results.

- Return value `>= 0`: index of a matching element.
- Return value `< 0`: `-(insertion point) - 1`.

```java
int index = Arrays.binarySearch(arr, target);

if (index >= 0) {
    System.out.println("Found at index " + index);
} else {
    int insertionPoint = -index - 1;
}
```

**Complexity:** \(O(\log n)\).

## 8. StringBuilder

```java
StringBuilder sb = new StringBuilder();
```

### Modify

```java
sb.append("Java");
sb.insert(0, "Learn ");
sb.delete(0, 6);
sb.deleteCharAt(0);
sb.replace(0, 4, "Code");
sb.reverse();
```

### Access and Convert

```java
sb.charAt(index);
sb.setCharAt(index, 'x');

sb.length();
sb.capacity();

sb.substring(start);
sb.substring(start, end);
sb.toString();
```

**DSA tip:** `StringBuilder` is generally more efficient than repeated string concatenation inside loops.

## 9. String

### Substring

```java
s.substring(start);
s.substring(start, end);
```

The ending index is exclusive.

### Split

```java
s.split(",");
s.split("\\s+");
s.split("[,:;]");
```

`split()` accepts a regular expression, so special regex characters may need escaping.

### Character Operations

```java
char c = s.charAt(i);

Character.isDigit(c);
Character.isLetter(c);
Character.isUpperCase(c);
Character.isLowerCase(c);
```

### Other Useful Methods

```java
s.length();
s.equals(other);
s.equalsIgnoreCase(other);
s.contains("Java");
s.indexOf('a');
s.toCharArray();
s.toLowerCase();
s.toUpperCase();
```

## 10. Enhanced For Loop

### Array

```java
for (int x : arr) {
    // Process x
}
```

### List

```java
for (int x : list) {
    // Process x
}
```

### Set

```java
for (int x : set) {
    // Process x
}
```

### HashMap

```java
for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
    int key = entry.getKey();
    int value = entry.getValue();
}
```

**Tip:** Use a traditional indexed loop when you need array indices or want to modify elements by position.

## 11. Fast Input

### BufferedReader and StringTokenizer

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

BufferedReader br = new BufferedReader(
    new InputStreamReader(System.in)
);

int n = Integer.parseInt(br.readLine());

StringTokenizer st = new StringTokenizer(br.readLine());

int a = Integer.parseInt(st.nextToken());
int b = Integer.parseInt(st.nextToken());

String s = br.readLine();
long l = Long.parseLong(br.readLine());
double d = Double.parseDouble(br.readLine());
```

For complete programs, handle `IOException` using `throws IOException` in `main()` or a `try-catch` block.

**Important:** `readLine()` reads an entire line. If input values span multiple lines, create a reusable token-reading helper instead of assuming all tokens are on one line.

---

## 12. Must-Know Methods

| Structure | Essential methods |
|---|---|
| `HashMap` | `put`, `get`, `getOrDefault`, `containsKey`, `merge`, `entrySet` |
| `HashSet` | `add`, `contains`, `remove`, `size` |
| `PriorityQueue` | `offer`, `poll`, `peek` |
| `ArrayDeque` | `offerFirst`, `offerLast`, `pollFirst`, `pollLast`, `push`, `pop` |
| `Arrays` | `sort`, `binarySearch`, `fill`, `copyOf` |
| `Collections` | `sort`, `reverse`, `shuffle`, `max`, `min` |
| `String` | `length`, `charAt`, `substring`, `split`, `equals` |
| `StringBuilder` | `append`, `insert`, `delete`, `reverse`, `setCharAt` |
| Fast Input | `BufferedReader`, `StringTokenizer` |

---

## 🎯 Interview Reminders

- Know the average time complexity of common collection operations.
- Use a `HashMap` for frequency counting and a `HashSet` for uniqueness.
- Use a min heap or max heap for top-K and Kth-element problems.
- Use `ArrayDeque` for stack and queue implementations.
- Sort before using binary search.
- Use `StringBuilder` when building strings repeatedly.
- Avoid subtraction-based comparators when integer overflow is possible.

---

<p align="center">
  <b>☕ Practice consistently. Understand the APIs. Master the patterns.</b>
</p>
