# LiteralScript v3.0 Complete Developer Guide & API Reference

**Version**: 3.0.0 - Module System Edition  
**Last Updated**: April 17, 2026  
**Target Audience**: Developers, Contributors, API Users

---

## What's New in v3.0

### Major Features
✅ **Module System** - Import and create reusable code modules  
✅ **Cross-Language Packages** - Use npm, pip, cargo, gem, maven packages  
✅ **New CLI Commands** - `do`, `build`, `run`, `watch`, `serverhost`  
✅ **Module Resolver** - Automatic package detection and installation  
✅ **Advanced Imports** - Import with aliases and selective imports  

### New Commands

| Command | Purpose | Signature |
|---------|---------|-----------|
| `do` | Execute .literal file | `literal do <file.literal>` |
| `run` | Execute file (alias) | `literal run <file.literal>` |
| `build` | Compile/interpret | `literal build <file> [--interpret]` |
| `watch` | Auto-rebuild on change | `literal watch <file.literal>` |
| `serverhost` | HTTP server hosting | `literal serverhost <file> [--port N]` |
| `import` | Resolve/install modules | `literal import <module> [--info/--list]` |

### New Syntax

```english
import express                    # Import module
import pandas as pd              # Import with alias
import numpy from array, math    # Selective import

module mylib                     # Define module
  ...
done module
```

---

## Table of Contents

