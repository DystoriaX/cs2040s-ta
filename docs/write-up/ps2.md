# PS2

## Styling Issues

Most of you do not have this issue, but please at least try to write a readable code.
At the very least:

- Indent properly (very important!)
    - There could be differences in indentation of you mix up `<Tab>` and `<spaces>`.
      Since most of you use IntelliJ for development, you can try to follow
      [this guide](https://www.jetbrains.com/help/idea/indentation.html#detect-indentation)
      to change your indentation settings. I would recommend to use spaces of 4. Please
      check that your submitted program is also indented properly.
- Proper braces (very important!)
    - Even though the if-block has only one line statement, please use braces to
      make it clear the scope of your if block.

      ```java
      if (n < 1) // Use braces...
        System.out.println("Bad");

      if (n < 2) { // Like this
        System.out.println("Good");
      }
      ```

- Meaningful (at least representative) variable names
- No magic numbers (give the number names!)
    - See [Don't Write Comments](https://www.youtube.com/watch?v=Bf7vDBBOBUA&t=207s)
- `camelCase` for variable names and functions
- `CAPITAL_SNAKE_CASE` for constants
- `PascalCase` for class/interface names

If I find your code hard to read due to bad presentation, ***marks will be deducted***.

## Common mistakes

Some of you forget to put the big-O when doing complexity analysis. Note that
this is important. Stating that an algorithm runs in $f(n)$ means that
it takes _exactly_ $f(n)$ steps, when in fact some constant factors might be
involved. Therefore, it is more accurate to write down our complexity using
asymptotic notation. You can use any of big-O, big-Omega, or big-Theta, depends
on what you are trying to convey.

"The algorithm runs in $\mathcal{O}(f(n))$" means that it is upperbounded by
some constant factor of $f(n)$ for large values $n$, i.e. cannot be worse than
$c \cdot f(n), \forall n > n_0$ for some ***positive*** constants $c, n_0$

## Improvement Suggestions

### If-else return

The returning-boolean-if-else functions can be simplified. Compare the following.

```java
boolean isLarger(int a, int b) {
    if (a > b) {
        return true;
    } else {
        return false;
    }
}

boolean betterIsLarger(int a, int b) {
    return a > b;
}
```

### Avoid Nested Code
Nested codes are not recommended in practice as it hurts readability. Two to three
nests are acceptable, but more than that is... bad. You are going to learn this more
later in your software engineering module. Most of the time, it is possible to
refactor (i.e. restructure) your code. For instance, handle all edge cases that
is not part of main logic in if else statement.

Further reference (recommended): [Why you shouldn't nest your code](https://www.youtube.com/watch?v=CFRhGnuXG-4)

### Binary Search Implementation
Some of your binary search implementation could have been improved. The
following is my usual implementation of binary search for lowerbound (i.e. finding
the first index such that `arr[index] >= x`, where `x` is the value of interest and
`arr[]` is a non-decreasingly sorted array).

```java linenums="1"
int lowerBound(int[] arr, int x) {
    int l = 0;
    int r = arr.length - 1;

    while (l < r) {
        int mid = l + (r - l) / 2;

        if (a[mid] >= x) {
            r = mid;
        } else {
            l = mid + 1;
        }
    }

    // at this point, l = r
    return l;
}
```

Some important notes:

- At line 6, it is preferred to do that way instead of `mid = (l + r) / 2`. There
  is a possibility of overflow when we calculating `l + r`. Though chances are
  low, but when it occurs, it will be very frustrating to debug.
- At the end of loop, we can infer that `l` = `r` for two reasons:
    - While loop stops when `l` >= `r`
    - It is not possible for `l` > `r` (you can try to deduce this from revery
      possible branch statements executed)
- Let's consider what `l` points during the loop execution. If we try to visualize what
  is happening during the loop, if `arr[l] < x`, it will always move to right until
  `arr[l] >= x`, and the final value of `l` is the answer, i.e. the first index whose value
  is >= `x`. This is true as we only move `l` to `mid + 1` when `arr[mid] < x`.
  This implies that either:
    - `arr[mid + 1] < x`, which means that the value `l` will continue to change again
    - `arr[mid + 1] >= x`, this means that `mid + 1` = `l` is the first index whose
      value is >= `x`. At this point, `l` will never change its value again.
- From the reasoning above, we can conclude that `arr[l] >= x` and `l` is the answer.
- If you want to handle the case where there is no `index` such that `arr[index] >= x`,
  initialize `r` to `arr.length`. If the function returns `arr.length`, then there is
  no such index. Think why this works.

## Questions to Ponder

- On my binary search implementation, what is my pre-condition, loop invariant,
  and post-condition?
