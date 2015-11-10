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