# CHANGELOG

All notable changes to LiteralScript are documented in this file.

---

## [3.0.0] - April 17, 2026

### ✨ Major Features Added

#### Module System 🎉
- **Complete Import System**: Import modules and packages from any programming language
  - Python (pip): `import pandas`, `import numpy`
  - JavaScript (npm): `import express`, `import axios`
  - Rust (cargo): `import tokio`, `import serde`
  - .NET (nuget), Java (maven), Ruby (gem), Go modules
- **Custom Module Definition**: Create reusable code modules
  - `module mylib; ... done module`
  - `export` to expose functions
  - Module namespacing and organization
- **Module Resolver**: Smart module discovery and installation
  - Automatic package source detection
  - Cross-language package mapping
  - Built-in registry of 50+ popular packages
- **Import Syntax**:
  - Basic: `import express`
  - With alias: `import pandas as pd`
  - Selective: `import numpy from array, reshape`

#### New CLI Commands 🚀
- **`literal do`** - Execute .literal files immediately
  - `literal do hello.literal`
  - Direct interpretation mode
  - Immediate execution without compilation
  
- **`literal run`** - Alias for `do` command
  - `literal run app.literal`
  
- **`literal build`** - Compile or interpret files
  - `literal build app.literal` (compile to Rust)
  - `literal build app.literal --interpret` (direct execution)
  
- **`literal watch`** - Auto-rebuild on file changes
  - `literal watch myapp.literal`
  - Continuous monitoring with 500ms polling
  - Perfect for active development
  
- **`literal serverhost`** - Launch as HTTP server
  - `literal serverhost api.literal --port 3000`
  - Expose functions as HTTP endpoints
  - Built-in server hosting
  
- **`literal import`** - Module management
  - `literal import module_name` - Resolve and install
  - `literal import module --info` - Get package info
  - `literal import --list` - List available packages

#### Unified Interpreter (literal.exe)
- **Integrated Terminal**: literal.exe now doubles as a LiteralScript interpreter
  - Start interactive session: `literal` (no arguments)
  - Seamless command dispatch
  - Full REPL functionality built-in
- **Smart Mode Detection**:
  - Command execution when args provided
  - Interactive terminal when launched without args
  - Backward compatible with existing workflows

#### Enhanced Lexer
- Added module-related keywords: `import`, `module`, `export`, `namespace`, `include`
- Supports `import` as language-level keyword
- Case-insensitive parsing for all new keywords

#### Parser Extensions
- New AST nodes: `ImportStmt`, `ModuleStmt`
- Graceful import/module parsing
- Error recovery for malformed imports
- Support for import aliases and selective imports

#### Semantic Analyzer Updates
- IR support for `Import { module, alias, items }`
- IR support for `Module { name, body }`
- Symbol tracking for module-level definitions
- Namespace isolation support

#### Runtime Module Support
- Execute import statements
- Module body execution
- Namespace management
- Cross-module function calls

#### Code Generation for Modules
- Generates Rust `use` statements
- Creates `mod` blocks for module definitions
- Handles import aliases properly

### 📚 Documentation Updates

#### New Documents
- **[MODULE_SYSTEM.md](docs/MODULE_SYSTEM.md)** - Complete module guide
  - Import examples for all languages
  - Creating custom modules
  - Module file organization
  - Cross-language integration
  - Best practices

#### Updated Documents
- **[QUICK_START.md](docs/QUICK_START.md)** - v3.0 updates
  - New `do`, `run`, `build`, `watch` commands
  - Module import examples
  - Server hosting quick start
  - Updated command reference table
  
- **[CODING_TUTORIAL.md](docs/CODING_TUTORIAL.md)** - v3.0 edition
  - Module system section
  - Updated syntax table with import keyword
  - Module creation tutorial
  - Cross-language integration examples
  
- **[API_COMPLETE_REFERENCE.md](docs/API_COMPLETE_REFERENCE.md)** - v3.0 reference
  - New CLI commands documentation
  - Module system architecture
  - Import statement syntax
  - Module resolution order

