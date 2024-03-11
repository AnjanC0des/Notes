## "Java 8 features by coding it" Course notes on udemy

* Used declarative way of coding using Instream to find the sum in a range and find the unique elements in a List.
* Used lambda functions(similar to lambda functions in es6) to init comparator and runnable instead of making anonymous classes using the new keyword.

```java
// sum of integers for the range from 0 to 100
/**
 * Imperative Style - how style of programming
 */
int sum=0;
for(int i=0;i<=100;i++){
        sum+=i; // shared mutable state and its sequential anf it will go step by step
            // and it will have issues if we try to run the code in multithreaded environment
}
System.out.println("Sum is : "+sum);


/**
 * Declarative style. (Functional programming uses the same style)
 * what style of programming.
 * You let the system do the job for you and get the result.
 */
int sum1= IntStream.rangeClosed(0,100)
        //.parallel()
        .map(Integer::new)
        .sum();

System.out.println("sum1 : " + sum1);
```

```java
List<Integer> integerList =Arrays.asList(1,2,3,4,4,5,5,6,7,7,8,9,9);
/**
 * Imperative Style
 */
List<Integer> uniqueList = new ArrayList<>();
for(Integer i :integerList)
    if(!uniqueList.contains(i)){
    uniqueList.add(i);
    }
System.out.println("unique List : " + uniqueList);
/**
 * Declarative Syle
 */
List<Integer> uniqueList1 = integerList.stream()
        .distinct()
        .collect(toList());
System.out.println("uniqueList1 : " + uniqueList1);
```

```java
import java.util.Comparator;
public class Main {
  public static void main(String[] args) {
    Comparator<Integer> comp=(a,b)->a.compareTo(b);
    System.out.println(comp.compare(4,2));
  }
}
```
