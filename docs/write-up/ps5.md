# PS5

## Common Mistakes

- For Q2, some of you tried to find highest unbalanced node _while_ inserting the new node. Note that this is fine, but you need to be aware of the mistake when you call the `checkBalance` function, as there is a chance that you compare the updated-weight node with not-updated-weight children. It's also preferable if you separate the two.
- For Q4, many of you use the `.substring()` method. Note that this takes linear time! Though you may not know how it is implemented, but you can infer that it should takes linear, as it returns a `String` object
- Please use `StringBuilder` if you need $\mathcal{O}(1)$ append operation. And also _do not copy_ the `StringBuilder` object, as it defeats the purpose of `StringBuilder`. You can use `.setLength()`.
- Notice that `.deleteCharAt()` method takes $\mathcal{O}(k)$ time, where $k$ is the number of characters _after_ the character to be deleted. Essentially, if you delete the last character, it's constant time. You can check the implementation of [`.deleteCharAt()`](https://github.com/AdoptOpenJDK/openjdk-jdk11/blob/master/src/java.base/share/classes/java/lang/AbstractStringBuilder.java#L912-L917) and [`.setLength()`](https://github.com/AdoptOpenJDK/openjdk-jdk11/blob/master/src/java.base/share/classes/java/lang/AbstractStringBuilder.java#L270-L283).
- Lesson: know your library! Don't just use it :( You cannot assume everything is $\mathcal{O}(1)$. _At least_ make some inference of the cost.

## Suggestions

- If your code is deeply nested, please watch [this](https://www.youtube.com/watch?v=CFRhGnuXG-4). As much as possible, you do not want your main logic nested inside the `if` block. In practice, we handle all the edge cases first (which is usually much much shorter), and leave the main logic _outside_ the if braces.
- If you want the division to work as floating point number, you need to either cast it to type `float`, or you can make the number into floating point number. For instance, write `node.weight * 2.0 / 3.0` instead of `node.weight * 2 / 3`. Both might produce different result.
- For the point above, if you want to compare, say `node.left.weight <= node.weight * 2.0/3.0`, it's usually better for us to rearrange the inequality that consists of _only_ integer operations, i.e. `node.left.weight * 3 <= node.weight * 2`
- In Trie implementation, storing the pointer to children nodes and a flag indicating end-of-word is enough.
- I see many of the submissions use [magic number](https://stackoverflow.com/questions/47882/what-is-a-magic-number-and-why-is-it-bad). As much as possible, try avoid it. For instance, when you try to get the index of a character, try not to write the following:

    ```java
    if (48 <= character && character <= 57) {
      return character - 48;
    } else if (65 <= character && character <= 90) {
      return character - 55;
    } ...
    ```

    Instead:

    ```java
    final int ASCII_0 = 48;
    final int ASCII_9 = 57;
    final int ASCII_A = 65;
    final int ASCII_Z = 90;

    final boolean isNumber = ASCII_0 <= character && character <= ASCII_9;
    final boolean isCapital = ASCII_A <= character && character <= ASCII_Z;

    if (isNumber) {
      return character - ASCII_0;
    } else if (isCapital) {
      return character - ASCII_A + 10;
    } ...
    ```

    Try compare the two. You do not need to decipher what each numbers mean. At least the cognitive load to read the code is less on the second example.

## Pseudocode

Please use the following to compare your code and my _pseudocode_. See which part you could improve in terms of algorithm and writing style. Note that I do not claim my snippet code is better than yours, but I would like you to think about what's good and what's bad from your solution and my solution.

!!! warning

    My code has not been tested on Coursemology. If you found any mistake, let me know.

### Q1

```java
private int getWeight(TrieNode node) {
  return node == null ? 0 : node.weight;
}

public boolean checkBalance(TrieNode node) {
  // Best practice is to check all edge-cases and return straight away
  // We leave the happy-path (i.e. the main logic of the code) in the body
  if (node == null) {
    return true;
  }

  // This is the happy-path
  // Notice that I use the condition such that the node is called balanced, instead of calling the negation on unbalanced condition.
  boolean isLeftBalanced = getWeight(node.left) * 3 <= getWeight(node) * 2;
  boolean isRightBalanced = getWeight(node.right) * 3 <= getWeight(node) * 2;
  return isLeftBalanced && isRightBalanced;
}
```

### Q3

```java
  private class TrieNode {
    private boolean isEnd;
    private TrieNode[] children = new TrieNode[MAX_SIZE];

    // some details are omitted
    ...
  }

  void insert(String s) {
    TrieNode node = root;

    for (int i = 0; i < s.length(); i++) {
      char ch = s.charAt(i);

      // Handle the logic accordingly
      // You could create such method for your TrieNode and let your TrieNode
      // handle the logic, which is a good separation of responsibility.
      // Note that this is a good abstraction barrier between Trie and TrieNode.
      if (!node.isExistChild(ch)) {
        node.createChild(ch);
      }

      node = node.getChild(ch);
    }

    node.markEnd();
  }

  boolean contains(String s) {
    TrieNode node = root;

    for (int i = 0; i < s.length(); i++) {
      char ch = s.charAt(i)

      if (!node.isExistChild(ch)) {
        return false;
      }

      node = node.getChild(ch);
    }

    return node.isEndWord();
  }
```

### Q4

```java
  void prefixSearch(String prefix, ArrayList<String> results, int limit) {
    return prefixSearch(prefix, 0, results, limit, this.root, new StringBuilder());
  }

  private void prefixSearch(String prefix, int index, ArrayList<String> results,
                            TrieNode curNode, StringBuilder curString) {
    if (results.length() >= limit) {
      return;
    }

    // Happy path starts here
    if (index >= prefix.length()) {
      // We only add string if we've gone through the whole prefix
      if (curNode.isEndWord()) {
        results.add(curString.toString());
      }

      // Try concatenating a new one
      for (int i = 0; i < MAX_SIZE; i++) {
        TrieNode child = curNode.getChildForIndex(i);

        if (child == null) {
          continue;
        }

        curString.append(TrieNode.getCharacterFromIndex(i));
        prefixSearch(prefix, index + 1, results, child, curString);
        curString.setLength(index);
      }

      return;
    }

    // Case where you have to still traverse
    char curChar = prefix.charAt(index);

    if (curChar == WILDCARD) {
      // Try concatenating a new one
      for (int i = 0; i < MAX_SIZE; i++) {
        TrieNode child = curNode.getChildForIndex(i);

        if (child == null) {
          continue;
        }

        curString.append(TrieNode.getCharacterFromIndex(i));
        prefixSearch(prefix, index + 1, results, child, curString);
        curString.setLength(index);
      }
    } else {
      TrieNode child = curNode.getChildForCharacter(curChar);

      curString.append(curChar);
      prefixSearch(prefix, index + 1, results, child, curString);
      curString.setLength(index);
    }
  }
```
