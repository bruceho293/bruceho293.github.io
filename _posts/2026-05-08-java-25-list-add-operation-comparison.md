---
layout: post
title: "Java 25 - List Add operation comparision"
description: "Comparison in add operation between ArrayList and other implementations"
date: "2026-05-08 15:15:00"
categories: backend
tag: [java]
---

## Objective
During my time working with Java as my main programming language, I have taken for granted that ArrayList would be the most optimal implementation for the List interface so in this post, I will run some measurement with the `System.nanoTime()` to compare `ArrayList` with `LinkedList` and `Stack`.

The setup is based on my personal experience testing with Java 25 in my personal Windows machine. 
The result might be different in other OS system and the results in this posts are not 100% accurate.

## Setup
In this setup, I would compare ArrayList with LinkedList and Stack. For the data, I will first use the following types: Integer, String and Map.

```java
public class PlaygroundApplication {

	public static void main(String[] args) {

		List<Long> duration = new ArrayList<>();
		int repetitions = 100;
		int[] sizeChosen = {1, 1000, 1000000};

		List<Integer> list = new ArrayList<>();
		for (var i = 0; i < repetitions; i++){
			IO.println("Warming up in " + (repetitions - i));
		}
		for (var j = 0; j < repetitions; j ++){
			long startTime = System.nanoTime();
			int size = sizeChosen[2];
			for (var i = 0; i < size; i ++) {
				list.add(i);
			}
			duration.add(System.nanoTime() - startTime);
			list.clear();
		}


		IO.println("Duration: " + getMedian(duration));
	}

	public static double getMedian(List<Long> list) {
		if (list == null || list.isEmpty()) return 0.0;

		List<Long> sortedList = new ArrayList<>(list);
		Collections.sort(sortedList);
		int size = sortedList.size();

		// Even size: average of the two middle elements
		if (size % 2 == 0) {
			return (sortedList.get(size / 2 - 1) + sortedList.get(size / 2)) / 2.0;
		}
		// Odd size: the middle element
		else {
			return sortedList.get(size / 2);
		}
	}

} 
```
Let me explain about the setup for my quick comparision. First I want to warm up the JVM as much as possible to help removing the startup time as well as any dead code duration. Next, I would repeat the process a fixed amount of times and then take the median value of all the duration as the final result.

For each permutation of the setup, I would execute the codes 2 to 3 times to get the most frequent value.

For the String value, I would use UUID to generate a random UUID string.
```java
for (var j = 0; j < repetitions; j ++){
  long startTime = System.nanoTime();
  int size = sizeChosen[0];
  for (var i = 0; i < size; i ++) {
    list.add(UUID.randomUUID().toString());
  }
  duration.add(System.nanoTime() - startTime);
  list.clear();
}
```

For the Map value, I generate a simple Map object
```java
Map<String, String> map = Map.of("id", "1", "sessionId", UUID.randomUUID().toString());
```

## Comparision Result
### Data Type - Integer

| Implementation | 1 Element (ns) | 1,000 Elements (ns) | 1,000,000 Elements (ns) |
| :--- | :---: | :---: | :---: |
| **ArrayList** | 200 | 47,800| 9,276,800|
| **LinkedList** | 200 | 51,600 | 13,558,300 |
| **Stack** | 200  | 55,650 | 22,181,200 |

### Data Type - String

| Implementation | 1 Element (ns) | 1,000 Elements (ns) | 1,000,000 Elements (ns) |
| :--- | :---: | :---: | :---: |
| **ArrayList** | 100 | 30,500 | 8,966,550 |
| **LinkedList** |200 | 32,350 | 9,482,100 |
| **Stack** | 100 | 33,900| 21,657,650 |

### Data Type - Map

| Implementation | 1 Element (ns) | 1,000 Elements (ns) | 1,000,000 Elements (ns) |
| :--- | :---: | :---: | :---: |
| **ArrayList** | 100 | 30,500 | 8,722,650 |
| **LinkedList** | 200 | 34,800 | 9,151,200 |
| **Stack** | 100 | 35,550 | 21,531,700 |

## Conclusion
It seems in this context, ArrayList remains the optimal solution when using with the List interface. In the future I might cover other operations but for now, please excuse me as I will dive into more in the `ArrayList` implementation.
