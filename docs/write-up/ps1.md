# PS1

## Styling Issues
I noticed many of you are not accustomed to the standard styling of Java. You
are going to learn that in CS2030S, but I would like to highlight some important
guides that I found: member variable and method names should use `camelCase`.
If your constructor has the same variable names with the member variables', you
can refer to member variable with `this.memberVariable`.

```java
class Cat {
  private String name;
  private int age;

  public Cat(String name, int age) {
    this.name = name;
    this.age = age;
  }
}
```

Don't forget that member variables should be `private`, as we do not want
external user to modify a property of our object. Methods should usually be
`public` unless you do not want external user to call the method (typically
helper functions).

## Trivia
If it is possible to work only with integers, we prefer to do so if precision
is of concern. Note that working with floating-point number implies that we
sacrifices our precision.

## Reflection
Most of you initialized the seed (which is an array) using assignment (i.e.
`this.seed = seed`). Do you think this is a good idea? If not, why?

??? question "Reveal answer"

    Array type in Java is a reference type. It means that if we do an assignment
    from a variable to another, they share the same reference to the same entity.
    Consequently, if one variable change its value, the effect will apparent to
    other values who share the same reference. Try run this code on `jshell`

    ```java linenums="1"
    int[] a = {1, 2, 3};
    int[] b = a;
    a[0] = 10;
    a; // returns {10, 2, 3}
    b; // returns {10, 2, 3}, too! :(
    ```

    After modification in line 3, you would expect that the value of `b` should
    not change. In fact, at line 5, the value of `b` changes too!

