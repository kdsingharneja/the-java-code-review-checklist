# The Java Code Review Checklist

A code review guide and checklist when working with Java and related technologies. The following should really help when writing new code in Java applications after upgrading to Java 8 or refactoring code that is < Java8

# Core Java 
The following should 

## Prefer Lambdas

Instead of 

```
Runnable runner = new Runnable(){
    public void run(){
        System.out.println("I am running");
    }
};
```

do...

```
Runnable running = () -> {
    System.out.println("I am running");
};
```

## Refactor interfaces with default methods

Instead of 

```
public class MyClass implements InterfaceA {
 
    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        // TODO code application logic here
    }
 
    @Override
    public void saySomething() {
        System.out.println("Hello World");
    }
 
}
 
interface InterfaceA {
  public void saySomething(); 
 
}
```

Use default methods. Make sure you do not do this as a a habit because this pattern pollutes interfaces.

```
public class MyClass implements InterfaceA {
 
    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        // TODO code application logic here
    }
 
    @Override
    public void saySomething() {
        System.out.println("Hello World");
    }
 
}
 
interface InterfaceA {
 
    public void saySomething();
 
    default public void sayHi() {
      System.out.println("Hi");
    }
 
}
```

## Prefer Streams to reduce code.

```
private static void printNames(List persons, Predicate predicate) {
            persons.stream()
                    .filter(predicate)
                    .map(p -> p.getName())
                    .forEach(name -> System.out.println(name));
        }
}
```

## Use Parallel sorting

Instead of 

```
Array.sort(myArray);
```

Use...

```
Arrays.parallelSort(myArray);
```

## Depend on parameter reflection

Instead of...

```
Person getEmployee(@PathParam("dept") Long dept, @QueryParam("id") Long id)
```

Do...

```
Person getEmployee(@PathParam Long dept, @QueryParam Long id)
```

Since params names as same as var names.

## Prefer to use "filter / map / reduce" approach

```
List<String> names = Arrays.asList("Smith", "Adams", "Crawford"); 
List<Person> people = peopleDAO.find("London"); 
  
// Using anyMatch and method reference 
List<Person> anyMatch = people.stream().filter(p -> (names.stream().anyMatch(p.name::contains))).collect(Collectors.toList()); 
  
// Using reduce 
List<Person> reduced = people.stream().filter(p -> names.stream().reduce(false (Boolean b, String keyword) -> b || p.name.contains(keyword), (l, r) -> l | r)).collect(Collectors.toList()); 
```
