title: Scala via Ruby
author:
  name: Lloyd
  twitter: meta_lloyd
  github: lloydmeta
  url: https://beachape.com
output: index.html
theme: sudodoki/reveal-cleaver-theme
controls: true

--

# Scala via Ruby
[beachape.com/scala-via-ruby](http://beachape.com/scala-via-ruby)

--

## Overview

1. Things Rubyists ♥ in Ruby
2. Things Rubyists might ♥ in Ruby
3. Scala overview
4. Scala similarities w/ Ruby
5. Things Rubyists might ♥ in Scala

--

![Ruby](imgs/ruby.png)

--

### Things Rubyists ♥ in Ruby

* REPL
* Malleable
* Functional programming support
* Terse (very little typing)
* Expressive

--

### Things Rubyists ♥ in Ruby: Malleable

* Easily extendable:
  ```ruby
class String
    def truthy
      self == "true"
    end
end
"hello".truthy
  ```
* Duck typing
  ```ruby
my_thing.respond_to?(:to str)
  ```
* Metaprogramming (eg. `:define_method`)

--

### Things Rubyists ♥ in Ruby: Functional programming support

* `fold`, `map`, `each`, `select`
  ```ruby
values = (1..100)
values.select { |i| i % 5 == 0 }.map { |i| i * 5 }.take(3)
# vs
temp = # ...
for i := 0; i < 10; i++ {
    if values[i] % 5 == 0
     # kill me now
}
  ```
* anonymous functions ("lambdas")
  ```ruby
long = lambda { |a, b| a + b }
long.call(2, 3)
  ```

--

### Things Rubyists ♥ in Ruby: Terse

```ruby
class Car
  attr_accessor :max_speed, :max_people
end
```

vs

```java
public class Car {
  private int maxSpeed;
  private int maxPeople;

  public int getMaxSpeed {
    return maxSpeed;
  }

  public void setMaxSpeed(int speed) {
    maxSpeed = speed;
  }

  public int getMaxPeople {
    return maxPeople;
  }

  public void setMaxPeople(int people) {
    maxPeople = people;
  }

}

```

--

### Things Rubyists ♥ in Ruby: Expressive

#### DSL paradise:
* Cucumber
* RSpec
* Capybara

--

### Things Rubyists might ♥ in Ruby

* Better predictability (easy to reason about)
  * Immutability (references + structures)
  * Make extensions obvious/controlled
* Better Concurrency support
* Type system
* Better lazy support
* Better refactoring support

--

# Scala

![Scala](imgs/scala.png)

--

### Scala overview

- Multiparadigm (OOP + FP), strongly-typed
- Type inference
- Designed to make concurrency easy: immutability
- Runs on the JVM with compile-to Javascript support

--

### Scala similarities w/ Ruby

* REPL
* Malleable
* Functional programming support
* Terse (very little typing)
* Expressive

:D

--

### Scala similarities w/ Ruby: Malleable

* Easily extendable:
  ```scala
object RichString {
    implicit class StringOps (val s: String) extends AnyVal {
        def truthy = s == "true"
    }
}
import RichString._
"hello".truthy
  ```
* Duck typing
  ```scala
def quacker(duck: {def quack(value: String): String}) {
  ```
* Type classes
* Metaprogramming via Macros

--

### Scala similarities w/ Ruby: FP support

* `map`, `filter`, `fold`
  ```scala
(1 until 100).filter { _ % 5 == 0 }.map { _ * 5 }.take(3)
  ```
* anonymous functions ("lambdas")
  ```scala
val f = { (a: Int, b: Int) => a + b }
f(1,2)

  ```

--

### Scala similarities w/ Ruby: Terse

```scala
case class Car(maxPeople: Int, maxSpeed: Int)
```

--

### Scala similarities w/ Ruby: Expressive

* Also DSL paradise
* Can drop `.` for invocations
  ```scala
(1 until 100) filter {_ % 5 == 0 } map { _ * 5 } take 3
  ```
* Spray, ScalaTest, Spec2, etc
* ScalaTags for typed HTML

```scala
html(
  head(
    script(src:="..."),
    script(
      "alert('Hello World')"
    )
  ),
  body(
    div(
      h1(id:="title", "This is a title"),
      p("This is a big paragraph of text")
    )
  )
)

```

--

### Things Rubyists might ♥ in Scala

* Predictability (easy to reason about)
  * Immutability (references + structures)
  * Make extensions obvious/controlled
* Concurrency as a 1st class citizen
* Type system w/ inference
  * Checked at compile time
* Lazy support
* Easy refactoring

--

### Things Rubyists might ♥ in Scala: Predictability

* Controlled monkey patching via imports
  * [No more freedom patch problems](http://tenderlovemaking.com/2013/05/21/one-danger-of-freedom-patches.html)
* Immutable references and data strutures out of the box
  ```scala
val x = 3
x = 4 // => compile error
val stuff = IndexedSeq("a", "b", "c")
stuff(0) = "d" // => compile error
  ```

--

### Things Rubyists might ♥ in Scala: Concurrency

* Composable `Future`s
  ```scala
val fAsyncCalc= Future { 1 + 1 }
val fTransformed = fAsyncCalc.map { i => doWithResult(i) }
fTransformed.foreach { i => println(i) }
  ```
* Built in concurrency abstractions + immmutability + predictability → awesome

--

### Things Rubyists might ♥ in Scala: Type inference

* As you saw, in the previous slide, we didn't declare *any* types
* Yet, everything is checked at compile time, so if `doWithResult` needed a `String` argument, the compiler would throw an error

--

### Things Rubyists might ♥ in Scala: Laziness

* Lazy references
  ```scala
lazy val result = expensiveOp // memoisation on demand
  ```
* Lazy objects: `object` is lazily instantiated on first use
* Lazy data structures: `Stream` is a lazy collection
* Call by name parameters
  ```scala
def method(actuallyUseA: Boolean, expensiveA: => Int) // expensiveA is called lazily
  ```

--

### Things Rubyists might ♥ in Scala: Nicer refactoring

* Static types + controlled extension → the IDE can be very helpful in refactoring

--

### Other Things Rubyists might ♥ in Scala

* [Performance](http://benchmarksgame.alioth.debian.org/u64q/compare.php?lang=scala&lang2=yarv)
* Pattern matching
  ```scala
case class User(firstName: String, lastName: String, score: Int)
def advance(xs: List[User]) = xs match {
    case User(_, _, score1) :: User(_, _, score2) :: _ => score1 - score2
    case _ => 0
}
  ```
* Tail call optimisation (checked via `@tailrec`)

--

## Conclusion

* If you like Ruby you might like Scala; they're more similar than you think

--

## Resources

* [Programming in Scala](http://www.amazon.com/Programming-Scala-Comprehensive-Step---Step-ebook/dp/B004Z1FTXS/ref=sr_1_1?s=books&ie=UTF8&qid=1432262060&sr=1-1&keywords=scala+programming)
* [Functional Programming on Coursera](https://www.coursera.org/course/progfun)
* [Reactive Programming on Coursera](https://www.coursera.org/course/reactive)

--

## Questions?

--

If you can't switch to Scala now, you might want to take a look at [Octoparts](https://beachape.com/octoparts-intro)
