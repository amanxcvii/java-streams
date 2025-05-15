## 🟢 Advance Level Questions

## 1. How would you handle exceptions inside a Stream pipeline?
Streams don’t support checked exceptions directly. You can handle them using wrapper methods or try-catch inside lambdas (for unchecked exceptions):

```java
List<String> list = Arrays.asList("1", "2", "a");

List<Integer> result = list.stream()
    .map(s -> {
        try {
            return Integer.parseInt(s);
        } catch (NumberFormatException e) {
            return 0; // or handle differently
        }
    })
    .collect(Collectors.toList());
```

## 2. Explain the concept of reduce() with examples.
The reduce() method performs a reduction on elements of the stream using an identity value and a BinaryOperator:

```java
int sum = Stream.of(1, 2, 3, 4)
    .reduce(0, Integer::sum);

String combined = Stream.of("a", "b", "c")
    .reduce("", String::concat);
```

## 3. How is Optional used with Streams to handle null values?
Optional helps avoid NullPointerException. Useful in terminal operations like findFirst, findAny, min, max:

```java
Optional<String> first = Stream.of("apple", "banana")
    .filter(s -> s.startsWith("a"))
    .findFirst();

first.ifPresent(System.out::println);
```

## 4. Can you perform file operations using Streams in Java? Provide an example.
Yes, you can use Files.lines() or BufferedReader.lines():

```java
try (Stream<String> lines = Files.lines(Paths.get("file.txt"))) {
    lines.filter(line -> line.contains("error"))
        .forEach(System.out::println);
} catch (IOException e) {
    e.printStackTrace();
}
```

## 5. Explain the difference between findFirst() and findAny().
- findFirst(): Returns the first element of the stream (deterministic).
- findAny(): May return any element, better performance with parallel streams (non-deterministic).

```java
Optional<String> first = list.stream().findFirst();
Optional<String> any = list.parallelStream().findAny();
```

## 6. What are some performance considerations when using Streams?
- Avoid unnecessary operations (e.g. multiple sorts).
- Prefer primitive streams (IntStream, LongStream) to avoid boxing.
- Use parallelStream with care – it can degrade performance for small tasks or unordered collections.
- Avoid using stateful lambda expressions (e.g., shared mutable state).

## 7. Describe how to implement parallel processing using Streams.
Use parallelStream() or stream().parallel():

```java
List<Integer> numbers = IntStream.range(1, 1_000_000).boxed().collect(Collectors.toList());

long count = numbers.parallelStream()
    .filter(n -> n % 2 == 0)
    .count();
```

## 8. Write a program to find the most repeated word in a paragraph using Streams.

```java
String paragraph = "apple banana apple orange banana apple";

String mostRepeated = Arrays.stream(paragraph.split(" "))
    .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
    .entrySet().stream()
    .max(Map.Entry.comparingByValue())
    .map(Map.Entry::getKey)
    .orElse(null);
```

## 9. How can you merge multiple Streams into one?

```java
Stream<String> merged = Stream.of(stream1, stream2, stream3)
    .flatMap(Function.identity());
```

## 10. Explain the use of Stream.generate() and Stream.iterate() for infinite streams.
- Stream.generate(): Takes a Supplier and generates infinite stream.
- Stream.iterate(): Takes a seed and UnaryOperator to produce successive elements.

```java
Stream<Integer> ones = Stream.generate(() -> 1).limit(5); // 1, 1, 1, 1, 1

Stream<Integer> evens = Stream.iterate(0, n -> n + 2).limit(5); // 0, 2, 4, 6, 8
```

---

## 🔁 Additional Advanced Questions to Practice:

### 11. How do you create a custom Collector?
A custom collector is created using the Collector.of() method. It requires a supplier, accumulator, combiner, and finisher.

Example: Collect elements into a LinkedList

```java
Collector<String, ?, LinkedList<String>> toLinkedList =
    Collector.of(
        LinkedList::new,                // Supplier
        LinkedList::add,                // Accumulator
        (left, right) -> {              // Combiner
            left.addAll(right);
            return left;
        },
        Collector.Characteristics.IDENTITY_FINISH
    );

List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
LinkedList<String> result = names.stream().collect(toLinkedList);
```

### 12. How to use StreamEx or third-party libraries to extend Stream features?
StreamEx (from the stream-ex library) is an enhanced version of Java Streams that offers additional functionality.

Example: Using StreamEx to zip two lists

```java
import one.util.streamex.StreamEx;

List<String> names = List.of("Alice", "Bob", "Charlie");
List<Integer> scores = List.of(90, 85, 88);

List<String> result = StreamEx.zip(names, scores, (name, score) -> name + ": " + score)
                              .toList();

// Output: ["Alice: 90", "Bob: 85", "Charlie: 88"]
```

StreamEx also simplifies operations like distinct by key, joining indexed streams, filtering with indices, and more.

### 13. How to convert a Stream to a ConcurrentMap?

```java
Map<String, Integer> map = list.stream()
    .collect(Collectors.toConcurrentMap(Function.identity(), String::length));
```

### 14. How to group by and summarize statistics in one pass?
```java
Map<String, IntSummaryStatistics> stats = employees.stream()
    .collect(Collectors.groupingBy(Employee::getDepartment,
        Collectors.summarizingInt(Employee::getSalary)));
```

### 15. How do you avoid modifying state inside a stream operation (side-effects)?
Avoid shared variables. Prefer pure functions:
```java
// BAD: shared state mutation
AtomicInteger count = new AtomicInteger();
list.stream().forEach(e -> count.incrementAndGet());

// BETTER: use count() or collect
long count = list.stream().count();
```

-----------------------------------------------------------------

Happy Coding! ☕