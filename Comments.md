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
    
    private int myField;
    private String name;
    private ExampleStatus status;

    /**
     * Does many big business Things, depending on the factor. This method might
     * create several new Things, resulting in a new name.
     * 
     * @param factor Controls which new Things are created and added to this
     *               Example
     * @return The new status of this object
     */
    public ExampleStatus bigBusinessMethod(int factor) {
        
        Collection<Thing> things = loadTheThings();
        // Only even numbered factors are valid because of reasons
        // See BUG-7243
        for (int i = 0; i < factor; i += 2) {
            Thing newThing = createANewThing(factor);
            things.append(newThing);
            updateStatus(newThing);
        }
        this.name = calculateNewName();
        return this.status;
    }
}
```

While contrived, the example above shows a good use of comments. The first thing
to point out is that only a couple of key places are commented. The comments
that exist either provide good documentation for callers, or explain why the
code is structured as it is. Also, note how using descriptive variable and
method names, along with good object-oriented principles, turns the the code
itself into "documentation". Thus, it minimizes the need to have comments
explain what the code is doing and why.

###### Avoid end-of-line comments

End-of-line comments **should** be avoided.

_Rationale:_ Comments at the end of a line are easy to miss. They offer no
benefit over placing the comment _before_ the line of code it applies to.
