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

Before refactoring:
```
function calc(a: number, b: number): number {
    return a * b;
}

let x = calc(10, 5);
```
After refactoring:
```
function calculate_rectangle_area(
    width: number,
    height: number
): number {
    return width * height;
}

let rectangle_area = calculate_rectangle_area(10, 5);
```
Before refactoring:
```
class Player {
public:
    int h;
    int s;
};
```
After refactoring:
```
class Player {
public:
    int health;
    int score;
};
```
### Language Comparison
These issues can happen in any language. In the typescript example types provide additional information about variables and functions, but meaningful names are still necessary to explain their purpose. And in the C++ example types are explicitly declared, but vague field and function names can still make classes difficult to understand.

## 2. Long Function
### What Is It?
A long function is a code smell that occurs when a function attempts to do too many things. This can occur when new features are added over time and the programmer does not break the code into smaller functions. Long functions can be hard to follow, debug, and update because the reader often has to track many steps in order to understand its functionality.
### Prevention and Refactoring
To prevent long functions, we want to give each function a distinct purpose that is focused. When a function performs multiple tasks, those tasks can be separated into smaller functions with names that clearly show their purpose. A chunk of code may be moved into its own function using Fowler's Extract Function refactoring. Because the function names clarify what each part performs, this makes the original function simpler to read.
### Code Examples
Although this specific example is short, imagine if it also checked the player's score, updated the UI, played a sound, and handled achievements. The function would become longer and harder to understand because it would handle many different tasks.
```
void CollectCoin()
{
    coins += 1;
    Debug.Log("Coin collected!");
    Destroy(gameObject);
}
```
Atter refactoring: 
```
void CollectCoin()
{
    UpdateCoinCount();
    ShowCollectionMessage();
    Destroy(gameObject);
}
```
```
void UpdateCoinCount()
{
    coins += 1;
}
```
```
void ShowCollectionMessage()
{
    Debug.Log("Coin collected!");
}
```
Example 2: This function can be split into two more functions when we use the extract function solution
```
function attackEnemy() {
    enemy.health -= 10;
    console.log("Enemy took damage!");
    if (enemy.health <= 0) {
        console.log("Enemy defeated!");
    }
}
```
After refactoring: 
```
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
```

## 3. Comments

### What Is It?
Comments are text notes in simple English that explain what a code function does so that anyone reviewing the code may understand it. Comments themselves are not a smell, but as Martin Fowler notes, they are often used as a "deodorant" that covers up bad code smells.

### Why Is It Problematic?
Comments become problematic when they give bad code a more pleasant aroma, allowing reviewers to ignore the underlying structural issues entirely. At times, code is refactored while comments are rarely updated, leading to outdated and misleading notes sitting above modernized code. Relying on heavy inline comments is often a cop-out way to avoid fixing unclear variable names or overly complex logic.

### Prevention and Refactoring
These issues can be prevented by writing self-documenting code and reserving comments to describe *why* a decision was made (such as workarounds, shortcuts, or alternate solutions), rather than narrating *what* the function is doing one step at a time. 

We can eliminate unnecessary comments using Martin Fowler's refactoring patterns:
- **Extract Variable (page 119):** Break complex expressions into descriptive local variables or constants so the math or boolean logic explains itself.
- **Extract Function (page 106):** Move a commented block of code into its own helper function named after what the comment was trying to explain.
- **Rename Function / Rename Variable (page 124 / 137):** Update vague identifiers so they don't require a translation note.

### Code Examples

**Example 1 (Python):**
In this example, a multi-line comment is used to explain a complex boolean condition, making it easy for the comment to fall out of sync if the weight logic changes later.

Before refactoring:
'''python
def can_pick_up_item(player, item):
    # Player can pick up the item if the combined weight doesn't exceed max_carry_weight,
    # OR if the item is a quest item (quest items bypass weight limits)
    if (player.current_weight + item.weight <= player.max_carry_weight) or item.is_quest_item:
        return True
    return False
'''

After Refactoring:
'''python
def can_pick_up_item(player, item):
    fits_in_inventory = (player.current_weight + item.weight) <= player.max_carry_weight
    
    # Quest items bypass weight limits to prevent soft-locking story progression
    return fits_in_inventory or item.is_quest_item
'''

Example 2:

'''javascript
Before Refactoring:
function calculateDamage(baseDamage, attacker, target) {
    let total = baseDamage;

    // Apply 1.5x multiplier if attacker hits from behind (backstab)
    if (attacker.isBehind(target)) {
        total *= 1.5;
    }

    // Reduce damage by half if target has active shield buff
    if (target.buffs.includes("SHIELD")) {
        total *= 0.5;
    }

    return total;
}
'''

After Refactoring:
'''javascript
const BACKSTAB_MULTIPLIER = 1.5;
const SHIELD_MITIGATION = 0.5;

function calculateDamage(baseDamage, attacker, target) {
    let totalDamage = baseDamage;

    if (isBackstabAttack(attacker, target)) {
        totalDamage *= BACKSTAB_MULTIPLIER;
    }

    if (hasActiveShield(target)) {
        totalDamage *= SHIELD_MITIGATION;
    }

    return totalDamage;
}

function isBackstabAttack(attacker, target) {
    return attacker.isBehind(target);
}

function hasActiveShield(target) {
    return target.buffs.includes("SHIELD");
}
'''

### Language Comparison
Across different languages, Comment smells exist in similar ways, but each language has its own way of eliminating these smells. 

Python features Docstrings ("""...""") and optional Type Hints (def attack(target:Enemy) -> bool:) 
Docstrings are great for explaining module and public function behaviors. Using inline # comments is a key indicator that you should break up the expression into multiple named variables. 

JavaScript frequently uses JSDoc comments (/** @param {number} damage */) just to explain parameter types.
It's a great practice to transition to TypeScript so you don't need these type-explanatory comments.
