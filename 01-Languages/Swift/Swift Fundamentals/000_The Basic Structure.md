The Basic Structure

Monday, November 8, 2021

8:12 AM

-   In swift I don\'t need semicolons at the end of my statements

    -   It won\'t cause an error though

-   Unlike many other languages, Swift does NOT need a **main** method or function. By default the compiler just begins at the top and moves its way down.

    -   ![no required import / include / using no required main print(\"He110, Pluralsight\" ) no required return A basic Swift program ](000_The_Basic_Structure_000.png)

-   Swift IS a type safe language. Even though **var** is commonly used to define variables... once defined, this variables cannot be changed.

-   ![var var var var playerName = \" Alice \" age = 21 temperature = 72 6 activeMember = true inferred inferred inferred inferred as a a a a Swift Swift Swift Swift String Int Double BOOI Type Inference Swift infers the type from the initial value ](000_The_Basic_Structure_001.png)

-   **Var** is required.... And it is the ONLY keyword we need/use to declare a variable.

**REPL read/eval/print/loop**

There are other ways to write swift code but not use playgrounds. This is where a REPL file comes into place.

The concept of a REPL started with LISP. This feature is what lets us write and immediately run a single expression/statement in the terminal. Also known as Interactive Mode... To start using REPL just go to the terminal and type **swift**. Playgrounds are just way easier to do things so I\'m not going to be using this much.

**The Swift Compilation Process**

![DEVELOPER COMPILED LANGUAGES (C++, C) SOURCE CODE \> FULL COMPILATION INTERMEDIATE (C#, JAVA) SOURCE CODE \> PARTIAL COMPILATION INTERPRETED LANGUAGES (JAVASCRIPT, RUBY) SOURCE CODE - NO COMPILATION BYTECODE USER RUN JIT COMPILE\' \> RUN • VM Runtime Engine required INTERPRET• \> RUN • Interpreter required ](000_The_Basic_Structure_002.png)

![DEVELOPER SWIFT IS A COMPILED LANGUAGE SOURCE CODE \> FULL COMPILATION INTERMEDIATE SOURCE CODE \> PARTIAL COMPILATION INTERPRETED LANGUAGES SOURCE CODE - NO COMPILATION BYTECODE USER RUN JIT COMPILE• \> RUN • VM / Runtime Engine required INTERPRET• \> RUN •Intergreter reauired ](000_The_Basic_Structure_003.png)
