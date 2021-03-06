# Parantheses Matching

```
() - nested correctly
)( - nested incorrectly
(  - nested incorrectly
```

### If expression contains only one type of paranthesis

* scan expression from left to right:
    * when left parenthesis encountered increment `depth`
    * when right parenthesis encountered decrement `depth`
        * if `depth<0`, it is not balanced.
* at end of expression if `depth!=0`, it is not balanced.

```java
boolean isNestedCorrectly(String expr) {
    int depth = 0;
    for(char ch: expr) {
        if(isLeftParenthesis(ch))
            depth++;
        else {
            depth--;
            if(depth<0)
                return false;
        }
    }
    return depth==0;
}
```

### If expression contains more than one type of parenthesis

* scan expression from left to right:
    * when left parenthesis encountered, push into stack.
    * when right parenthesis encountered, pop from stack and check that the parenthesis match.
* at end of expression stack should be empty.

```java
boolean isNestedCorrectly(String expr) {
    Stack stack = new Stack();

    for(char ch: expr) {
        if(isLeftParenthesis(ch))
            stack.push(ch);
        else {
            if(stack.isEmpty())
                return false;
            else if(getRightParenthesis(stack.pop())!=ch)
                return false;
        }
    }
    return stack.isEmpty();
}
```
