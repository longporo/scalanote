# scalanote

## Functional programming language

- A Scala function(function and method) is essentially a Java method
- A Scala function will be specified with: `private static final`

### Add default value to a function parameter
```scala
def defaultVal(name : String = "default name", age : Int): Unit = {
  println(s"register age: ${age}, name: ${name}")
}

// specify name to change the sequence
defaultVal(age = 18)
```
