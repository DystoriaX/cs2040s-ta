# PS3

## Things to Note

- Ensure that you do not print anything to `stdout`, such as using `System.out.println`. If you use it for debugging purpose, please remember to remove it before submitting.
- Sometimes you comment out code that is not used. Make sure you also remove that before submission. It helps me to grade your work easier :)
- Your code has to pass all test cases, public and private! If it doesn't, then most likely your solution is incorrect, or there are missing files.
- Start early, if possible :")

## Common Mistakes

- You cannot ***compare*** the performance of two algorithms/sorters just by looking at the cost! A $\mathcal{O}(n \lg n)$ algorithm does not always perform worse than $\mathcal{O}(n)$ algorithm for all input sizes $n$. It also depends with the ***hidden*** constant involved. You can look at T3 Q5.
- To determine whether an algorithn runs in $\mathcal{O}(n^2)$, you need analyse the growth of the cost, i.e. testing for input size $k$, $2k$, $4k$, $8k$, and so on. Compare how much the cost grows. In this case, you should expect the cost growth is $2^2=4$ times more than the previous one.
- Some of you argue that the best running time and the worst running time by comparing the *significant* difference of the cost. This is kinda valid, but I would suggest that use the analysis method as written in point 2.
- The term of worst case and best case are unique for each algorithm. Hence, you ***cannot*** assume that reversed sorted array is the worst case for ***all*** sorting algorithms! For instance, it might not be the worst case for QuickSort, as the worst case for QuickSort is when the pivot choice is horrible (uneven partition).

## Possible Improvements

- Some of you tried to hardcode when check for a sorter's stability. Note that as long as we generate sufficient repeating element, it should be okay. You can generate an array whose element ranging from `0` to `size / 2`, where `size` is the array size.
- Be aware of edge cases, i.e. checking for array of size `0` or `1`.
- Do extensive testing! Be your own adversary. This is the key for you to get better in anything.
