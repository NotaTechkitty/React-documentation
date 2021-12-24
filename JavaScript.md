## JavaScript engines

**Basics concept** :

- Compiler : Run code after compile all line of code in the program.

- Interpreter : Run code line by line. Fast but slow when reading repeating code multiple times.

**JavaScript** engines

![javaScript Engines](Image/javaScript_engine.PNG)

- parser : check syntax and semantics. Break code into tokens. These tokens call Abstract Syntax tree.
- Abstract Syntax tree : Help the interpreter understand the program.
- Interpreter : convert Abstract Syntax tree into  Byte code. ( ignition ).
- Profiler ( Moniter ) : Fix the Interpreter weakness. Observing the JS code, which code is reapeated some times marked as warm, many times marked as hot and then send it to compiler
- Compiler : Return optimized byte. V8 engines using the Turbo Fan compiler.

**Mozilla’s SpiderMonkey JavaScript Engine**

![mozilla javaScript Engines](Image/Mozilla_JS_engine.PNG)
- JS source code to compiler
- Interpreter
- JIT compiler

V8 engine have more performance than Mozilla's spidermonkey engine.
## Important Note

### const
- Block scope and can't be re-declare in the same block.
- Can't be reasign **NOT** an immutable value. What not be changed is the reference to the value.

example : An array/object can change its value but can't change the reference to a new a new array or object or any other data types.
- create read only reference to a value.

