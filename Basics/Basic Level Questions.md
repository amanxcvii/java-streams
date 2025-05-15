## 🟢 Basic Level Questions

1. 🔹 What are Streams in Java?  
   Streams in Java are a sequence of elements that support aggregate operations like filtering, mapping, and reducing. They provide a functional programming approach to process collections.

2. 🔹 How is Stream different from Collections?
   - Collections store data and manage it in-memory.
   - Streams process data in a functional style without modifying the original source.
   - Streams are lazy and support method chaining with lambdas.

3. 🔹 Difference between stream() and parallelStream()
   - stream(): Creates a sequential stream.
   - parallelStream(): Splits data into sub-streams for parallel processing (multi-threaded).

4. 🔹 Advantages of using Streams
   - Simplifies code and improves readability.
   - Efficient memory usage.
   - Supports parallel processing.
   - Chaining of operations (pipelining).

5. 🔹 What is Lazy Evaluation in Streams?
   Intermediate operations (like filter, map) are not executed until a terminal operation (like collect or forEach) is called.

6. 🔹 Difference between Intermediate and Terminal Operations
   - Intermediate: Return a Stream and are lazy (e.g., map, filter, distinct).
   - Terminal: Trigger processing and produce a result (e.g., collect, forEach).

7. 🔹 Examples of Intermediate Operations
```java
List<String> names = List.of("John", "Alice", "Bob", "John");
names.stream()
     .filter(name -> name.startsWith("J"))
     .forEach(System.out::println);
```

8. 🔹 Use of forEach()
   forEach is a terminal operation used to iterate over each element.
```java
List<Integer> numbers = List.of(1, 2, 3);
numbers.stream().forEach(System.out::println);
```

9. 🔹 Creating Streams from Different Data Sources
```java
Stream<Integer> stream1 = Stream.of(1, 2, 3);
Stream<Integer> stream2 = Arrays.stream(new int[]{1, 2, 3});
Stream<String> stream3 = List.of("A", "B").stream();
```

10. 🔹 Converting Stream to Collection
```java
List<Integer> list = Stream.of(1, 2, 3).collect(Collectors.toList());
Set<String> set = Stream.of("A", "B", "A").collect(Collectors.toSet());
```

11. 🔹 What is Stream Pipelining?
   A Stream pipeline consists of intermediate operations (e.g., filter, map) followed by a terminal operation (e.g., collect), allowing method chaining.

12. 🔹 Difference between peek() and map()
   - peek(): Used for debugging (non-terminal).
   - map(): Transforms elements.

13. 🔹 Can a Stream be reused?
   No, once a Stream has been consumed, it cannot be reused.

14. 🔹 How to limit and skip elements in a Stream?
   - limit(n): Processes only the first n elements.
   - skip(n): Ignores the first n elements.

15. 🔹 Stream.of() vs Arrays.stream()
   - Stream.of(): Used for objects.
   - Arrays.stream(): Supports both object and primitive arrays.

-----------------------------------------------------------------

Happy Coding! ☕