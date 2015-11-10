# The Java Code Review Checklist

A code review guide and checklist when working with Java, Spring and related technologies

# Core Java 

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

# Spring 

Coming soon...
