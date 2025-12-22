## I plan to use this for Revison or to convert it to NoteBook LLM 
## It contains stuff i find good or intersting or worth something

### 1.1.8 Functions as Black-Box Abstractions
This section is saying that the square-root program works because it is built out of many small, well-defined functions that each handle one task. These functions are treated as black boxes: when one function uses another, it does not care how that function is implemented internally, only what result it returns. This idea of hiding details and using functions only based on their inputs and outputs is called a black-box abstraction, and it is one of the most important ideas in programming.


### Bound Name and Free Name
A name is bound in a function if it is introduced there as a parameter or local variable (recieved or defined). The same name can be free in another function if that function uses it without defining it. Whether a name is bound or free is relative to the function being considered. With lexical scoping, a free name gets its value from the nearsest enclosing funtion  where it is bound.

Why this concept is used:
It is used to make programs predictable, safe, and scalable.

1. So functions behave the same every time
    A function doesnt accidentally depend on who calls it or what variables exist else where.

2. So helpers can be written cleanly
    Inner functions can use shared data without passing it everywhere.

3. So names dont clash in large programs
    You can reuse common names x,y,z etc without breaking other code.

4. So functions can be real black boxes
    You only need to know inputs and outputs , not internal variable names to use them.

5. So closures are possible
    Functions can "rememb" valuesfrom where they where created - essential for many designs.