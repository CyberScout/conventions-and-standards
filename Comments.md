# Comments

###### Comments must be helpful

Comments **should** be used to clarify a section of code. They can explain the
business rule behind it, the rationale for a particular solution, or a
plain-language description of some very complicated logic.

Comments **must not** be meaningless or redundant.

_Rationale:_ Comments are extremely important for helping both code and
configuration to be understandable. However, they must be informative to have
any value.

_Example of bad comments:_

```java
public class Example {
    private int index;  // the index of Example
    
    /**
     * Retrieves the index.
     * 
     * @return the index
     */
    public int getIndex() {
        // Return the index
        return this.index;
    }
    
    /**
     * Sets the index.
     * 
     * @param index The new index
     */
    public void setIndex(int index) {
        // Set the index
        this.index = index;
    }
}
```

None of the comments above actually tell the reader anything more about the code
than what they can learn by simply scanning the file. The comments are just
white noise.

_Example of good comments:_

```java
public class Example {
    
    private int index = 0;
    
    /**
     * Increments the index, so that the next value can be retrieved. If the
     * index is out of range, an Exception will be thrown.
     * 
     * @return The new index 
     */
    public int increment() {
        // index must be incremented before it is returned. Otherwise, we would
        // be returning the old value to the caller.
        return ++this.index;
    }
}
```

While contrived, the example above shows a good use of comments. The first thing
to point out is that only a couple of key places are commented. The comments
that exist either provide good documentation for callers, or explain why the
code is structured as it is.

###### Avoid end-of-line comments
