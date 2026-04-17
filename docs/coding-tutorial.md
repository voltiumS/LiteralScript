# LiteralScript v3.0 Complete Coding Tutorial

**Version**: 3.0.0 - With Module System!  
**Last Updated**: April 17, 2026  
**Duration**: ~3 hours for complete guide

---

## Table of Contents

1. [Getting Started](#getting-started)
2. [Using Modules (NEW!)](#using-modules-new)
3. [Language Basics](#language-basics)
4. [Data Types](#data-types)
5. [Control Flow](#control-flow)
6. [Functions & Custom Modules](#functions--custom-modules)
7. [Advanced Features](#advanced-features)
8. [Ecosystem Features](#ecosystem-features)
9. [Real-World Examples](#real-world-examples)
10. [Best Practices](#best-practices)
11. [Troubleshooting](#troubleshooting)

---

## Getting Started

### Quick Launch with `do` Command

Create a file called `hello.literal`:

```english
Display "Hello, LiteralScript!"
```

Run it with the new `do` command:
```bash
literal do hello.literal
```

**Output**:
```
Hello, LiteralScript!
```

✅ **Success!** You've written your first program!

### Alternative: Use `build` Command

```bash
# Compile to Rust
literal build hello.literal

# Or interpret it
literal build hello.literal --interpret
```

---

## Using Modules (NEW!)

### What are Modules?

Modules let you:
- ✅ Import external libraries from Python, Node.js, Rust, etc.
- ✅ Create reusable code packages
- ✅ Organize code logically
- ✅ Avoid code duplication

### Import External Packages

**Example 1: Import Python Packages**

```english
import pandas as pd
import numpy

Record [1, 2, 3] into data
Display pd.describe using data
```

**Example 2: Import Node.js Packages**

```english
import express as app
import axios

app.listen at 3000
Display "Server running"
```

**Example 3: Import Multiple Packages**

```english
import requests
import json
import datetime as dt

record requests.get using "https://api.example.com" into response
display response
```

### Creating Your Own Modules

**Create a file `utilities.literal`**:

```english
module utilities

  record function greet using name
    Display "Hello, " + name
  done

  record function add using a, b
    Record a + b into result
    Display result
  done

done module
```

**Use it in another file**:

```english
import utilities

call utilities.greet using "World"
call utilities.add using 5, 3
```

### Module Organization

Organize large projects with directory structure:

```
myproject/
├── modules/
│   ├── utils/
│   │   ├── index.literal      # Main module file
│   │   ├── math.literal       # Submodule
│   │   └── string.literal     # Submodule
│   ├── database/
│   │   └── index.literal
│   └── api/
│       └── index.literal
├── main.literal               # Entry point
└── config.literal             # Configuration
```

Usage:
```english
import utils
import database
import api
```

For detailed information, see [MODULE_SYSTEM.md](MODULE_SYSTEM.md)

---

## Language Basics

### Syntax Overview

LiteralScript uses **natural English** instead of programming symbols:

| Traditional | LiteralScript |
|-------------|--------------|
| `print(x)` | `Display x` |
| `x = 5` | `Record 5 into x` |
| `for i in list:` | `For item in list:` |
| `if x > 5:` | `When x greater than 5:` |
| `def func():` | `Define func:` |
| `import lib` | `import lib` |

### Commands Overview

| Command | Purpose | Example |
|---------|---------|---------|
| `Display` | Output text/values | `Display "Hello"` |
| `Record` | Create/assign variable | `Record 42 into x` |
| `For` | Loop through items | `For item in list:` |
| `When` | Conditional (if) | `When x greater than 5:` |
| `Define` | Create function | `Define greet:` |
| `Call` | Execute function | `Call greet` |
| `import` | Load a module | `import numpy` |
| `module` | Define a module | `module mylib` |

---

## Data Types

### Numbers

Store and use numeric values:

```english
Record 42 into age
Record 3.14 into pi
Record -10 into negative

Display age + 10           # Output: 52
Display pi * 2             # Output: 6.28
Display negative + 20      # Output: 10
```

**Supported Operations**: `+`, `-`, `*`, `/`

### Text (Strings)

Store words and sentences:

```english
Record "Alice" into name
Record "Hello, World!" into greeting

Display name                       # Output: Alice
Display greeting                   # Output: Hello, World!
Display name + " is awesome!"     # Output: Alice is awesome!
```

**String Operations**:
- Concatenation (combining): `"Hello" + " " + "World"`
- Display: `Display text`

### Lists (Arrays)

Store multiple values:

```english
Record [1, 2, 3, 4, 5] into numbers
Record ["apple", "banana", "cherry"] into fruits
Record [10, "text", 3.14] into mixed

Display numbers             # Output: [1, 2, 3, 4, 5]
Display fruits              # Output: ["apple", "banana", "cherry"]
```

### Booleans

True/False values:

```english
Record true into is_valid
Record false into is_empty

When is_valid:
  Display "Valid!"

When is_empty otherwise:
  Display "Not empty"
```

---

## Control Flow

### Displaying Values

Output to console:

```english
Display "Hello"
Display 42
Display true
Display [1, 2, 3]

Record 10 into x
Display x
Display x + 5
```

### If/Else (When)

Conditional execution:

```english
Record 15 into age

When age greater than 18:
  Display "Adult"
Otherwise:
  Display "Minor"
```

**Comparison Operators**:
- `greater than` (>)
- `less than` (<)
- `equal to` (==)
- `not equal to` (!=)
- `greater than or equal to` (>=)
- `less than or equal to` (<=)

### Multiple Conditions

```english
Record 20 into score

When score greater than 90:
  Display "A"
When score greater than 80:
  Display "B"
When score greater than 70:
  Display "C"
Otherwise:
  Display "F"
```

### Loops (For)

Repeat code multiple times:

```english
Record [1, 2, 3, 4, 5] into numbers

For item in numbers:
  Display item

# Output:
# 1
# 2
# 3
# 4
# 5
```

**Loop with Operations**:

```english
Record [1, 2, 3, 4, 5] into numbers

For item in numbers:
  Record item * 2 into doubled
  Display doubled

# Output:
# 2
# 4
# 6
# 8
# 10
```

---

## Functions

### Simple Functions

Define reusable code:

```english
Define greet:
  Display "Hello, World!"

Call greet
Call greet
Call greet

# Output:
# Hello, World!
# Hello, World!
# Hello, World!
```

### Functions with Parameters

Pass data to functions:

```english
Define greet taking name:
  Display "Hello, " + name + "!"

Call greet "Alice"
Call greet "Bob"
Call greet "Charlie"

# Output:
# Hello, Alice!
# Hello, Bob!
# Hello, Charlie!
```

### Multiple Parameters

```english
Define add taking x, y:
  Record x + y into result
  Display result

Call add 5, 3      # Output: 8
Call add 10, 20    # Output: 30
```

### Functions with Loops

```english
Define print_numbers taking count:
  For i in [1, 2, 3, 4, 5]:
    When i less than or equal to count:
      Display i

Call print_numbers 3

# Output:
# 1
# 2
# 3
```

---

## Advanced Features

### Complex Data Operations

```english
Record [1, 2, 3, 4, 5] into numbers
Record 0 into sum

For num in numbers:
  Record sum + num into sum

Display "Total: " + sum    # Output: Total: 15
```

### Nested Loops

```english
Record [1, 2, 3] into rows
Record [10, 20, 30] into cols

For row in rows:
  For col in cols:
    Display row + col
```

**Output**:
```
11
21
31
12
22
32
13
23
33
```

### Conditional Logic with Loops

```english
Record [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] into numbers
Record 0 into even_count

For num in numbers:
  Record num / 2 into quotient
  Record num - (quotient * 2) into remainder
  When remainder equal to 0:
    Record even_count + 1 into even_count

Display "Even numbers: " + even_count    # Output: Even numbers: 5
```

---

## Ecosystem Features

### Terminal Commands

Execute shell commands:

```english
Call shell:
  ls        # List files (macOS/Linux)
  dir       # List files (Windows)
  cd folder # Change directory
```

### Database Operations

Work with databases:

```english
Call database:init postgresql mydb
Call database:create_table users
Call database:add_column id integer
Call database:add_column name text
```

### File System

Create and read files:

```english
Call filesystem:create_file data.txt
Call filesystem:write "Hello" into data.txt
Record filesystem:read data.txt into content
Display content
```

### Package Management

Install packages:

```english
Call packages:install numpy
Call packages:install pandas
Call packages:install requests
```

### API Generation

Create APIs:

```english
Call api:init rest
Call api:add_route /hello GET
Call api:add_route /users POST
```

---

## Real-World Examples

### Example 1: Grade Calculator

```english
Define calculate_grade taking score:
  When score greater than or equal to 90:
    Display "Grade: A"
  When score greater than or equal to 80:
    Display "Grade: B"
  When score greater than or equal to 70:
    Display "Grade: C"
  When score greater than or equal to 60:
    Display "Grade: D"
  Otherwise:
    Display "Grade: F"

Call calculate_grade 95     # Output: Grade: A
Call calculate_grade 87     # Output: Grade: B
Call calculate_grade 72     # Output: Grade: C
```

### Example 2: Sum Calculator

```english
Define sum_list taking numbers:
  Record 0 into total
  
  For num in numbers:
    Record total + num into total
  
  Display "Sum: " + total

Call sum_list [10, 20, 30, 40]    # Output: Sum: 100
```

### Example 3: Factorial Function

```english
Define factorial taking n:
  When n equal to 1:
    Display n
  Otherwise:
    Record n - 1 into decremented
    Call factorial decremented

Call factorial 5

# Output:
# 5
# 4
# 3
# 2
# 1
```

### Example 4: Password Validator

```english
Define validate_password taking password:
  Record false into is_valid
  Record 0 into length
  
  For char in password:
    Record length + 1 into length
  
  When length greater than or equal to 8:
    Record true into is_valid
  
  When is_valid:
    Display "Password accepted"
  Otherwise:
    Display "Password too short (min 8 characters)"

Call validate_password "short"       # Output: Password too short...
Call validate_password "verylongpassword"  # Output: Password accepted
```

### Example 5: Text Generation from Data

```english
Define generate_report taking names, scores:
  Display "=== Student Report ==="
  
  For name in names:
    For score in scores:
      Display name + ": " + score

Record ["Alice", "Bob"] into students
Record [95, 87] into their_scores

Call generate_report students, their_scores
```

---

## Best Practices

### 1. Clear Variable Names

❌ **Bad**:
```english
Record 100 into x
Record 50 into y
Display x + y
```

✅ **Good**:
```english
Record 100 into initial_balance
Record 50 into withdrawal
Display initial_balance - withdrawal
```

### 2. Descriptive Function Names

❌ **Bad**:
```english
Define calc taking x:
  Display x + 10
```

✅ **Good**:
```english
Define add_tax taking price:
  Record price + (price * 0.1) into final_price
  Display final_price
```

### 3. Comment Your Code

```english
# This function calculates the total cost
Define total_with_tax taking base_price:
  # Calculate 10% tax
  Record base_price * 0.1 into tax_amount
  
  # Calculate total
  Record base_price + tax_amount into total
  
  # Display result
  Display total

Call total_with_tax 100
```

### 4. Input Validation

```english
Define check_age taking age:
  When age less than 0:
    Display "Invalid age"
  When age greater than 150:
    Display "Invalid age"
  Otherwise:
    Display "Valid age: " + age

Call check_age 25     # Output: Valid age: 25
Call check_age -5     # Output: Invalid age
```

### 5. Modular Design

Break complex tasks into smaller functions:

```english
Define calculate_final_price taking base:
  Record calculate_tax base into tax
  Record calculate_shipping base into shipping
  Record base + tax + shipping into total
  Display total

Define calculate_tax taking price:
  Record price * 0.1 into tax
  Display tax

Define calculate_shipping taking price:
  Record price * 0.05 into shipping
  Display shipping

Call calculate_final_price 100
```

---

## Troubleshooting

### "Command not found"

**Error**:
```
literal: command not found
```

**Solution**:
```bash
# Make sure LiteralScript is in PATH
echo $PATH | grep literal

# Or use full path
/usr/local/bin/literal program.literal --run
```

### "Syntax Error"

**Common Mistake**:
```english
# WRONG - semicolon not needed
Record 5 into x;

# CORRECT
Record 5 into x
```

**Solution**: LiteralScript doesn't use semicolons

### "Variable not defined"

**Error**:
```
Undefined variable: x
```

**Wrong Code**:
```english
Display x    # x not defined yet!
Record 5 into x
```

**Correct Code**:
```english
Record 5 into x
Display x
```

### Code Not Running

**Check**:
1. Syntax: `literal program.literal --ast` (shows AST)
2. Errors: `literal program.literal` (shows errors)
3. Trace: `literal program.literal --ir` (shows IR)

---

## Code Generation

LiteralScript generates production code in 6 languages!

### Example Program

Create `example.literal`:
```english
Record 10 into x
Record 20 into y
Display x + y
```

### Generate Code

```bash
literal example.literal
```

**Generated Files**:
- `example.literal.rs` - Rust (production-quality)
- `example.literal.py` - Python
- `example.literal.js` - JavaScript
- `example.literal.cpp` - C++
- `example.literal.sql` - SQL
- `example.literal.html` - HTML/CSS/JS

### View Generated Rust

```bash
cat example.literal.rs
```

**Output**:
```rust
fn main() {
    let x = 10;
    let y = 20;
    println!("{}", x + y);
}
```

---

## Next Steps

### 1. Learn the Basics (30 min)
Follow examples 1-5 above

### 2. Read API Reference
See [API_COMPLETE_REFERENCE.md](../docs/API_COMPLETE_REFERENCE.md)

### 3. Explore Examples
```bash
literal examples/hello.literal --run
literal examples/basic_demo.literal --run
literal examples/sum_numbers.literal --run
literal examples/list_processing.literal --run
```

### 4. Try the REPL
```bash
literal-repl
literal> Display "Hello"
literal> Record 42 into x
literal> Display x * 2
literal> quit
```

### 5. Create Your Program
Write and test your own programs!

---

## Quick Reference

### Commands
```
Display value              # Output
Record value into var      # Assign variable
For item in list:          # Loop
When condition:            # If statement
Otherwise:                 # Else
Define func:               # Define function
Call func                  # Call function
```

### Operators
```
+  Addition
-  Subtraction
*  Multiplication
/  Division
>  Greater than
<  Less than
== Equal to
!= Not equal to
>= Greater than or equal
<= Less than or equal
```

### Data Types
```
Number:    42, 3.14, -10
Text:      "Hello", "World"
List:      [1, 2, 3], ["a", "b"]
Boolean:   true, false
```

---

## Common Patterns

### Pattern 1: Count Items
```english
Record 0 into count
For item in list:
  Record count + 1 into count
Display count
```

### Pattern 2: Find Max
```english
Record 0 into max_value
For num in numbers:
  When num greater than max_value:
    Record num into max_value
Display max_value
```

### Pattern 3: Filter List
```english
Record [] into filtered
For item in list:
  When item greater than 5:
    # Add to filtered (advanced: use concatenation)
Display filtered
```

### Pattern 4: Nested Function Calls
```english
Define process taking data:
  Call validate data
  Call transform data
  Call output data

Call process [1, 2, 3]
```

---

## Resources

- **Official Documentation**: [README.md](../docs/README.md)
- **API Reference**: [API_COMPLETE_REFERENCE.md](../docs/API_COMPLETE_REFERENCE.md)
- **Installation**: [INSTALLATION_GUIDE.md](../docs/INSTALLATION_GUIDE.md)
- **Contributing**: [CONTRIBUTING.md](../docs/CONTRIBUTING.md)
- **Examples**: See `examples/` folder

---

## Summary

You can now:

✅ Write basic programs  
✅ Use variables and data types  
✅ Control flow with conditionals and loops  
✅ Create and call functions  
✅ Generate production code in 6 languages  
✅ Use ecosystem features (database, API, etc.)  

**Next**: Pick a project and start coding! 🚀

---

**LiteralScript v2.0.0** — Transform English into Code  
MIT License | https://github.com/voltiumS/LiteralScript