### 🔧 Technical Improvements

#### Code Organization
- Created `src/module_resolver.rs` - Module resolution engine
- Integrated resolver into main CLI
- Clean separation of concerns

#### Build System
- All binaries compile without errors
- Only non-critical warnings (dead code, unused imports)
- Release binary: `target/release/literal.exe`

#### Performance
- Module caching for faster imports
- Efficient module resolution pipeline
- Minimal overhead for non-modular code

### 🐛 Breaking Changes

None - Full backward compatibility maintained

### ↪️ Migration Guide

**Existing Code**: Works as-is, no changes needed

**New Code**: Use new `do`/`run`/`build` commands for better DX

**Modules**: Opt-in feature - use only when needed

---

## [2.0.0] - March 27, 2026

### Initial Release with Ecosystem

- Complete compiler pipeline (Lexer → Parser → Semantic → Runtime/CodeGen)
- Tree-walking interpreter
- 6-language code generation (Rust, Python, JavaScript, C++, SQL, HTML)
- Ecosystem modules (Network, Database, GPU, Cloud, Desktop, API, WebGen)
- REPL support
- Package registry system
- Virtual terminal, filesystem, and database support

### Features
- English-based syntax for programming
- Continuous stream (semicolon-separated) statements
- Lowercase enforcement for keywords
- Support for variables, loops, conditionals, functions
- List and dictionary literals
- Map, filter, reduce operations
- Type inference
- Cross-language code generation

### Modules Included
- `lexer.rs` - Tokenization with English keywords
- `parser.rs` - Recursive descent parser
- `semantic_analyzer.rs` - AST to IR transformation
- `codegen.rs` - Code generation for 6 targets
- `runtime.rs` - Tree-walking interpreter
- `network.rs` - HTTP/TCP/WebSocket utilities
- `database.rs` - Multi-database abstraction
- `gpu.rs` - GPU acceleration (CUDA, Metal, OpenCL, Vulkan)
- `cloud.rs` - Cloud deployment (AWS, Azure, GCP)
- `desktop.rs` - Desktop UI (Qt, Tkinter, Electron, Win32)
- `api.rs` - REST/GraphQL/WebSocket/gRPC frameworks
- `packages.rs` - Dependency and package management
- `webgen.rs` - HTML/CSS/JS generation
- `filesystem.rs` - Virtual filesystem
- `terminal.rs` - Virtual terminal
- `repl.rs` - Interactive REPL (separate binary)

---

## Version Numbering

### Format: MAJOR.MINOR.PATCH

- **MAJOR**: Breaking changes or major features (modules, new paradigm)
- **MINOR**: New features, backward compatible (new commands)
- **PATCH**: Bug fixes, minor improvements (warnings, optimizations)

---

## Upgrade Path

### From 2.0 → 3.0
- Update documentation references in scripts
- Consider adopting new `do`/`run` syntax (optional)
- No code changes required for existing .literal files

---

## Known Limitations

### Current Version (3.0.0)
- Module definitions limited to single files (directory modules in development)
- No cyclic module dependencies
- Version pinning requires manual coordination
- Type system is inferred, no explicit type annotations yet
- REPL is integrated into main binary (previously separate)

### Future Roadmap
- [ ] Type annotations and static type checking
- [ ] Module versioning system
- [ ] Async/await support
- [ ] Advanced packaging (monorepos, workspaces)
- [ ] WASM compilation target
- [ ] LSP server for IDE integration
- [ ] Debugger support

---

## Contributors

- **Core Team**: LiteralScript Development Team
- **Contributors**: Community developers and testers

---

## How to Report Bugs

1. Check [GitHub Issues](https://github.com/YourOrg/LiteralScript/issues)
2. Create a new issue with:
   - LiteralScript version
   - Operating system
   - Minimal code example reproducing the bug
   - Expected vs actual behavior

---

## License

LiteralScript is released under the [MIT License](docs/LICENSE).

---

**Last Updated**: April 17, 2026  
**Current Version**: 3.0.0  
**Next Release**: 3.1.0 (Q3 2026)
