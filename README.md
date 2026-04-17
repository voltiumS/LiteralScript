# LiteralScript

**Transform English into Code** — A natural language programming language that generates production code in 6 languages.

![Status](https://img.shields.io/badge/status-%20not%20ready-red)  
![Version](https://img.shields.io/badge/version-1.0.5-blue)  
![License](https://img.shields.io/badge/license-MIT-green)

---

## 🚀 Quick Start

### Installation (Choose Your Platform)

**Windows** (Automated):
```bash
cd installers
setup.bat
```

**macOS/Linux** (Cross-Platform):
```bash
python3 installers/install_universal.py
```

**From Source** (Any Platform):
```bash
cargo build --release
```

### First Program

Create `hello.literal`:
```english
Display "Hello, LiteralScript!"
```

Run it:
```bash
literal hello.literal --run
```

**Output**: `Hello, LiteralScript!`

---

## 📚 Documentation

All documentation is organized in the `docs/` folder:

| Document | Purpose | Audience |
|----------|---------|----------|
| **[CODING_TUTORIAL.md](docs/CODING_TUTORIAL.md)** | **Complete guide on how to code in LiteralScript** | Everyone |
| [QUICK_START.md](docs/QUICK_START.md) | Your first program (5 min) | Beginners |
| [API_COMPLETE_REFERENCE.md](docs/API_COMPLETE_REFERENCE.md) | All 110+ functions documented | Developers |
| [INSTALLATION_GUIDE.md](docs/INSTALLATION_GUIDE.md) | Detailed installation help | Users |
| [CONTRIBUTING.md](docs/CONTRIBUTING.md) | How to contribute | Contributors |
| [CHANGELOG.md](docs/CHANGELOG.md) | Version history | Everyone |

---

## 📁 Project Structure

```
LiteralScript/
├── docs/                          Documentation & guides
│   ├── CODING_TUTORIAL.md         ⭐ START HERE
│   ├── QUICK_START.md
│   ├── API_COMPLETE_REFERENCE.md
│   ├── INSTALLATION_GUIDE.md
│   ├── CONTRIBUTING.md
│   ├── CHANGELOG.md
│   └── LICENSE
│
├── src/            Source code (17 modules, 6000+ lines)
NOT READY - COME BACK SOON
│
├── installers/                    Installation tools
NOT READY - COME BACK SOON
│
├── tools/                         Build utilities
NOT READY - COME BACK SOON
│
├── .github/                       GitHub configuration
│   └── workflows/
│       └── build.yml              CI/CD pipeline
│
├── target/                        Compiled binaries & artifacts
│   └── release/
│       ├── literal.exe            Main compiler (542 KB)
│       └── literal-repl.exe       Interactive REPL (503 KB)
│
├── Cargo.toml                     Project manifest
├── .gitignore                     Git exclusions
└── LICENSE                        MIT License
```

---

## ✨ Key Features

### 🎯 Natural Language Programming
Write code in English, not symbols:
```english
Display "Hello"
Record 42 into number
For item in [1, 2, 3]:
  Display item
```

### 🚀 Multi-Language Code Generation
Generate production code in 6 languages:
- **Rust** (compiled, production-quality)
- **Python** (Flask, asyncio)
- **JavaScript** (modern ES2020+)
- **C/C++** (systems programming)
- **SQL** (database schemas)
- **HTML/CSS/JavaScript** (web UIs)

### 🛠 Complete Ecosystem
- Virtual terminal with shell commands
- Multi-backend database (PostgreSQL, MySQL, MongoDB, Redis, SQLite)
- GPU acceleration (CUDA, Metal, OpenCL, Vulkan)
- Cloud deployment (AWS, Azure, GCP)
- API generation (REST, GraphQL, WebSocket, gRPC)
- Package management
- Desktop app generation

### 🎮 Interactive REPL
```bash
literal-repl
literal> Display "Hello"
literal> Record 5 into x
literal> Display x * 2
8
literal> quit
```

---

## 💻 Installation

### Windows (Easiest)
```bash
cd installers
setup.bat
```
Then choose installation method (portable/PATH/MSI)

### macOS/Linux
```bash
python3 installers/install_universal.py
# or
bash installers/install.sh
```

### From Source (Any Platform)
```bash
cargo build --release
# Binaries in: target/release/
```

See [INSTALLATION_GUIDE.md](docs/INSTALLATION_GUIDE.md) for detailed instructions.

---

## 📖 Learning Path

1. **Start**: Read [CODING_TUTORIAL.md](docs/CODING_TUTORIAL.md) — Complete guide on how to code in LiteralScript
2. **Quick**: Try [examples/](examples/) — Run example programs
3. **Reference**: Check [API_COMPLETE_REFERENCE.md](docs/API_COMPLETE_REFERENCE.md) — All functions documented
4. **Create**: Build your own program

---

## 🎓 Language Basics

### Variable Assignment
```english
Record 42 into age
Record "Alice" into name
Record [1, 2, 3] into numbers
```

### Display Output
```english
Display "Hello, World!"
Display age
Display age + 10
```

### Conditionals
```english
When age greater than 18:
  Display "Adult"
Otherwise:
  Display "Minor"
```

### Loops
```english
For item in [1, 2, 3]:
  Display item
```

### Functions
```english
Define greet taking name:
  Display "Hello, " + name

Call greet "Alice"
```

For more, see [CODING_TUTORIAL.md](docs/CODING_TUTORIAL.md).

---

## 📊 Statistics

| Metric | Value |
|--------|-------|
| **Total Lines of Code** | 6,000+ |
| **Modules** | 17 |
| **Functions Documented** | 110+ |
| **Code Generation Targets** | 6 languages |
| **Compilation Status** | 0 errors |
| **Binary Size** | ~1 MB |
| **Build Time** | ~4 seconds |

---

## 🛠 Commands

### Compiler
```bash
literal program.literal                   # Generate code
literal program.literal --run             # Execute
literal program.literal --ast             # Show AST
literal program.literal --ir              # Show IR
literal --help                            # Show help
literal --version                         # Show version
```

### REPL
```bash
literal-repl                              # Interactive shell
```

### Ecosystem
```bash
literal shell                             # Virtual terminal
literal db:init postgresql mydb           # Database
literal gpu:init                          # GPU acceleration
literal cloud:deploy aws us-east-1        # Cloud deployment
literal pkg:install numpy                 # Packages
literal fs:init /data                     # Filesystem
literal api:init rest                     # API generation
```

---

## 📦 Requirements

### Minimum
- Windows 7 SP1+ / macOS 10.13+ / Linux (Ubuntu 18.04+)
- 100 MB disk space
- No external dependencies (binary distribution)

### Build from Source
- Rust 1.70+
- Cargo
- Git

---

## 🤝 Contributing

We welcome contributions! See [CONTRIBUTING.md](docs/CONTRIBUTING.md) for:
- Development setup
- Coding standards
- How to submit PRs
- Areas for contribution

---

## 📄 License

MIT License — See [LICENSE](docs/LICENSE) for details.

Free to use, modify, and distribute.

---

## 🔗 Resources

- **GitHub**: https://github.com/voltiumS/LiteralScript
- **Issues**: Report bugs on GitHub
- **Discussions**: GitHub Discussions

---

## 🎯 What's New in v2.0

✅ Interactive REPL interpreter  
✅ 7 Ecosystem modules (Terminal, Database, GPU, Cloud, Filesystem, Packages, API)  
✅ Windows MSI professional installer  
✅ Cross-platform Python installer  
✅ GitHub Actions CI/CD  
✅ Complete documentation (CODING_TUTORIAL.md)  
✅ 110+ functions documented  

---

## 💡 Examples

### Hello World
```english
Display "Hello, World!"
```

### Calculator
```english
Record 10 into x
Record 20 into y
Display x + y           # Output: 30
```

### Loop
```english
For i in [1, 2, 3, 4, 5]:
  Display i * i
```

### Function
```english
Define add taking a, b:
  Display a + b

Call add 5, 3           # Output: 8
```

See [examples/](examples/) for more programs.

---

## 🚀 Getting Help

1. **Read Documentation**: [docs/CODING_TUTORIAL.md](docs/CODING_TUTORIAL.md)
2. **Check Examples**: Run programs in [examples/](examples/)
3. **API Reference**: [docs/API_COMPLETE_REFERENCE.md](docs/API_COMPLETE_REFERENCE.md)
4. **File Issues**: GitHub Issues
5. **Discuss**: GitHub Discussions

---

**LiteralScript v2.0.0** — Transform English into Code  
Created by Voltium | MIT License

