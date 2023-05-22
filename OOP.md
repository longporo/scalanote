# OOP

## Package

- The keyword 'package' can be declared multiple times(from up to bottom) to show the different package relationships while Java implements using '.'
- Scope can be used in packages to show the hierarchy
- A package can be defined as an object. The attributes and functions in the package object can be accessed in current context and its sub packages
- The package name is not related to the physical path

```scala
  package com
  package my
  package scala
  package note {
  
    package oop {
      object oopObj {
        def main(args: Array[String]): Unit = {
          test()
        }
      }
    }
  
    package object oop {
      def test(): Unit = {
        println("test fun")
      }
    }
  }
```

### Import

#### Import package
```scala
  import com.my.scala.note.oop.test
  test()
```

### Import can be used anywhere, only works in current scope
```scala
  import java.util.Date
  val date = new Date()
```

### Import all class(as '*' in Java)
```scala
  import java.util._
  new ArrayList()
```

#### Import multiple classes
```scala
  import java.util.{List, ArrayList, Map, HashMap}
```

### Exclude certain classes
```scala
  import java.util._
  import java.sql.{Date => _, _}
  new Date()
```

### Set another name for a class
```scala
  import java.util.{HashMap => JavaHashMap}
  val map = new JavaHashMap()
```

### Import rule: based on current package, search from the specified sub packages, if nothing is found, search from super packages
```scala
  println(new _root_.java.util.HashMap())
```

### Something do not need to be imported
- Packages: java.lang, scala
- All functions in Predef object(static import)