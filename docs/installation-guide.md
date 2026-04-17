# LiteralScript Installation Guide

**Version**: 2.0.0  
**Last Updated**: April 17, 2026  
**Platforms**: Windows, macOS, Linux

---

## Quick Start (Choose Your Platform)

### Windows Users

#### Option A: Automated Setup (Recommended)
```bash
setup.bat
```
This script will:
1. ✅ Verify Rust installation
2. ✅ Build release binaries
3. ✅ Offer portable, PATH, or MSI installation
4. ✅ Verify everything works

#### Option B: Manual Installation
```bash
# Build binaries
cargo build --release

# Add to PATH
setx PATH "C:\Users\%USERNAME%\LiteralScript\target\release;%PATH%"

# Test
literal --version
literal-repl
```

#### Option C: MSI Installer (Professional)
**Requirements**: WiX Toolset 3.x installed
```bash
build_msi.bat
# Then double-click LiteralScript-Setup.msi
```

[See WiX Setup section below]

---

### macOS Users

#### Option A: Automated Setup (Recommended)
```bash
python3 install_universal.py
# Select option 1: "From source"
```

#### Option B: Manual Installation
```bash
# Install Rust if needed
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env

# Clone and build
git clone https://github.com/voltiumS/LiteralScript.git
cd LiteralScript
./install.sh

# Verify
literal --version
literal-repl
```

#### Option C: Homebrew (Coming Soon)
```bash
brew tap voltiums/literalscript
brew install literalscript
```

---

### Linux Users

#### Option A: Automated Setup (Recommended)
```bash
python3 install_universal.py
# Select option 1: "From source"
```

#### Option B: Manual Installation (Ubuntu/Debian)
```bash
# Install Rust and build tools
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
sudo apt-get install build-essential

# Build and install
git clone https://github.com/voltiumS/LiteralScript.git
cd LiteralScript
./install.sh

# Verify
literal --version
literal-repl
```

#### Option C: Package Manager
```bash
# Snap (Ubuntu/Fedora/etc)
sudo snap install literalscript

# Or compile from AUR (Arch)
yay -S literalscript
```

---

## Installation Methods Explained

### Method 1: Portable Installation

**Best For**: Testing, USB drives, custom locations

**What It Does**:
- Copies binaries to a folder you choose
- No system modification
- Easy to move or delete

**Steps**:
```bash
setup.bat
# Select option 1 (Windows)
# Or manually:
mkdir C:\MyApps\LiteralScript
copy target\release\literal*.exe C:\MyApps\LiteralScript\
```

**To Run**:
```bash
C:\MyApps\LiteralScript\literal.exe --version
```

**To Add to PATH Later**:
```bash
setx PATH "C:\MyApps\LiteralScript;%PATH%"
```

---

### Method 2: System PATH Installation

**Best For**: Daily development, global access

**What It Does**:
- Installs to Program Files (Windows) or `/usr/local/bin` (Unix)
- Adds to system PATH
- Accessible from any directory
- Easy to uninstall

**Windows Steps**:
```bash
# Option A: Using setup.bat
setup.bat
# Select option 2

# Option B: Manual
mkdir "%ProgramFiles%\LiteralScript"
copy target\release\literal*.exe "%ProgramFiles%\LiteralScript\"
setx PATH "%ProgramFiles%\LiteralScript;%PATH%"
```

**Unix/Linux/macOS Steps**:
```bash
./install.sh
# Or manually:
sudo mkdir -p /usr/local/bin
sudo cp target/release/literal /usr/local/bin/
sudo cp target/release/literal-repl /usr/local/bin/
sudo chmod +x /usr/local/bin/literal*
```

**To Run**:
```bash
literal --version
literal-repl
```

---

### Method 3: Windows MSI Installer (Professional)

**Best For**: End-users, distribution, silent deployment

**What It Does**:
- Professional installer with GUI
- Automatic PATH integration
- File associations (.literal files)
- Start Menu shortcuts
- Automatic uninstall
- Silent install/uninstall capability

