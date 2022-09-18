# Debugging with gdb

[gdb](https://www.sourceware.org/gdb/) is an interactive debugger that you can use to watch what your programs do at runtime. Although many guides are available on the Internet, this guide shows some basics to get you started at USF.

## Setup

1. `gdb` is most helpful when you can see the source code as you're debugging. To enable that, edit `~/.gdbinit` and add the text
    ```
    layout src
    ```
    save and exit the editor

## Compiling your program

1. Use the `-g` flag with `gcc` or `as` to include debug symbols with your program
    ```
    gcc -g -o foo foo.c
    ```

    ```
    as -g -o foo.o foo.s
    ```
1. If `gdb` says "No source available", you probably didn't compile with `-g`

## Starting the debugger

1. To debug an executable program called `foobar`
    ```
    $ gdb foobar
    ```
    not
    ```
    $ gdb foobar.c
    ```

1. Once the debugger launches, set a breakpoint using a function name or line number
    ```
    (gdb) break main
    ```

1. Now you can run the program with command-line arguments. To run `foobar` with the arguments `1 2 3`
    ```
    (gdb) run 1 2 3
    ```

## Debugging your program

1. Once you're stopped at a breakpoint, you can 

    run one statement at a time
    ```
    (gdb) next
    ```
    step into function calls
    ```
    (gdb) step
    ```
    inspect the value of a variable called `x`
    ```
    (gdb) print x
    ```
    format the printing of `x` in hexadeximal, or as a character
    ```
    (gdb) print/x x
    (gdb) print/c x
    ```
    examine memory at a pointer called `pdata`
    ```
    (gdb) x/8 pdata
    ```
1. You can continue until the next breakpoint or the end of the program
    ```
    (gdb) continue
    ```
1. You can execute until the end of a function
    ```
    (gdb) finish
    ```

## Segmentation Faults

1. If you encounter a seg fault, you can look at the call chain (back trace) using
    ```
    (gdb) bt
    ```
    and look at the variables in each frame using
    ```
    (gdb) frame 0
    (gdb) print pdata
    ```

## Shortcuts

1. `gdb` commands can be abbreviated with shortcuts, e.g. `b` for break or `p` for `print`
    ```
    (gdb) b main
    (gdb) p x
    ```
1. To step/next quickly through your program, you can use the Return/Enter key, which repeats the previous command command.

## gdb and printf()

1. If your program uses `printf()` and the output messes up the `gdb` view, you can get rid of the `printf()` output
    ```
    (gdb) refresh
    ``` 

## Assembly language

1. A helpful setup in `~/.gdbinit` might be
    ```
    tui new-layout asm {-horizontal src 1 regs 1} 2 status 0 cmd 1
    layout asm
    ```
1. You can inspect register values
    ```
    (gdb) print $a0
    ```
1. You can examine memory pointed to by a register (8 words in hex)
    ```
    (gdb) x/8x $a0
    ```
    or as a string (8 characters)
    ```
    (gdb) x/8c $a0
    ```
