# scalanote

## Functional

- A Scala function(function and method) is essentially a Java method
- A Scala function will be specified with: `private static final`
- Special characters can be used to name functions

### Variable function
```scala
def variableFun(names: String*): Unit = {
  println(names)
}
```

### Default value
```scala
def defaultVal(name : String = "default name", age : Int): Unit = {
  println(s"register age: ${age}, name: ${name}")
}

// specify name to change the sequence
defaultVal(age = 18)
```

### Anonymous functions
The Principle of Simplicity can be applied when anonymous function is a parameter
```scala
def anoFun(f: (Int, Int) => Int): Unit = {
  println(f(10, 20))
}

def anoFun(f : Int => Int) : Unit = {
  println(f(3))
}

// 1, Omit the braces if the method body has just one expression
anoFun(
  (x : Int, y : Int) => x + y
)

// 2, Omit the parameter type if the type can be inferred
anoFun(
  (x, y) => x + y
)

// 3, Omit parenthesis if there is only one parameter
anoFun(
  x => x * 10
)

// 4, Parameters can be replaced with underlines if they are used once in sequence
anoFun(_ + _)
```
#### A function can be used as a return result
```scala
def out(): Unit = {
  def inner(): Unit = {
    
  }
  inner_
}

// f is a function object () => Unit
var f = out()

// something crazy
def outer(x : Int) = {
  def mid(f: (Int, Int) => Int) =  {
    def inner(y : Int) = {
      f(x, y)
    }

    inner _
  }

  mid _
}

// 30
var res = outer(10)(_ + _)(20)
```
### Closures
- Before Scala 2.12, closures is implemented with anonymous functions, while it is implemented by changing the signatures of the functions after Scala 2.12, closure
- Usage scenarios
    - An inner function uses outer variables which changes the life cycle of the variables
    - A function is used as a function object which changes the life cycle of the function
    - All anonymous functions
    - Return a function object in a function
```scala
  def outer(x: Int) = {
    def inner(y: Int) = {
      x + y
    }
    inner _
  }

  var inner = outer(10)
  var res = inner(20)
  println(res)
```
![Pasted Graphic 8.png](..%2F..%2FLibrary%2FGroup%20Containers%2Fgroup.com.apple.notes%2FAccounts%2F91446127-E8D3-43F3-908A-052A1D073119%2FMedia%2FC7374F59-0F80-4DC5-9F42-BCC6C4D85C94%2FPasted%20Graphic%208.png)

### Control abstraction
Use code as a parameter, can be used to define grammar since you can change the logics through the code(try-catch)
```scala
breakable {
  for ( i <- 1 to 5) {
    if (i == 3) {
      break
    }
    println(s" = ${i}")
  }
}
```

### Function currying

Simplify the function, separate the parameters, support multiple parameters, decouple the unrelated parameters

```scala
  def fun(a: Int, b: Int): Unit = {
  for (i <- 0 to a) {
    println(i)
  }

  for (i <- 0 to b) {
    println(i)
  }
}

// have to fill in all parameters
fun(10, 20)

def curryFun(a: Int)(b: Int): Unit = {
  for (i <- 0 to a) {
    println(i)
  }

  for (i <- 0 to b) {
    println(i)
  }
}

// fill in parameter separately
val intToUnit : Int => Unit = curryFun(10)

curryFun(10)(20)
```

### Recursion
Scala uses tail recursion to optimize stack overflow (using while(true))
```scala
def tailRecursion(): Unit = {
  tailRecursion()
}

tailRecursion()
```

### Lazy function
```scala
  def lazyFun(): String = {
    println("lazy function")
    "Lazy..."
  }
  
  lazy val str = lazyFun()
  println("233333")
  println(str)
```