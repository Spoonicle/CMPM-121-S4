# CMPM-121-S4: Code Smells and Refactoring

## Group Members
- Mason Reoch
- Tim Phan
- Elder Ivan Argueta

## Introduction to Code Smells

## 1. Mysterious Name
### What Is It?
Mysterious Name is a code smell that occurs when variables, functions, or classes have names that do not clearly describe their purpose. This usuallyhappens when programmers use short names. abberviations, names that are too general, or names that make sense to them at the moment, but later can be confusing to themselves and eveyone else.


### Why Is It Problematic?
It affects readability and understanding for other programmers. developers need to spend more time figuring out the purpose of variables or functions before making changes. When working with froup  unclear names makes it harder for toher memebrs to understand and contribute. Mislableing can lead to misunderstandings of what a variable represents or what the function does. Can lead to erros. 
### Prevention and Refactoring
We can prevent these issues by using meaningful names. Martin fowler states we should, Change Function Declaration (page 124): Rename a function to better describe what it does. Rename Variable (page 137): Replace vague variable names with ones that clearly describe the information they store, and Rename Fields (page 244): Rename class or object fields to better communicate their purpose.
### Code Examples

Before refactoring
function calc(a: number, b: number): number {
    return a * b;
}

let x = calc(10, 5);

After refactoring
function calculate_rectangle_area(
    width: number,
    height: number
): number {
    return width * height;
}

let rectangle_area = calculate_rectangle_area(10, 5);

Before refactoring
class Player {
public:
    int h;
    int s;
};

After refactoring
class Player {
public:
    int health;
    int score;
};
### Language Comparison
These issues can happen in any language. In the typescript example types provide additional information about variables and functions, but meaningful names are still necessary to explain their purpose. And in the C++ example types are explicitly declared, but vague field and function names can still make classes difficult to understand.

## 2. Long Function
### What Is It?
### Why Is It Problematic?
### Prevention and Refactoring
### Code Examples
### Language Comparison

## 3. Comments
### What Is It?
### Why Is It Problematic?
### Prevention and Refactoring
### Code Examples
### Language Comparison

## Conclusion

## References