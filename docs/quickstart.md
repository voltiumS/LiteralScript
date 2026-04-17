# LiteralScript v3.0 Quick Start Guide

**Now with Module System, Import Support & New Commands!**

## 🚀 Installation

### Windows (MSI Installer) - RECOMMENDED
1. Download `LiteralScript-Setup.msi` from Releases
2. Run the installer
3. Choose installation location
4. Click "Install"
5. `literal` and `literal-repl` are now in your PATH

### macOS/Linux (From Source)
```bash
git clone https://github.com/voltiumS/LiteralScript.git
cd LiteralScript
./install.sh
```

### Or Build Manually
```bash
cargo install --path .
```

---

## ✨ Your First Program

### Method 1: Using `do` (Execute Immediately)

Create a file `hello.literal`:
```english
Display "Hello, LiteralScript!"
Record 42 into answer
Display answer
```

Run it with the new `do` command:
```bash
literal do hello.literal
```

Output:
```
Hello, LiteralScript!
42
```

### Method 2: Using `build` (Compile/Interpret)

```bash
# Compile to Rust
literal build hello.literal

# Interpret instead
literal build hello.literal --interpret
```

---

## 📦 Using Modules (NEW!)

### Import a Package

```english
import express
import pandas as pd
import numpy

Display "Modules loaded!"
```

Run: `literal do app.literal`

### Create Your Own Module

**math_utils.literal**:
```english
module math_utils

  record function add using a, b
    Record a + b into result
    Display result
  done

done
```

Use in another file:
```english
import math_utils

add using 5, 3
```

See [MODULE_SYSTEM.md](MODULE_SYSTEM.md) for complete module documentation!

---

## 🎮 Interactive REPL

Launch the interactive interpreter:
```bash
literal-repl
```

Then try:
```
literal> Display "Hello"
literal> Record 5 into x
literal> Display x * 2
literal> help
literal> quit
```

---

## 📝 Language Basics

### Variables
```english
Record 42 into number
Record "text" into message
Record [1, 2, 3] into list
```

### Loops
```english
Record [1, 2, 3] into list
For item in list:
  Display item
```

### Conditionals
```english
Record 10 into x
When x greater than 5 then:
  Display "Big"
Otherwise:
  Display "Small"
```

### Imports (NEW!)
```english
import numpy from array, math
import pandas as pd
import express
```

---

## 🔧 Command Reference v3.0

### Core Execution Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `do` | Execute file immediately | `literal do app.literal` |
| `run` | Execute file (alias for `do`) | `literal run app.literal` |
| `build` | Compile or interpret file | `literal build app.literal` |
| `watch` | Auto-rebuild on file change | `literal watch app.literal` |
| `serverhost` | Start HTTP server | `literal serverhost api.literal --port 8080` |

### Module Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `import <module>` | Load and resolve module | `literal import numpy` |
| `import <module> --info` | Get module information | `literal import flask --info` |
| `import --list` | List available packages | `literal import --list` |

### Traditional Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `<file.literal> --run` | Execute with interpreter | `literal hello.literal --run` |
| `<file.literal> --ast` | Show AST | `literal hello.literal --ast` |
| `<file.literal> --ir` | Show IR | `literal hello.literal --ir` |

---

## 🌐 Server Hosting (NEW!)

Create a simple REST API:

**api.literal**:
```english
Display "Server starting..."

record function hello_endpoint
  Display "Hello from LiteralScript!"
done

record function get_data
  Display "Returning data..."
done
```

Host it as a server:
```bash
literal serverhost api.literal --port 3000
```

Access endpoints at `http://localhost:3000`

---

## ⏱️ Watch Mode (NEW!)

For development, auto-rebuild on save:

```bash
literal watch myapp.literal
```

Your file is re-compiled automatically whenever you save. Perfect for active development!

---

## 📚 More Resources

- **[MODULE_SYSTEM.md](MODULE_SYSTEM.md)** - Complete module system guide
- **[CODING_TUTORIAL.md](CODING_TUTORIAL.md)** - Language features & syntax
- **[API_COMPLETE_REFERENCE.md](API_COMPLETE_REFERENCE.md)** - Full API documentation
- **[CHANGELOG.md](CHANGELOG.md)** - Version history & release notes

```bash
# Execute directly
literal program.literal --run

# Generate code (see .literal.output/)
literal program.literal

# View abstract syntax tree
literal program.literal --ast

# View intermediate representation
literal program.literal --ir
```

---

## 🌐 Code Generation

LiteralScript automatically generates production code in 6 languages:

```bash
literal program.literal
```

Generates:
- `program.rs` - Rust (production)
- `program.py` - Python
- `program.js` - JavaScript
- `program.cpp` - C++
- `program.sql` - SQL schema
- `program.html` - HTML/CSS/JS

---

## 🛠 Integrated Environment

### Virtual Terminal
```bash
literal shell
```

### Database Orchestration
```bash
literal db:init postgresql mydb
# or: mysql, sqlite, mongodb, redis
```

### GPU Acceleration
```bash
literal gpu:init
# Supports: CUDA, Metal, OpenCL, Vulkan
```

### Cloud Deployment
```bash
literal cloud:deploy aws us-east-1
# or: azure, gcp
```

### Package Management
```bash
literal pkg:install numpy pandas
```

### File System
```bash
literal fs:init /data
```

### APIs
```bash
literal api:init rest http://localhost:8000
# or: graphql, websocket, grpc
```

---

## 📚 Examples

Check the `examples/` folder:
```bash
literal examples/hello.literal --run
literal examples/sum_numbers.literal --run
literal examples/list_processing.literal --run
```

---

## 💡 Tips

1. **Development Workflow**: Use `literal-repl` for testing, then create `.literal` files
2. **Code Generation**: View generated code to understand output targets
3. **Performance**: Generated Rust code is production-ready and optimized
4. **Documentation**: Run `literal --help` for all commands

---

## ❓ Need Help?

```bash
# Get all commands
literal --help

# Get language reference
literal-repl help

# View documentation
cat README.md
```

---

## 🐛 Report Issues

Create an issue on GitHub with:
1. Your program
2. Expected output
3. Actual output
4. OS and version

---

## 🤝 Contribute

See `CONTRIBUTING.md` for guidelines on:
- Adding new features
- Reporting bugs
- Improving documentation
- Code style and standards

---

Happy coding! 🎉

