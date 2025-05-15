## 🟢 Intermediate Level Questions

## 1. How can you perform filtering using Java Streams?
You can use the `filter()` method to filter elements based on a condition:

```java
List<String> names = Arrays.asList("Alice", "Bob", "Amanda");
List<String> filtered = names.stream()
    .filter(name -> name.startsWith("A"))
    .collect(Collectors.toList());
```

## 2. Explain how map() works in Java Streams. Provide an example.
`map()` transforms each element of the stream and returns a new stream:

```java
List<String> names = Arrays.asList("alice", "bob");
List<String> upper = names.stream()
    .map(String::toUpperCase)
    .collect(Collectors.toList());
```

## 3. What is the difference between map() and flatMap()?
- `map()` is used to transform elements one-to-one.
- `flatMap()` is used to transform elements into a stream of elements and flattens them into a single stream.

Example:
```java
List<String> words = Arrays.asList("Hello", "World");
List<String> letters = words.stream()
    .map(w -> w.split(""))             // Stream<String[]>
    .flatMap(Arrays::stream)           // Stream<String>
    .collect(Collectors.toList());
```

## 4. How can you find duplicates using Streams?

```java
List<Integer> list = Arrays.asList(1, 2, 3, 2, 4, 1);
Set<Integer> seen = new HashSet<>();
List<Integer> duplicates = list.stream()
    .filter(e -> !seen.add(e))
    .collect(Collectors.toList());
```

## 5. Write a Stream program to count the frequency of characters in a String.

```java
String input = "banana";
Map<Character, Long> freq = input.chars()
    .mapToObj(c -> (char) c)
    .collect(Collectors.groupingBy(c -> c, Collectors.counting()));
```

## 6. Explain the concept of Collectors and some commonly used ones.
Collectors are utility functions that accumulate elements into collections or summaries:
- `Collectors.toList()` – collects stream into a List
- `Collectors.toSet()` – collects into a Set
- `Collectors.joining()` – concatenates stream of strings
- `Collectors.groupingBy()` – groups elements by a classifier function

Example:
```java
Map<String, List<Employee>> groupedByDept = employees.stream()
    .collect(Collectors.groupingBy(Employee::getDepartment));
```

## 7. How do you remove null values from a list using Streams?

```java
List<String> namesWithNulls = Arrays.asList("Alice", null, "Bob", null);
List<String> cleaned = namesWithNulls.stream()
    .filter(Objects::nonNull)
    .collect(Collectors.toList());
```

## 8. How can you sort a list of objects using Streams?

```java
List<Employee> sortedBySalary = employees.stream()
    .sorted(Comparator.comparing(Employee::getSalary))
    .collect(Collectors.toList());
```

## 9. Write a Stream program to find the second highest number from a list.

```java
Optional<Integer> secondHighest = numbers.stream()
    .sorted(Comparator.reverseOrder())
    .distinct()
    .skip(1)
    .findFirst();
```

## 10. How can you find the sum and average of numbers using Streams?

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.stream().mapToInt(Integer::intValue).sum();
double average = numbers.stream().mapToInt(Integer::intValue).average().orElse(0);
```

### 11. How do you merge two lists using Streams?
```java
List<String> merged = Stream.concat(list1.stream(), list2.stream())
    .collect(Collectors.toList());
```

### 12. How do you check if any/all/none of the elements match a condition?
```java
boolean anyMatch = list.stream().anyMatch(e -> e > 10);
boolean allMatch = list.stream().allMatch(e -> e != null);
boolean noneMatch = list.stream().noneMatch(e -> e < 0);
```

### 13. How can you convert a list of strings to a comma-separated string?
```java
String joined = list.stream().collect(Collectors.joining(", "));
```

### 14. How to count total number of elements after filtering?
```java
long count = list.stream().filter(e -> e.startsWith("A")).count();
```

### 15. How do you find max/min value from a list using Streams?
```java
Optional<Integer> max = numbers.stream().max(Integer::compareTo);
Optional<Integer> min = numbers.stream().min(Integer::compareTo);
```

-----------------------------------------------------------------

Happy Coding! ☕