**Requirements**:
- Windows 7 SP1 or later
- 100 MB disk space
- Internet access (for WiX Toolset one-time)

**Setup Instructions**:

**Step 1: Install WiX Toolset** (One-time)
```
1. Go to: https://wixtoolset.org/releases/
2. Download "WiX v3.x" (e.g., wix314.exe)
3. Run the installer
4. Accept default installation
5. Restart your computer
```

**Step 2: Build MSI**
```bash
build_msi.bat
```

**Step 3: Test MSI**
```bash
# GUI Installation
LiteralScript-Setup.msi

# Or command-line
msiexec /i LiteralScript-Setup.msi
```

**MSI Features**:
- ✅ Installs to: `C:\Program Files\LiteralScript\`
- ✅ Adds both `literal.exe` and `literal-repl.exe` to PATH
- ✅ Creates Start Menu shortcuts
- ✅ Associates `.literal` files with default editor
- ✅ Includes example programs
- ✅ Supports silent installation
- ✅ Automatic uninstall support

**Silent Installation** (for IT deployment):
```bash
msiexec /i LiteralScript-Setup.msi /quiet /norestart
```

**Custom Installation Directory**:
```bash
msiexec /i LiteralScript-Setup.msi INSTALLDIR="C:\CustomPath\LiteralScript"
```

**Uninstall**:
```bash
# GUI Uninstall
msiexec /x LiteralScript-Setup.msi

# Silent Uninstall
msiexec /x LiteralScript-Setup.msi /quiet
```

---

## Cross-Platform Universal Installer

**Python-based installer** works on all platforms

### Usage

```bash
python3 install_universal.py
```

### Menu Options

```
1. From source (builds with cargo) - Recommended
2. From GitHub releases (pre-built binaries)
3. Windows MSI installer (if available)
4. Exit
```

### Features

- Detects your operating system
- Checks system requirements
- Installs to appropriate directory
- Verifies installation
- Color-coded output
- Progress indicators

### System Support

| OS | Method | Install Path |
|----|--------|--------------|
| Windows | Source Build or MSI | `Program Files\LiteralScript` |
| macOS | Source Build | `/usr/local/bin` |
| Linux | Source Build | `/usr/local/bin` |

---

## Verification

After installation, verify everything works:

### Test 1: Version Check
```bash
literal --version
# Output: LiteralScript v2.0 - Integrated Environment
```

### Test 2: REPL Launch
```bash
literal-repl
# Output: LiteralScript> 
```

### Test 3: Run Example
```bash
literal examples/hello.literal --run
# Output: Hello World!
```

### Test 4: Code Generation
```bash
literal examples/hello.literal
# Generates: hello.literal.rust, hello.literal.py, etc.
```

---

## Platform-Specific Notes

### Windows

**Antivirus Issues**:
- Some antivirus software may flag the .exe
- This is normal for unsigned executables
- Build from source if concerned

**PATH Not Updated**:
- If `literal` command not found after PATH installation
- Restart terminal/Command Prompt
- Or run: `refreshenv` (in Windows Terminal)

**Administrator Rights**:
- MSI installation typically requires admin
- `Program Files` directory is protected
- Use administrator account or UAC prompt

### macOS

**Code Signing**:
- Binary may show "unidentified developer" warning
- Go to: System Preferences → Security → Allow
- Or: `sudo xattr -d com.apple.quarantine /usr/local/bin/literal*`

**Homebrew Alternative** (Coming Soon):
```bash
brew tap voltiums/literalscript
brew install literalscript
```

### Linux

**Permissions**:
- `/usr/local/bin` requires sudo
- Or install to `~/.local/bin` (user directory)
- Update `.bashrc`: `export PATH="$HOME/.local/bin:$PATH"`

**Library Dependencies**:
- Most modern Linux distributions have required libraries
- If missing: `sudo apt install libssl-dev` (Debian/Ubuntu)

---

## Troubleshooting

### Problem: "Rust not found"

**Solution**:
```bash
# Install Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Reload PATH
source $HOME/.cargo/env  # macOS/Linux
# Or restart terminal (Windows)
```

### Problem: "candle: command not found" (MSI Build)

**Solution**:
1. Download WiX from https://wixtoolset.org/
2. Install using installer (not portable ZIP)
3. Restart computer
4. Try again

### Problem: "Permission denied" (Linux/macOS)

**Solution**:
```bash
sudo chmod +x /usr/local/bin/literal*
sudo chmod +x /usr/local/bin/literal-repl
```

### Problem: Build Fails with Compilation Errors

**Solution**:
```bash
# Update Rust
rustup update

