# General Java Questions
### Core Java Features
- Object oriented
- Inheritance
- Encapsulation
- Polymorphism
- Abstraction
- Platform independent
- High performance
- Multi-threaded
- Pass-by-value

### Primitives
Because of these primitive types, Java is not strictly object-oriented:

- `byte`
- `string`
- `int`
- `float`
- `char`
- `double`
- `boolean`
- `long`

These often get wrapped in *Wrapper classes*, which convert primitives to reference types (objects).

### Volatile Keyword
In Java, each thread has its own stack including its own copy of any variables it can access. When the thread is created, it copies the value of all accessible variables into the stack.

The `volatile` keyword tells the JVM that this variable might be modified in another thread - so the thread is forced to read it directly from memory rather than using the cached value.

### Classloader
Part of the runtime environment that loads classes on demand (lazily loading) into the JVM. 
1) Bootstrap classloader - loads core Java API files
2) Extension classloader - loads JAR files from folder
3) Application classloader - loads JAR files from path specified in CLASSPATH env variable

### String Pool
```java
String string = "Hello"
String string = new String("Hello")
```

First option is more efficient, because a `String` with value `Hello` will be created in the String pool. If another string with the same value is created, it will reference the same object.

Calling `new String("...")` creates a `String` with value `Hello` in the String pool, and that string is then passed to the `String` constructor. This creates another `String` object which is _not_ in the String pool. Each call therefore creates a new object rather than just reusing an object from the pool.

