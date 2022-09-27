# Writing Good C Code

## Background

1. It's really important to write clean and readable code because
    1. Instructors and TAs have an easier time helping you and grading your work.
    1. After you graduate, you may work on a long-lived codebase with many contributors. To be a good teammate, your code should be neat and clean.
    1. Sloppy code is buggy code. If you or co-workers can't read it, they can't fix it.
    1. Sloppy code is slow code. You can only improve the performance of code you fully understand.
1. I'm writing this document for C programmers in CS 221 and CS 315, but it's important to write [idiomatic](https://medium.com/swlh/idiomatic-code-a73f17f0f287) code in any environment
1. Students sometimes object, saying, "My program works; isn't that enough?". No, it isn't.

## Comments

1. Ideally, we would write such clear and obvious code that comments aren't necessary. In reality, you need to document what you're thinking, so the next person who looks at the code can easily see what it's supposed to do.
1. If you do something clever or tricky, always add a comment.
1. In C, we can format comments like this
    ```c
    int i = 0;  /* assign 0 to i */
    ```
    or like this
    ```c
    int i = 0;  // assign 0 to i
    ```
    The latter style came from C++ but is acceptable in C
1. Multiline comments in C should be formatted like this:
    ```c
    /*
     * This is a comment
     * Be careful with the following code because...
     */
1. Make your comments helpful. `assign 0 to i` is not as helpful as `initialize loop index variable`
1. If you're writing comments for each line of code, align their left edges like this:
    ```c
    #define X 0         // X is important because...
    #define Y "foobar"  // "foobar" is used to...
    #define Pi 3.14159  // Geometry is fun!
    ```

## Code Blocks

1. In C, it's idiomatic to put `{` at the end of a line, and the `}` in the same column which started the block, like this:
    ```c
    if (something) {
        x = 0;
    } else {
        x = 1;
    }
    ```
    Putting both braces in the column which started the block is idiomatic in Java, but acceptable in C:
    ```c
    if (something) 
    {
        x = 0;
    } else {
        x = 1;
    }
    ```
    This is not acceptable:
    ```c
    if (something) { x = 0; } else { x = 1; }
    ```
    nor is this:
    ```c
    if (something)
        {
        x = 0;
        }
        else {
            x = 1;
        }
    ```

## Spacing

1. You should have braces around operators, after commas, and before open braces. Acceptable:
    ```c
    for (int i = 0; i < argc; i++) {
        x += 4;
    ```
    Not acceptable:
    ```c
    for(int i=0;i<argc;i++){
        x+=4;
    ```

## Identifier Naming

1. You should use variable and function names which clearly indicate their purpose. Acceptable
    ```c
    int best_move = find_best_move(&board);
    ```
    Not acceptable:
    ```c
    int b = find(&bd);
    ```
1. Although snake_case names are idiomatic in C, camelCase names are idiomatic in Java and Go (and acceptable in C)
    ```c
    int bestMove = findBestMove(&board);
    ```

## Function Size

1. Think of each function as being a paragraph, with a beginning, middle, and end.
1. If your function appears to have multiple beginnings, then you should break it up into multiple functions.
1. Each function should do only what it says, and use only the parameters it gets passed.
1. Same idea with files. If you have a file called `chess_move.c` and it starts drawing the board, you need a new file. 
1. This is called [Separation of Concerns](https://en.wikipedia.org/wiki/Separation_of_concerns)