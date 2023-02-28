# PS4

## Things to Note

- Some of you have redundant checks, which could have/should have been handled by the base case. I have put comments for those who had this issue. When designing recursive function, do ask yourself:
    - Are there any better base case? Having a better base case will help simplify unnecessary if branch checks when you recurse further down the function.
    - Are there any better way to represent the recurrence relation? (e.g. for `rebuild`, is it easier to design recursive function for a `node` or `children`)
- For `rebuild` function, some of you copy the whole array of `TreeNode`. Note that this is not recommended! Arguably, it is easier for you to think of rebuilding for an array of `TreeNode`. However, copying over the content is not a good idea as copying itself takes linear time. This unnecessary cost will make the function slower. You can pass the original array on the function and use pointers instead.
- For those whom I suggested to use wrapper type `Integer` instead of the primitive type `int`, please ignore. I just realized that the wrapper class does not pass the argument by reference.
- For question 1b (Enumerate Nodes) Some of you attempted the following:
    - Using `int[]` to pass by reference. A hacky way to do it :)
    - Using member variable to keep track of index for inorder traversal array. A nicer solution :), but you need to remember to reset the value to `0` for every function calls on `enumerateNodes`!

Note: some programming languages support referring to subarray in $\mathcal{O}(1)$ time, i.e. it does not copy the whole array. You can implement one on your own, too! See an implementation of [`ImmutableArray`](https://nus-cs2030s.github.io/2122-s2/28-immutability.html#enabling-safe-sharing-of-internals) in Java. You might learn this in your CS2030S as well :)

## Additional Challenges

- Problem 1b (Enumerate Nodes) can be solved either iteratively or recursively. Do give it a try :)