# Clean and rebuild
cargo clean
cargo build --release
```

### Problem: "Cannot find literal" after Installation

**Solution**:
```bash
# Verify installation
where literal  # Windows
which literal  # macOS/Linux

# Add to PATH manually
setx PATH "C:\Program Files\LiteralScript;%PATH%"  # Windows
export PATH="/usr/local/bin:$PATH"  # macOS/Linux
```

---

## Uninstallation

### Windows (Portable)
```bash
# Just delete the folder
rmdir /s C:\LiteralScript
```

### Windows (PATH)
```bash
# Delete files
del "%ProgramFiles%\LiteralScript\*.*"
rmdir "%ProgramFiles%\LiteralScript"

# Remove from PATH (open Command Prompt as admin)
setx PATH "NewPathValue"  # Edit as needed
```

### Windows (MSI)
```bash
# Use Control Panel
Start → Settings → Apps → Apps & Features → LiteralScript → Uninstall

# Or command line
msiexec /x LiteralScript-Setup.msi
```

### macOS/Linux
```bash
# Delete binaries
sudo rm /usr/local/bin/literal*

# Remove from PATH (if in ~/.bashrc)
nano ~/.bashrc
# Remove the export PATH line
```

---

## Build from Source

### Requirements
- Rust 1.70+
- Cargo (comes with Rust)
- Git
- ~1 GB free disk space

### Build Steps

```bash
# 1. Clone repository
git clone https://github.com/voltiumS/LiteralScript.git
cd LiteralScript

# 2. Build (debug)
cargo build

# 3. Build (optimized release)
cargo build --release

# 4. Test
cargo test --release

# 5. Install
cargo install --path .
```

### Build Variants

```bash
# Debug build (fast compile, slow run)
cargo build
# Output: target/debug/literal

# Release build (slow compile, fast run)
cargo build --release
# Output: target/release/literal

# Release with profiling
RUSTFLAGS="-g" cargo build --release

# Minimal size
cargo build --release -Z build-std=std,panic_abort --target x86_64-pc-windows-msvc
```

---

## Next Steps

After installation, see:
- **Quick Start**: `QUICK_START.md`
- **Full Documentation**: `README.md`
- **API Reference**: `API_COMPLETE_REFERENCE.md`
- **Contributing**: `CONTRIBUTING.md`

---

## System Requirements

### Minimum
- **OS**: Windows 7 SP1, macOS 10.13, Linux (Ubuntu 18.04+)
- **RAM**: 512 MB
- **Disk**: 200 MB (binaries + examples)
- **Internet**: For downloading WiX (Windows MSI only)

### Recommended
- **OS**: Windows 10+, macOS 11+, Linux (Ubuntu 22.04+)
- **RAM**: 2 GB
- **Disk**: 1 GB (source + build artifacts)
- **Internet**: For GitHub releases

### Build Requirements (if building from source)
- **Rust**: 1.70+
- **Cargo**: Latest
- **C/C++ Compiler**: MSVC (Windows), Clang/GCC (Unix)

---

## Support

- **GitHub Issues**: https://github.com/voltiumS/LiteralScript/issues
- **Documentation**: README.md, QUICK_START.md
- **API Guide**: API_COMPLETE_REFERENCE.md

---

**LiteralScript v2.0.0** - Transform English into Code  
Licensed under MIT