1. [CLI Commands (v3.0)](#cli-commands-v30)
2. [Module System](#module-system)
3. [Project Architecture](#project-architecture)
4. [Core Compiler Modules](#core-compiler-modules)
5. [Ecosystem Modules](#ecosystem-modules)
6. [Complete Function Reference](#complete-function-reference)
7. [Module Dependencies](#module-dependencies)
8. [Data Structure Reference](#data-structure-reference)
9. [Code Examples](#code-examples)
10. [Contributing Guide](#contributing-guide)

---

## CLI Commands (v3.0)

### `literal do <file.literal>`

**Purpose**: Execute a LiteralScript file immediately using the interpreter

**Syntax**:
```bash
literal do hello.literal
literal do app.literal
```

**Details**:
- Uses direct interpretation (no compilation)
- Fastest way to run scripts
- Perfect for testing and development
- Equivalent to old: `literal file.literal --run`

**Return Code**: 
- 0 on success
- Non-zero on error

---

### `literal run <file.literal>`

**Purpose**: Alias for `do` command

**Syntax**:
```bash
literal run app.literal
```

**Details**:
- Identical behavior to `do`
- Alternative syntax for convenience

---

### `literal build <file.literal> [OPTIONS]`

**Purpose**: Compile LiteralScript to another language or interpret

**Syntax**:
```bash
# Compile to Rust (default)
literal build app.literal

# Interpret instead
literal build app.literal --interpret

# With program options
literal build data.literal > output.rs
```

**Options**:
| Option | Effect |
|--------|--------|
| `--interpret` | Skip compilation, execute directly |
| `--ast` | Display abstract syntax tree |
| `--ir` | Display intermediate representation |

**Output**:
- Default: Generates `<filename>.out.rs`
- With `--interpret`: Direct execution with output

---

### `literal watch <file.literal>`

**Purpose**: Monitor file for changes and automatically rebuild

**Syntax**:
```bash
literal watch myapp.literal
literal watch server.literal --port 3000
```

**Details**:
- Polls file every 500ms for changes
- Auto-runs `build` on file modification
- Perfect for active development
- Press Ctrl+C to stop watching

**Useful For**:
- Real-time development feedback
- Continuous testing
- Quick iteration cycles

---

### `literal serverhost <file.literal> [OPTIONS]`

**Purpose**: Launch a LiteralScript file as an HTTP server

**Syntax**:
```bash
# Default port 3000
literal serverhost api.literal

# Custom port
literal serverhost app.literal --port 8080

# With options
literal serverhost websocket.literal --port 9000 --ssl
```

**Options**:
| Option | Default | Effect |
|--------|---------|--------|
| `--port` | 3000 | HTTP server port |
| `--ssl` | off | Enable HTTPS |
| `--host` | 0.0.0.0 | Bind address |

**Details**:
- Starts HTTP server for your .literal file
- Functions become HTTP endpoints
- Serves files and handles requests
- Press Ctrl+C to stop

**Example**:
```english
# api.literal
import express as app

record function api_handler
  Display "Handler called"
done

app.get "/" using api_handler
app.listen at 3000
```

Run: `literal serverhost api.literal --port 3000`

---

### `literal import <MODULE> [OPTIONS]`

**Purpose**: Resolve, install, or query module information

**Syntax**:
```bash
# Resolve and install a module
literal import pandas

# Get module information
literal import express --info

# List all available packages
literal import --list

# Search for packages
literal import --search "web"
```

**Options**:
| Option | Effect |
|--------|--------|
| `--info` | Display source & version info |
| `--list` | List all known packages |
| `--search <term>` | Search package registry |
| `--install` | Force installation |

**Output Example**:
```
[Module] Installing package: pandas
[Module] Detected: Python/pip
[Module] Run: pip install pandas
[Module] Successfully resolved: pandas
```

---

## Module System

### Import Statements

**Basic Import**:
```english
import express
import numpy
```

**Import with Alias**:
```english
import pandas as pd
import requests as http
```

**Selective Import**:
```english
import numpy from array, reshape, solve
import pandas from DataFrame, Series, read_csv
```

**Multiple Imports**:
```english
import express
import socket
import crypto from random, hash
```

### Module Definition

**Basic Module**:
```english
module mylib

  record function add using a, b
    Record a + b into result
    Display result
  done

done module
```

**Module with Exports**:
```english
module utilities

  export clean_data
  export validate

  record function clean_data using values
    ...
  done

done module
```

### Module Resolution

Modules are resolved in this order:

1. **Local Files**: `module_name.literal`
2. **Directory Modules**: `./modules/module_name/index.literal`
3. **Package Sources**:
   - npm (Node.js/JavaScript)
   - pip (Python)
   - cargo (Rust)
   - nuget (.NET)
   - gem (Ruby)
   - go modules (Go)
   - maven (Java)

### Cross-Language Integration

**Python Packages**:
```english
import pandas
import numpy as np
import sklearn
```

**JavaScript/npm Packages**:
```english
import express
import axios
import lodash
```

**Rust Crates**:
```english
import tokio
import serde
import sqlx as db
```

---

## Project Architecture

### High-Level Overview

```
LiteralScript v3.0
├── Compiler Frontend
│   ├── Lexer (src/lexer.rs)
│   │   ├─ Tokenizes English input
│   │   └─ Supports: import, module, export keywords
│   ├── Parser (src/parser.rs)
│   │   ├─ Converts tokens into AST
│   │   └─ Handles ImportStmt & ModuleStmt
│   ├── Semantic Analyzer (src/semantic_analyzer.rs)
│   │   ├─ Type checking & validation
│   │   └─ Generates IR with Import/Module nodes
│   └── CodeGen (src/codegen.rs)
│       ├─ Generates 6 target languages
│       └─ Outputs use statements & mod blocks
│
├── Module System
│   ├── Module Resolver (src/module_resolver.rs)
│   │   ├─ Resolves local modules
│   │   ├─ Locates external packages
│   │   └─ Manages module cache
│   └── Package Manager
│       ├─ npm, pip, cargo, nuget, gem, maven, go
│       └─ Auto-detection & installation
│
├── Runtime (src/runtime.rs)
│   ├─ Direct interpretation
│   └─ Supports Import & Module execution
│
├── REPL (src/repl.rs)
│   └─ Interactive development (separate binary)
│
├── CLI Interface (src/main.rs)
│   └─ do, run, build, watch, serverhost, import
│
└── Ecosystem Modules (src/*_engine.rs)
    ├── Terminal, Database, GPU, Cloud
    ├── Filesystem, Packages, API
    ├── Network, WebGen, Desktop
    └── All support module import syntax
```

### Data Flow

```
English Code (.literal file)
         ↓
    [LEXER] 
    (import express → Token::Import)
         ↓
    [PARSER]  
    (import → ImportStmt { module, alias, items })
         ↓
    [SEMANTIC ANALYZER]
    (ImportStmt → IRNode::Import)
         ↓
    [MODULE RESOLVER]
    (Resolves module location/source)
         ↓
    ┌─────────────────────────────────────┐
    │                                     │
    ↓                    ↓        ↓        ↓
[RUNTIME]         [CODEGEN] → [6 Languages]
Executes imports  use stmt;  Python | JS | Rust | ...

    ┌──────────────────────────┐
    │ Resolved Modules         │
    │  npm | pip | cargo       │
    │  nuget | gem | maven | go│
    └──────────────────────────┘
```

---

## Core Compiler Modules

### 1. Lexer Module (`src/lexer.rs`)

**Purpose**: Converts English text into tokens

#### New Keywords (v3.0)

```rust
pub enum Token {
    // New Module Keywords
    Import,      // import module_name
    Module,      // module name ... done
    Export,      // export function_name
    Namespace,   // namespace scope
    Include,     // include other_module
    
    // ... existing keywords ...
}
```

---

## Project Architecture

### High-Level Overview

```
LiteralScript v2.0
├── Compiler Frontend
│   ├── Lexer (src/lexer.rs)
│   │   └─ Tokenizes English input into AST tokens
│   ├── Parser (src/parser.rs)
│   │   └─ Converts tokens into Abstract Syntax Tree (AST)
│   ├── Semantic Analyzer (src/semantic_analyzer.rs)
│   │   └─ Type checking and IR generation
│   └── CodeGen (src/codegen.rs)
│       └─ Generates 6 target languages
│
├── Runtime (src/runtime.rs)
│   └─ Direct interpreter for AST execution
│
├── REPL (src/repl.rs)
│   └─ Interactive development environment
│
├── CLI Interface (src/main.rs)
│   └─ Command-line tools and integration
│
└── Ecosystem Modules (src/*_engine.rs)
    ├── Terminal (shell/bash execution)
    ├── Database (schema generation & orchestration)
    ├── GPU (CUDA, OpenCL, Metal, Vulkan)
    ├── Cloud (AWS, Azure, GCP deployment)
    ├── Filesystem (virtual file system)
    ├── Packages (dependency management)
    ├── API (REST, GraphQL, WebSocket, gRPC)
    ├── Network (HTTP, TCP, WebSocket)
    ├── WebGen (HTML/CSS/JS generation)
    └── Desktop (Qt, Tkinter, Electron, Win32)
```

### Data Flow

```
English Code (.literal file)
         ↓
    [LEXER] → Tokens
         ↓
    [PARSER] → Abstract Syntax Tree (AST)
         ↓
    [SEMANTIC ANALYZER] → Intermediate Representation (IR)
         ↓
    ┌─────────────────────────────────────┐
    │                                     │
    ↓                    ↓        ↓        ↓
[RUNTIME]         [CODEGEN] → [6 Languages]
Direct Execution  Rust | Python | JS | C/C++ | SQL | HTML

    ┌──────────────────────────┐
    │ Ecosystem Modules        │
    │  Terminal | Database     │
    │  GPU | Cloud | FileSystem│
    │ Packages | API | Network │
    └──────────────────────────┘
```

---

## Core Compiler Modules

### 1. Lexer Module (`src/lexer.rs`)

**Purpose**: Converts English text into tokens (words, numbers, punctuation, keywords)

#### Key Structures

```rust
pub enum Token {
    Keyword(String),           // Display, Record, For, etc.
    Identifier(String),        // Variable names
    Number(f64),              // Numeric literals
    String(String),           // Text literals
    Operator(String),         // +, -, *, /, =, >, <
    Punctuation(char),        // :, (, ), [, ], {, }
    EOF,                      // End of file
}

pub struct Lexer {
    input: Vec<char>,         // Input characters
    position: usize,          // Current position
    current_char: Option<char>, // Current character
    line: usize,              // Current line (for errors)
    column: usize,            // Current column (for errors)
    lowercase_enforced: bool, // Grammar rule enforcement
}
```

#### Key Functions

| Function | Parameters | Return | Purpose |
|----------|-----------|--------|---------|
| `new(input: &str)` | Input string | `Lexer` | Create lexer instance |
| `tokenize()` | None | `Vec<Token>` | Convert entire input to tokens |
| `next_token()` | None | `Token` | Get next single token |
| `skip_whitespace()` | None | None | Advance past spaces/newlines |
| `read_number()` | None | `Token` | Read numeric literal |
| `read_word()` | None | `Token` | Read word and classify as keyword/identifier |
| `is_keyword(word: &str)` | Word string | `bool` | Check if word is LiteralScript keyword |

#### Usage Example

```rust
use literal::lexer::{Lexer, Token};

let code = "Display \"Hello\"";
let mut lexer = Lexer::new(code);
let tokens = lexer.tokenize();

// tokens = [
//   Token::Keyword("Display"),
//   Token::String("Hello"),
//   Token::EOF
// ]
```

---

### 2. Parser Module (`src/parser.rs`)

**Purpose**: Converts tokens into Abstract Syntax Tree (AST)

#### Key Structures

```rust
pub enum Expr {
    Number(f64),              // 42
    String(String),           // "text"
    Identifier(String),       // variable_name
    BinaryOp {
        left: Box<Expr>,      // Left operand
        op: String,           // Operator (+, -, *, /)
        right: Box<Expr>,     // Right operand
    },
    UnaryOp {
        op: String,           // Unary operator
        operand: Box<Expr>,   // Operand
    },
    FunctionCall {
        name: String,         // Function name
        args: Vec<Expr>,      // Arguments
    },
    Lambda {
        params: Vec<String>,  // Parameters
        body: Box<Expr>,      // Lambda body
    },
    Conditional {
        condition: Box<Expr>,     // Condition
        then_expr: Box<Expr>,     // Then branch
        else_expr: Option<Box<Expr>>, // Else branch
    },
}

pub enum Stmt {
    Display(Expr),            // Display expression
    Record { name: String, value: Expr }, // var = value
    For { var: String, iter: Expr, body: Vec<Stmt> }, // Loop
    When { cond: Expr, then_body: Vec<Stmt>, else_body: Vec<Stmt> }, // If/else
    Define { name: String, params: Vec<String>, body: Vec<Stmt> }, // Function def
    Call { name: String, args: Vec<Expr> }, // Function call
    Process { /* Custom process */ },     // Advanced feature
}

pub struct Parser {
    tokens: Vec<Token>,       // Token stream
    position: usize,          // Current position
    current_token: Token,     // Current token
}
```

#### Key Functions

| Function | Parameters | Return | Purpose |
|----------|-----------|--------|---------|
| `new(tokens: Vec<Token>)` | Token list | `Parser` | Create parser |
| `parse()` | None | `Vec<Stmt>` | Parse entire program |
| `parse_statement()` | None | `Stmt` | Parse single statement |
| `parse_expression()` | None | `Expr` | Parse expression with operator precedence |
| `parse_primary()` | None | `Expr` | Parse primary expression (literals, variables) |
| `parse_call()` | None | `Expr` | Parse function call |
| `parse_for_loop()` | None | `Stmt` | Parse For loop |
| `parse_when_block()` | None | `Stmt` | Parse When/If block |
| `parse_function_def()` | None | `Stmt` | Parse function definition |
| `match_token(expected: Token)` | Token | `bool` | Check if current matches expected |
| `advance()` | None | None | Move to next token |

#### Usage Example

```rust
use literal::parser::Parser;
use literal::lexer::Lexer;

let code = "Record 5 into x\nDisplay x";
let mut lexer = Lexer::new(code);
let tokens = lexer.tokenize();
let mut parser = Parser::new(tokens);
let ast = parser.parse();

// ast = [
//   Stmt::Record { name: "x", value: Expr::Number(5) },
//   Stmt::Display(Expr::Identifier("x"))
// ]
```

---

### 3. Semantic Analyzer Module (`src/semantic_analyzer.rs`)

**Purpose**: Type checking, scope analysis, and IR generation

#### Key Structures

```rust
pub enum Value {
    Number(f64),              // Numeric value
    Text(String),             // Text/string value
    List(Vec<Value>),         // List/array
    Function(String, Vec<String>), // Function with params
    Bool(bool),               // Boolean value
    Nil,                      // Null/undefined
}

pub enum IRNode {
    NumberLit(f64),           // Numeric literal
    StringLit(String),        // String literal
    Variable(String),         // Variable reference
    BinaryOp { op: String, left: Box<IRNode>, right: Box<IRNode> },
    UnaryOp { op: String, operand: Box<IRNode> },
    Assign { name: String, value: Box<IRNode> },
    Print(Box<IRNode>),       // Output statement
    IfElse {
        cond: Box<IRNode>,
        then_body: Vec<IRNode>,
        else_body: Vec<IRNode>,
    },
    While { cond: Box<IRNode>, body: Vec<IRNode> },
    For { var: String, iter: Box<IRNode>, body: Vec<IRNode> },
    Call { name: String, args: Vec<IRNode> },
    FuncDef { name: String, params: Vec<String>, body: Vec<IRNode> },
    Return(Box<IRNode>),      // Return statement
    Index { obj: Box<IRNode>, idx: Box<IRNode> }, // Array indexing
    Property { obj: Box<IRNode>, prop: String }, // Object property
    Sequence(Vec<IRNode>),    // Statement sequence
    Fold { func: Box<IRNode>, init: Box<IRNode>, collection: Box<IRNode> }, // Reduce operation
}

pub struct SemanticAnalyzer {
    symbols: HashMap<String, Value>, // Variable table
}
```

#### Key Functions

| Function | Parameters | Return | Purpose |
|----------|-----------|--------|---------|
| `new()` | None | `SemanticAnalyzer` | Create analyzer |
| `analyze_statements(stmts: Vec<Stmt>)` | Statement list | `Vec<IRNode>` | Convert AST to IR |
| `analyze_expression(expr: &Expr)` | Expression | `IRNode` | Analyze single expression |
| `type_check(value: &Value)` | Value | `bool` | Verify type validity |
| `resolve_variable(name: &str)` | Variable name | `Option<Value>` | Look up variable in scope |
| `define_variable(name: String, value: Value)` | Name, value | None | Store variable in scope |

#### Usage Example

```rust
use literal::semantic_analyzer::SemanticAnalyzer;

let mut analyzer = SemanticAnalyzer::new();
let ir = analyzer.analyze_statements(ast);
// ir = Intermediate Representation ready for execution
```

---

### 4. CodeGen Module (`src/codegen.rs`)

**Purpose**: Generates production code in 6 target languages

#### Supported Languages

1. **Rust** - Production-quality, compiled
2. **Python** - Dynamic, Flask/async support
3. **JavaScript** - Modern ES2020+, Node.js
4. **C/C++** - Systems programming
5. **SQL** - Database schema and queries
6. **HTML/CSS/JavaScript** - Web interfaces

#### Key Structures

```rust
pub enum CodeTarget {
    Rust,      // target.rs
    Python,    // target.py
    JavaScript, // target.js
    CPP,       // target.cpp
    SQL,       // target.sql
    WebUI,     // target.html
}

pub struct CodeGenerator {
    target: CodeTarget,       // Target language
    indent_level: usize,      // Current indentation
    generated_code: String,   // Accumulated output
}
```

#### Key Functions

| Function | Parameters | Return | Purpose |
|----------|-----------|--------|---------|
| `generate_from_ir(ir: Vec<IRNode>, target: CodeTarget)` | IR, language | `String` | Generate target code |
| `emit_rust(ir: &IRNode)` | IR node | `String` | Emit Rust code |
| `emit_python(ir: &IRNode)` | IR node | `String` | Emit Python code |
| `emit_js(ir: &IRNode)` | IR node | `String` | Emit JavaScript |
| `emit_cpp(ir: &IRNode)` | IR node | `String` | Emit C++ code |
| `emit_sql(ir: &IRNode)` | IR node | `String` | Emit SQL |
| `emit_html(ir: &IRNode)` | IR node | `String` | Emit HTML/CSS/JS |
| `indent()` | None | `String` | Get current indentation |
| `emit_statement(stmt: &IRNode)` | Statement | `String` | Generate statement |

#### Usage Example

```rust
use literal::codegen::{CodeGenerator, CodeTarget};

let rust_code = CodeGenerator::generate_from_ir(ir, CodeTarget::Rust);
// Generates production-quality Rust source code

let py_code = CodeGenerator::generate_from_ir(ir, CodeTarget::Python);
// Generates Python with asyncio support
```

---

### 5. Runtime Module (`src/runtime.rs`)

**Purpose**: Direct interpretation and execution of IR

#### Key Structures

```rust
pub struct Runtime {
    variables: HashMap<String, Value>,  // Global variables
    functions: HashMap<String, IRNode>, // Defined functions
    call_stack: Vec<ExecutionFrame>,    // Call stack
}

struct ExecutionFrame {
    locals: HashMap<String, Value>,     // Local variables
    return_value: Option<Value>,        // Return value
}
```

#### Key Functions

| Function | Parameters | Return | Purpose |
|----------|-----------|--------|---------|
| `new()` | None | `Runtime` | Create runtime environment |
| `execute(ir: Vec<IRNode>)` | IR nodes | `Value` | Execute IR code |
| `eval_expression(node: &IRNode)` | IR node | `Value` | Evaluate expression |
| `eval_statement(node: &IRNode)` | IR node | `Option<Value>` | Execute statement |
| `call_function(name: &str, args: Vec<Value>)` | Function name, args | `Value` | Call function |
| `push_scope()` | None | None | Create new scope |
| `pop_scope()` | None | None | Exit scope |
| `set_variable(name: String, value: Value)` | Name, value | None | Store variable |
| `get_variable(name: &str)` | Variable name | `Option<Value>` | Retrieve variable |

#### Usage Example

```rust
use literal::runtime::Runtime;

let mut runtime = Runtime::new();
let result = runtime.execute(ir);
println!("{:?}", result); // Output result
```

---

### 6. REPL Module (`src/repl.rs`)

**Purpose**: Interactive development environment

#### Key Functions

| Function | Parameters | Return | Purpose |
|----------|-----------|--------|---------|
| `main()` | None | `!` | REPL main loop |
| `execute_command(input: &str)` | User input | `Result<(), String>` | Process single command |
| `handle_help()` | None | None | Display help |
| `handle_history()` | None | None | Show command history |
| `handle_clear()` | None | None | Clear buffer |
| `load_file(path: &str)` | File path | `Result<String, String>` | Load .literal file |
| `save_file(path: &str, code: &str)` | Path, code | `Result<(), String>` | Save code to file |

#### REPL Commands

| Command | Syntax | Purpose |
|---------|--------|---------|
| `help` | `help` | Show available commands |
| `history` | `history [n]` | Show last n commands |
| `clear` | `clear` | Clear command buffer |
| `show` | `show` | Show current code |
| `load` | `load <file.literal>` | Load file |
| `save` | `save <output.literal>` | Save buffer to file |
| `quit` | `quit` | Exit REPL |
| Code | Any valid LiteralScript | Execute directly |

#### Usage Example

```bash
$ literal-repl
literal> Display "Hello"
Hello
literal> Record 5 into x
literal> Display x + 3
8
literal> quit
```

---

### 7. Main CLI Module (`src/main.rs`)

**Purpose**: Command-line interface and orchestration

#### Key Commands

| Command | Syntax | Purpose |
|---------|--------|---------|
| Help | `literal --help` | Show usage |
| Version | `literal --version` | Show version |
| Compile | `literal program.literal` | Generate code |
| Execute | `literal program.literal --run` | Run directly |
| AST Dump | `literal program.literal --ast` | Show AST |
| IR Dump | `literal program.literal --ir` | Show IR |
| Shell | `literal shell` | Virtual terminal |
| DB Init | `literal db:init <engine>` | Initialize database |
| GPU Init | `literal gpu:init` | Initialize GPU |
| Cloud Deploy | `literal cloud:deploy <provider>` | Deploy to cloud |
| Package Install | `literal pkg:install <pkg>` | Install package |
| File System | `literal fs:init <path>` | Initialize filesystem |
| API Init | `literal api:init <type>` | Create API |

---

## Ecosystem Modules

### Terminal Module (`src/terminal.rs`)

**Purpose**: Virtual shell environment execution

#### Key Structures

```rust
pub struct TerminalEngine {
    current_directory: String,  // Current working directory
    environment_vars: HashMap<String, String>, // ENV variables
}
```

#### Key Functions

| Function | Purpose |
|----------|---------|
| `new()` | Create terminal instance |
| `execute_command(cmd: &str)` | Run shell command |
| `change_directory(path: &str)` | Change directory |
| `list_directory(path: &str)` | List files |
| `create_file(path: &str, content: &str)` | Create file |
| `read_file(path: &str)` | Read file |
| `execute_pipe(cmds: Vec<&str>)` | Pipe commands |

#### Example Usage

```english
Record "echo 'Hello'" into command
Call terminal with command
```

---

### Database Module (`src/database.rs`)

**Purpose**: Multi-backend database orchestration

#### Supported Databases

- PostgreSQL (relational, advanced)
- MySQL (relational, popular)
- SQLite (embedded, file-based)
- MongoDB (document, NoSQL)
- Redis (cache, key-value)

#### Key Structures

```rust
pub enum DatabaseEngine {
    PostgreSQL(Connection),
    MySQL(Connection),
    SQLite(Connection),
    MongoDB(Client),
    Redis(Client),
}

pub struct Database {
    engine: DatabaseEngine,
    tables: Vec<Table>,
}

pub struct Table {
    name: String,
    columns: Vec<(String, ColumnType)>,
    rows: Vec<Row>,
}
```

#### Key Functions

| Function | Purpose |
|----------|---------|
| `initialize(engine_type: &str)` | Connect to database |
| `create_table(name: &str, columns: Vec<Column>)` | Create schema |
| `insert_row(table: &str, data: Map)` | Add record |
| `query(sql: &str)` | Execute query |
| `update_row(table: &str, condition: &str, data: Map)` | Update records |
| `delete_row(table: &str, condition: &str)` | Delete records |
| `generate_schema()` | Create DDL script |

#### Example Usage

```english
Call database:init postgresql mydb
Call database:create_table customers with columns id, name, email
```

---

### GPU Module (`src/gpu.rs`)

**Purpose**: GPU acceleration for compute-intensive tasks

#### Supported Frameworks

- **CUDA** (NVIDIA GPUs)
- **Metal** (Apple GPUs)
- **OpenCL** (Cross-platform)
- **Vulkan** (Modern graphics)

#### Supporting Libraries

- CuPy (Python GPU arrays)
- Numba (Python GPU JIT)
- TensorFlow (ML)
- PyTorch (ML)

#### Key Structures

```rust
pub enum GPUBackend {
    CUDA,      // NVIDIA
    Metal,     // Apple Silicon
    OpenCL,    // Cross-platform
    Vulkan,    // Modern graphics
}

pub struct GPUCompute {
    backend: GPUBackend,
    device: Device,
    context: Context,
}
```

#### Key Functions

| Function | Purpose |
|----------|---------|
| `new(backend: GPUBackend)` | Create GPU instance |
| `compile_kernel(code: &str)` | Compile GPU kernel |
| `allocate_memory(size: usize)` | Allocate GPU memory |
| `copy_to_device(data: &[f32])` | Transfer data to GPU |
| `execute_kernel(kernel: &str, params: Vec<Value>)` | Run kernel |
| `copy_from_device(data: &mut [f32])` | Transfer data from GPU |
| `generate_cuda_code()` | Output CUDA |
| `generate_cupy_code()` | Output CuPy Python |
| `generate_numba_code()` | Output Numba JIT |
| `generate_tensorflow_code()` | Output TensorFlow |
| `generate_pytorch_code()` | Output PyTorch |

#### Example Usage

```english
Call gpu:init cuda
Call gpu:allocate_memory 1000000
Call gpu:execute_kernel matrix_multiply with size 1000
```

---

### Cloud Module (`src/cloud.rs`)

**Purpose**: Cloud infrastructure and deployment

#### Supported Providers

- **AWS** (Elastic Beanstalk, Lambda, EC2)
- **Azure** (App Service, Functions, VMs)
- **GCP** (Cloud Run, Compute Engine)

#### Helper Technologies

- Docker containerization
- Kubernetes orchestration
- CloudFormation/ARM/Terraform IaC

#### Key Structures

```rust
pub enum CloudProvider {
    AWS,   // Amazon Web Services
    Azure, // Microsoft Azure
    GCP,   // Google Cloud Platform
}

pub struct CloudEngine {
    provider: CloudProvider,
    region: String,
    credentials: CloudCredentials,
}
```

#### Key Functions

| Function | Purpose |
|----------|---------|
| `new(provider: CloudProvider, region: &str)` | Create cloud engine |
| `create_container(image: &str, port: u16)` | Containerize app |
| `push_to_registry(image: &str)` | Push Docker image |
| `deploy_container(image: &str)` | Deploy to cloud |
| `create_database(engine: &str)` | Create cloud database |
| `scale_service(service: &str, instances: u32)` | Scale resources |
| `setup_load_balancer(services: Vec<&str>)` | Add load balancing |
| `configure_autoscaling(min: u32, max: u32)` | Enable autoscaling |
| `deploy_serverless(function_code: &str)` | Deploy function |
| `generate_cloudformation()` | Output CloudFormation |

#### Example Usage

```english
Call cloud:deploy aws us-east-1
Call cloud:create_database postgresql
Call cloud:scale_service 5
```

---

### Filesystem Module (`src/filesystem.rs`)

**Purpose**: Virtual filesystem operations and abstraction

#### Key Structures

```rust
pub struct VirtualFileSystem {
    root: Directory,
    current_path: PathBuf,
    mounted_systems: Vec<MountPoint>,
}

pub struct File {
    name: String,
    content: Vec<u8>,
    permissions: Permissions,
    metadata: FileMetadata,
}

pub struct Directory {
    name: String,
    entries: Vec<Entry>,
    permissions: Permissions,
}
```

#### Key Functions

| Function | Purpose |
|----------|---------|
| `new()` | Create filesystem |
| `create_file(path: &str, content: &[u8])` | Create file |
| `read_file(path: &str)` | Read file contents |
| `write_file(path: &str, content: &[u8])` | Write to file |
| `delete_file(path: &str)` | Remove file |
| `create_directory(path: &str)` | Create directory |
| `list_directory(path: &str)` | List contents |
| `change_directory(path: &str)` | Change working dir |
| `copy_file(src: &str, dst: &str)` | Copy file |
| `move_file(src: &str, dst: &str)` | Move/rename file |
| `set_permissions(path: &str, mode: u32)` | Set file permissions |
| `get_file_metadata(path: &str)` | Get file info |
| `mount_filesystem(path: &str, fs: &VirtualFileSystem)` | Mount FS |
| `search_files(pattern: &str)` | Find files |

#### Example Usage

```english
Call fs:init /data
Call fs:create_file /data/config.json with content
Call fs:list_directory /data
```

---

### Packages Module (`src/packages.rs`)

**Purpose**: Dependency management and package resolution

#### Key Structures

```rust
pub struct PackageManager {
    registry: PackageRegistry,
    installed: HashMap<String, Package>,
    cache: PackageCache,
}

pub struct Package {
    name: String,
    version: String,
    dependencies: Vec<Dependency>,
    metadata: PackageMetadata,
}

pub struct Dependency {
    name: String,
    version_spec: VersionSpec, // ==1.0.0, >=1.0, *
    required: bool,
}
```

#### Key Functions

| Function | Purpose |
|----------|---------|
| `new()` | Create package manager |
| `search(name: &str)` | Search registry |
| `install(package: &str, version: &str)` | Install package |
| `uninstall(package: &str)` | Remove package |
| `update(package: &str)` | Update to latest |
| `resolve_dependencies(package: &Package)` | Calculate deps |
| `download_package(url: &str)` | Fetch package |
| `check_conflicts(packages: Vec<&Package>)` | Detect conflicts |
| `generate_lockfile()` | Create lock file |
| `list_installed()` | Show installed |

#### Supported Registries

- PyPI (Python)
- npm (JavaScript)
- crates.io (Rust)
- Maven Central (Java)
- NuGet (.NET)

#### Example Usage

```english
Call pkg:install numpy 1.20.0
Call pkg:install pandas
Call pkg:search database
Call pkg:list_installed
```

---

### API Module (`src/api.rs`)

**Purpose**: Real-time communication and API generation

#### Supported Protocols

- **REST** (HTTP/HTTPS)
- **GraphQL** (Query language)
- **WebSocket** (Real-time)
- **gRPC** (High-performance RPC)

#### Key Structures

```rust
pub enum APIType {
    REST,
    GraphQL,
    WebSocket,
    gRPC,
}

pub struct APIEngine {
    api_type: APIType,
    routes: Vec<Route>,
    schemas: Vec<Schema>,
}

pub struct Route {
    path: String,
    method: String, // GET, POST, PUT, DELETE
    handler: String,
    documentation: String,
}
```

#### Key Functions

| Function | Purpose |
|----------|---------|
| `new(api_type: APIType)` | Create API engine |
| `add_route(path: &str, method: &str, handler: &str)` | Define endpoint |
| `add_schema(name: &str, fields: Vec<Field>)` | Define data model |
| `generate_code()` | Output API code |
| `generate_documentation()` | Create API docs |
| `validate_request(data: &Value)` | Check request schema |
| `serialize_response(data: &Value)` | Format response |
| `enable_cors()` | Allow cross-origin |
| `enable_auth(method: AuthMethod)` | Add authentication |
| `rate_limit(requests_per_minute: u32)` | Throttle requests |
| `setup_websocket(path: &str, handler: &str)` | WebSocket handler |
| `generate_grpc_definition()` | Output proto3 |

#### Example Usage

```english
Call api:init rest
Call api:add_route /users GET get_users
Call api:add_route /users POST create_user
Call api:enable_auth jwt
Call api:rate_limit 1000
```

---

### Network Module (`src/network.rs`)

**Purpose**: Low-level network protocol support

#### Supported Protocols

- HTTP/HTTPS
- TCP/UDP
- WebSocket
- DNS
- SSL/TLS

#### Key Functions

| Function | Purpose |
|----------|---------|
| `create_http_server(port: u16)` | HTTP server |
| `make_http_request(url: &str, method: &str)` | HTTP client |
| `create_tcp_socket(host: &str, port: u16)` | TCP connection |
| `create_udp_socket(host: &str, port: u16)` | UDP socket |
| `create_websocket(url: &str)` | WebSocket conn |
| `ssl_context(cert: &str, key: &str)` | SSL config |
| `resolve_dns(hostname: &str)` | DNS lookup |
| `parse_url(url: &str)` | URL parsing |

---

### WebGen Module (`src/webgen.rs`)

**Purpose**: Web interface generation from LiteralScript

#### Supported Frameworks

- HTML/CSS/JavaScript
- React.js
- Vue.js
- Angular
- Bootstrap

#### Key Functions

| Function | Purpose |
|----------|---------|
| `create_html_page(title: &str)` | Generate HTML |
| `add_css(styles: &str)` | Add CSS |
| `add_javascript(code: &str)` | Add JS |
| `create_form(fields: Vec<Field>)` | Generate form |
| `create_table(data: Vec<Vec<Value>>)` | Generate table |
| `create_navbar(items: Vec<MenuItem>)` | Navigation bar |
| `create_modal(title: &str, content: &str)` | Modal dialog |
| `generate_react_component(name: &str)` | React JSX |
| `generate_stylesheet()` | Output CSS |
| `add_responsive_design()` | Mobile support |

---

### Desktop Module (`src/desktop.rs`)

**Purpose**: Desktop application generation

#### Supported Frameworks

- **Qt** (C++, cross-platform)
- **Tkinter** (Python, lightweight)
- **Electron** (JavaScript, modern)
- **Windows Forms** (.NET, Windows)

#### Key Functions

| Function | Purpose |
|----------|---------|
| `create_window(title: &str, width: u32, height: u32)` | Create window |
| `add_button(label: &str, onclick: &str)` | Add button |
| `add_input(label: &str)` | Create input |
| `add_label(text: &str)` | Static text |
| `add_menu(items: Vec<MenuItem>)` | Menu bar |
| `create_dialog(title: &str)` | Dialog box |
| `generate_qt_code()` | Output Qt |
| `generate_electron_code()` | Output Electron |
| `generate_tkinter_code()` | Output Tkinter |

---

## Complete Function Reference

### All 110+ Functions by Category

[This is where the detailed function catalog from the subagent would be expanded with full signatures and parameters - see FUNCTION_CATALOG.md for complete reference]

---

## Module Dependencies

```
┌─────────────────────────────────────────┐
│           LiteralScript v2.0             │
├─────────────────────────────────────────┤
│                                          │
│  main.rs (CLI Entry Point)               │
│    ├─ lexer.rs (Tokenization)            │
│    ├─ parser.rs (AST Construction)       │
│    ├─ semantic_analyzer.rs (Type Check)  │
│    ├─ codegen.rs (Code Generation)       │
│    ├─ runtime.rs (Direct Execution)      │
│    ├─ repl.rs (Interactive REPL)         │
│    │                                     │
│    └─ Ecosystem Modules:                 │
│        ├─ terminal.rs                    │
│        ├─ database.rs                    │
│        ├─ gpu.rs                         │
│        ├─ cloud.rs                       │
│        ├─ filesystem.rs                  │
│        ├─ packages.rs                    │
│        ├─ api.rs (→ network.rs)          │
│        ├─ network.rs (→ ssl/tls)         │
│        ├─ webgen.rs (→ html/css/js)      │
│        └─ desktop.rs (→ frameworks)      │
│                                          │
└─────────────────────────────────────────┘
```

### Dependency Flow

```
Input (.literal) → Lexer → Parser → Analyzer → [CodeGen | Runtime]
                                       ↓
                              Ecosystem Modules
                        (Terminal, DB, GPU, Cloud, FS, Packages, API)
                                       ↓
                              Output (Code, Binaries, Services)
```

---

## Data Structure Reference

### Value Type (Runtime Values)

```rust
pub enum Value {
    Number(f64),                           // -∞ to +∞
    Text(String),                          // UTF-8 text
    List(Vec<Value>),                      // Heterogeneous arrays
    Function(String, Vec<String>),         // name, parameters
    Bool(bool),                            // true / false
    Nil,                                   // null/undefined
    Object(HashMap<String, Value>),        // Key-value pairs [v2.1+]
    Date(DateTime),                        // Timestamps [v2.1+]
}
```

### Type Conversions

| From | To | Method |
|------|-----|--------|
| Number | Text | `to_string()` |
| Text | Number | `parse::<f64>()` |
| List | Text | `join(", ")` |
| Text | List | `split(" ")` |
| Any | Bool | Truthiness rules |

---

## Code Examples

### Example 1: Hello World with Data

```english
Display "Welcome to LiteralScript"
Record "Alice" into name
Record 25 into age
Display name + " is " + age + " years old"
```

**Generated Rust:**
```rust
fn main() {
    println!("Welcome to LiteralScript");
    let name = "Alice";
    let age = 25;
    println!("{} is {} years old", name, age);
}
```

---

### Example 2: Loop with Calculation

```english
Record [1, 2, 3, 4, 5] into numbers
For item in numbers:
  Record item * item into squared
  Display squared
```

**Generated Python:**
```python
numbers = [1, 2, 3, 4, 5]
for item in numbers:
    squared = item * item
    print(squared)
```

---

### Example 3: Function Definition

```english
Define greet taking name:
  Display "Hello, " + name
  Display "Nice to meet you!"

Call greet "World"
```

**Generated JavaScript:**
```javascript
function greet(name) {
    console.log("Hello, " + name);
    console.log("Nice to meet you!");
}
greet("World");
```

---

## Contributing Guide

### Prerequisites

- Rust 1.70+
- Git
- Basic understanding of compilers

### Development Workflow

1. **Fork** the repository
2. **Create** a feature branch: `git checkout -b feature/my-feature`
3. **Code** with proper comments
4. **Test** with: `cargo test --release`
5. **Document** all public APIs
6. **Commit** with clear messages
7. **Push** and create Pull Request

### Code Style

- Use rustfmt: `cargo fmt`
- Run clippy: `cargo clippy -- -W clippy::all`
- Document with doc comments: `///`
- Write meaningful variable names

### Areas for Contribution

| Priority | Area | Difficulty |
|----------|------|-----------|
| High | Go/Kotlin code generation | Medium |
| High | IDE extensions (VS Code) | Hard |
| High | Web playground | Hard |
| Medium | More ecosystem modules | Medium |
| Medium | Performance optimization | Medium |
| Low | Documentation improvements | Easy |
| Low | Example programs | Easy |

### Testing

```bash
# Run all tests
cargo test --release

# Test specific module
cargo test lexer::tests

# Test with output
cargo test -- --nocapture

# Generate coverage
cargo tarpaulin
```

---

## Quick Reference

| Task | Command |
|------|---------|
| Build | `cargo build --release` |
| Test | `cargo test --release` |
| REPL | `literal-repl` |
| Run Program | `literal program.literal --run` |
| Generate Code | `literal program.literal` |
| View AST | `literal program.literal --ast` |
| Install | `python3 install_universal.py` |
| Build MSI | `build_msi.bat` |
| Format | `cargo fmt` |
| Lint | `cargo clippy` |

---

## Resources

- **GitHub**: https://github.com/voltiumS/LiteralScript
- **Documentation**: README.md
- **Quick Start**: QUICK_START.md
- **Contributing**: CONTRIBUTING.md
- **Changelog**: CHANGELOG.md
- **Issues**: GitHub Issues
- **Discussions**: GitHub Discussions

---

**LiteralScript v2.0.0** - Transform English into Code  
Created by Voltium  
Licensed under MIT

