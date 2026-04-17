# Contributing to LiteralScript

Thank you for your interest in contributing to LiteralScript! We welcome contributions from the community.

## Getting Started

### Prerequisites
- Rust 1.70 or later
- Git
- Cargo package manager

### Build from Source
```bash
git clone https://github.com/voltiumS/LiteralScript.git
cd LiteralScript
cargo build --release
```

### Run Tests
```bash
cargo test --release
./target/release/literal examples/hello.literal --run
```

## Areas for Contribution

### High Priority
- [ ] Additional language targets (Go, Kotlin, Java, C#)
- [ ] IDE integrations (VS Code extension, JetBrains plugin)
- [ ] Web-based playground
- [ ] Package extension system
- [ ] Performance optimizations

### Medium Priority  
- [ ] Additional database backends (DynamoDB, Cassandra, CouchDB)
- [ ] More cloud provider support (DigitalOcean, Heroku, Render)
- [ ] Enhanced error messages and debugging
- [ ] Visual AST/IR inspector
- [ ] WASM compilation target

### Documentation
- [ ] Language tutorial improvements
- [ ] Video tutorials
- [ ] Blog posts about use cases
- [ ] Architecture deep-dives
- [ ] API documentation

## Code Style

- Follow Rust conventions (rustfmt auto-formats code)
- Write comments for non-obvious logic
- Keep functions focused and small
- Add tests for new features
- Update README if adding major features

## Submitting Changes

1. **Fork** the repository
2. **Create a feature branch**: `git checkout -b feature/your-feature`
3. **Commit changes**: `git commit -am 'Add description of changes'`
4. **Push to branch**: `git push origin feature/your-feature`
5. **Submit pull request** with clear description

## Pull Request Guidelines

- Keep PRs focused on single features/fixes
- Write descriptive commit messages
- Include relevant issue numbers
- Update documentation if needed
- Ensure all tests pass: `cargo test --release`
- Run `cargo clippy` to catch common issues

## Reporting Bugs

Please report bugs via GitHub Issues with:
- Clear title and description
- Steps to reproduce
- Expected vs actual behavior
- LiteralScript version
- Operating system

## Feature Requests

Submit feature requests on GitHub with:
- Use case description
- Example code showing desired syntax
- Implementation complexity estimate
- Potential impact on existing code

## License

All contributions must be compatible with the MIT license.

## Questions?

Open an issue or discussion on GitHub for questions about the contribution process.

---

**Thank you for contributing to LiteralScript!**
