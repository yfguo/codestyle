# Notes on Coding Conventions

Here are some coding useful coding conventions which aim to improves the
readability and maintainability of C/C++ codes. Most of these rules are common
practise while others are from my own experience in preventing unexpected
problems.

For now, this document does not cover all coding conventions, but serves
as a complement to the existing coding styles.

## Basics

### Indention and Margin

The default indention is 4 spaces. Each line has a soft limit of 80
columns. While a line should exceed that limits, it is okay if there is
only a few characters more and breaking the line make the code ugly.

### Line Breaks

The line continuation character should only be used in macro definitions.
It is always better to break a line at a non-comparative operator with
the operator starts a new line. The newline should be indented with its
scope. (A vim configuration can do this automatically, see below) For
example:

```c++
AVeryLongVariableOne = AVeryLongVariableTwo + AVeryLongVariableThree;

// Can be broken as
AVeryLongVariableOne
    = AVeryLongVariableTwo + AVeryLongVariableThree;

// or
AVeryLongVariableOne = AVeryLongVariableTwo
                       + AVeryLongVariableThree;

// But not
AVeryLongVariableOne = AVeryLongVariableTwo +
                       AVeryLongVariableThree;

// Similarly
if (Condition1 && Condition2) {}

// Should be broken as
if (Condition1
    && Condition2) {}

// not
if (Condition1
   && Condition2) {} // indention does not match the scope

// or
if (Condition1 &&
    Condition2) {} // operator on the previous line
```

### Spaces

Spaces should always be used to separate identifiers, keywords and
punctuations, expects for parentheses, like the following example. Note
that there is a space after keywords like `while`, `if`, `else`, and
before `{`.

```c++
while (off > 0) {
    if (file_off + off > splitter->get_end_offset(file_idx)) {
        off -= (int)(splitter->get_end_offset(file_idx) - file_off);
        file_idx += 1;
        file_off = splitter->get_start_offset(file_idx);
    }
    else {
        file_off += off;
        off = 0;
    }
}

// Not like the following
while(off>0){
    if(file_off+off>splitter->get_end_offset(file_idx)){
        off-= (int)(splitter->get_end_offset(file_idx)-file_off);
        file_idx+=1;
        file_off=splitter->get_start_offset(file_idx);
    }else{
        file_off+=off;
        off=0;
    }
}
```

### Naming

1. The name of variables, consts and functions should be clear and
self-explain (to some extent). For example, naming the variable for
local rank to `myrank` is better than naming it as `me` because `me`
could be anything (may even be a pointer to an object) while `myrank`
implied that it is a rank (thus an integer).

2. The naming scheme should be consistent throughout the project.

3. The all uppercase names should only be used for macros, const and
enumerate values. It should not be used on variables and functions.

4. Underscore (`_`) cannot be the first character of an identifier.
Identifiers start with underscore is reserved in C/C++ standards. While
GCC may not complain it, it does not make it right.

5. Member variables of a class/struct can have a name ends with an
underscore as it is a common practise (not required).

### Break before a Clause

Clauses (`else`, `catch`) should started on a new line and not following
a preceeding brace (`}`). For example:

```c++
if (condition) {
    ...
}
else {
    ...
}

// Not
if (condition) {
    ...
} else {
    ...
}
```

It is less error-prone when you need to comment out a clause.

## Learn More from an Existing Coding Style Now

Some widely used styles:

1. [LLVM Coding Style](http://llvm.org/docs/CodingStandards.html)
2. [Google C++ Style](https://google.github.io/styleguide/cppguide.html)
3. [Chromium C++
   Style](https://chromium.googlesource.com/chromium/src/+/master/styleguide/c++/c++.md)
4. [Mozilla C++
   Style](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Coding_Style)
5. [WebKit Code Style](https://webkit.org/code-style-guidelines/)

#### 