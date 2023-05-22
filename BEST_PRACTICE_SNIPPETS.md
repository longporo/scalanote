

# Snippets from [Functional Programming Principles in Scala](https://www.coursera.org/learn/scala-functional-programming/home/module/1)

## Merge sort
```scala
def msort(xs: List[Int]): List[Int] = {
  val n = xs.length / 2
  if n == 0 then xs
  else {
    val (fst, snd) = xs.splitAt(n)
    merge(msort(fst), msort(snd))
  }
}

def merge(xs: List[Int], ys: List[Int]): List[Int] =  (xs, ys) match
  case (Nil, ys) => ys
  case (xs, Nil) => xs
  case (x :: xs1, y :: ys1) => {
    if x < y then x :: merge(xs1, ys)
    else y :: merge(xs, ys1)
  }

// parameterize msort so that it can also be used for lists with elements other than Int
def msort[T](xs: List[T])(lt: (T, T) => Boolean) = {
  ...
    merge(msort(fst)(lt), msort(snd)(lt))
}

def merge[T](xs: List[T], ys: List[T]) = (xs, ys) match
    ...
    case (x :: xs1, y :: ys1) =>
        if lt(x, y) then ...
        else ...

// call msort as follows
val xs = List(-5, 6, 3, 2, 7, 8)
val fruits = List("apple", "pear", "orange", "pineapple")

msort(xs)((x, y) => x < y)
msort(fruits)((x: String, y: String) => x.compareTo(y) < 0)
```