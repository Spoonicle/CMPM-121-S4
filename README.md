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
A long function is a code smell that occurs when a function attempts to do too many things. This can occur when new features are added over time and the programmer does not break the code into smaller functions. Long functions can be hard to follow, debug, and update because the reader often has to track many steps in order to understand its functionality.
### Prevention and Refactoring
To prevent long functions, we want to give each function a distinct purpose that is focused. When a function performs multiple tasks, those tasks can be separated into smaller functions with names that clearly show their purpose. A chunk of code may be moved into its own function using Fowler's Extract Function refactoring. Because the function names clarify what each part performs, this makes the original function simpler to read.
### Code Examples
Although this specific example is short, imagine if it also checked the player's score, updated the UI, played a sound, and handled achievements. The function would become longer and harder to understand because it would handle many different tasks.

void CollectCoin()
{
    coins += 1;
    Debug.Log("Coin collected!");
    Destroy(gameObject);
}

Atter refactoring: 

void CollectCoin()
{
    UpdateCoinCount();
    ShowCollectionMessage();
    Destroy(gameObject);
}

void UpdateCoinCount()
{
    coins += 1;
}

void ShowCollectionMessage()
{
    Debug.Log("Coin collected!");
}

Example 2: This function can be split into two more functions when we use the extract function solution

function attackEnemy() {
    enemy.health -= 10;
    console.log("Enemy took damage!");
    if (enemy.health <= 0) {
        console.log("Enemy defeated!");
    }
}

After refactoring: 

function attackEnemy() {
    damageEnemy();
    checkIfDefeated();
}

function damageEnemy() {
    enemy.health -= 10;
    console.log("Enemy took damage!");
}

function checkIfDefeated() {
    if (enemy.health <= 0) {
        console.log("Enemy defeated!");
    }
}
### Language Comparison

## 3. Comments
### Comments are text notes in simple English that explain what a code function does, so that anyone reviewing the code may understand it.Comments themselves are not a smell, but are a "deodorant" that covers up bad code smells. 
### Comments can be problematic when they give a bad code smell a more pleasant aroma, allowing the reviewers ignore the bad smells entirely. At times you'll also see code refactored, with comments rarely being updated, leading to outdated and incorrect comments over modernized code. This is a cop-out way to avoid fixing bad code smells.
### These issues can be prevented by writing comments that describe the code's ideal pattern, not the specifics of what the exact function is doing one step at a time. Additionally, using comments to describe workarounds, shortcuts, or alternate solutions helps streamline a confused readers understanding. 
### Code Examples
### Language Comparison

## Conclusion

## References
