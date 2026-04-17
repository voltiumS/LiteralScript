# LiteralScript Module System & Import Guide

## Overview

LiteralScript now includes a complete **module system** that allows you to:

- **Import** modules and packages from any programming language ecosystem
- **Define** your own reusable modules  
- **Organize** code into namespaces and packages
- **Use** functions and data from Python (pip), Node.js (npm), Rust (cargo), and more
- **Cross-language** integration with seamless package bridging

---

## Quick Start: Using Modules

### Basic Import

```literal
import express
```

This imports the Express.js web framework and makes all its functions available.

### Import with Alias

```literal
import requests as req
```

Use an alias to avoid naming conflicts or improve readability.

### Import Specific Items

```literal
import numpy from array, linker, random
```

Import only the functions you need from a module.

### Multiple Imports

```literal
import flask
import sqlite
import requests as req
```

You can chain multiple imports together.

---

## New Command: `do` - Execute Files

Execute a LiteralScript file immediately:

```bash
literal do hello.literal
literal do app.literal
```

The `do` command runs your .literal file using the interpreter engine, perfect for scripts and quick testing.

---

## New Command: `build` - Compile/Interpret Files

Build a LiteralScript file with compilation or interpretation:

```bash
# Compile to Rust
literal build app.literal

# Interpret instead
literal build app.literal --interpret
```

---

## New Command: `run` - Alias for `do`

```bash
literal run app.literal
```

Shorthand for executing files. Works identically to `do`.

---

## New Command: `watch` - Auto-Rebuild Files

Monitor a file for changes and automatically rebuild when it changes:

```bash
literal watch app.literal
```

Perfect for development! Press Ctrl+C to stop watching.

---

## New Command: `serverhost` - Host as HTTP Server

Launch a LiteralScript file as an HTTP server:

```bash
literal serverhost api.literal --port 8080
```

This command:
- Loads your .literal file as an HTTP service
- Exposes functions as endpoints
- Listens on the specified port (default: 3000)
- Perfect for creating REST APIs

---

## Module Management Commands

### List Available Packages

```bash
literal import --list
```

Shows all known packages across ecosystems:
- npm packages (Node.js/JavaScript)
- pip packages (Python)
- cargo crates (Rust)
- nuget packages (.NET)
- maven packages (Java)
- gem packages (Ruby)
- go modules (Go)

### Get Package Information

```bash
literal import flask --info
```

Displays source information about a package:
```
[Module] flask is a Python/pip package
```

### Resolve and Install Module

```bash
literal import pandas
```

Automatically detects the package source and installs it:
```
[Module] Detected package source: Python/pip
[Module] Run: pip install pandas
```

---

## Defining Your Own Modules

### Basic Module Definition

```literal
module math_utils;
  
  record function add using x, y
    x into result
    y into result
  done function
  
  record function multiply using x, y
    x into result  
    y into result
  done function
  
done module
```

### Using Your Module

```literal
import math_utils

display add using 5, 3
display multiply using 4, 2
```

### Module with Exports

```literal
module data_tools;
  export clean_data
  export validate_input
  
  record function clean_data using values
    ...
  done function
  
done module
```

---

## Module File Structure

### Single File Module

**mymodule.literal** - Contains all module code:

```literal
module mymodule;
  record function helper using x
    ...
  done function
done module
```

Use: `import mymodule`

### Directory Module

Create a directory structure:

```
project/
├── modules/
│   ├── database/
│   │   └── index.literal
│   ├── api/
│   │   ├── handlers.literal
│   │   └── index.literal
│   └── utils/
│       └── index.literal
```

Each directory's `index.literal` is the entry point.

Use: `import database`, `import api`, etc.

---

## Cross-Language Package Integration

### Python Packages

```literal
import pandas
import numpy from array, reshape, statistics
import tensorflow as tf

display pandas version
```

### JavaScript/Node.js Packages

```literal
import express
import axios as http_client
import lodash from map, filter, reduce
```

### Rust Crates

```literal
import tokio
import serde
import sqlx
```

### .NET Packages (NuGet)

```literal
import newtonsoft
import entity-framework
```

### Java Packages (Maven)

```literal
import spring
import junit
```

### Ruby Gems

```literal
import rails
import sinatra
```

---

## Advanced Module Features

### Namespaced Imports

Avoid naming conflicts with namespaces:

```literal
import json_lib as json
import csv_lib as csv

record data into json_result
record csv_data into csv_result
```

### Conditional Imports

Import based on conditions:

```literal
when environment is "production" then
  import prod_database
otherwise
  import dev_database
```

### Module Dependencies

Modules can depend on other modules:

```literal
# lib/logger.literal
module logger;
  record function log using message
    Display message
  done function
done module

# lib/api.literal
module api;
  import logger
  
  record function handle_request using path
    log using "Processing: " 
    ...
  done function
done module
```

---

## Example: Building a Web API

**hello_api.literal**

```literal
import express as app
import cors

build interface app;
  
  record function welcome
    response create with "message": "Welcome to LiteralScript API"
  done function
  
  app.get "/" using welcome
  app.post "/data" using handle_data
  app.listen at 3000
  
done interface
```

Run: `literal serverhost hello_api.literal --port 3000`

---

## Module Resolution Order

When you import a module, LiteralScript searches in this order:

1. **Local .literal files** - `module_name.literal`
2. **Directory modules** - `./modules/module_name/index.literal`
3. **Package registries**:
   - npm (Node.js)
   - pip (Python)
   - cargo (Rust)
   - nuget (.NET)
   - gem (Ruby)
   - go modules (Go)
   - maven (Java)

---

## Troubleshooting Module Imports

### Module Not Found

```
[Error] Cannot resolve module: pandas
[Module] Run: pip install pandas
```

**Solution**: Install the package using the suggested command.

### Name Conflicts

Use aliases to avoid conflicts:

```literal
import json_lib as data_json
import custom_json as my_json
```

### Version Specification

Specify versions in your module definitions:

```literal
module requirements;
  import numpy@1.21.0
  import pandas@1.3.2
done module
```

---

## Module Caching

LiteralScript caches imported modules for performance. To clear cache:

```bash
literal cache clear
```

---

## Best Practices

✅ **DO:**
- Use descriptive module names
- Keep modules focused and single-purpose
- Document module functions and exports
- Use aliases for clarity
- Version your module dependencies

❌ **DON'T:**
- Create circular module dependencies
- Import modules you don't use
- Pollute the global namespace
- Mix module styles inconsistently

---

## Complete Example: Data Processing Pipeline

**data_pipeline.literal**

```literal
import pandas as pd
import numpy as np
from visualization import plot, chart

record filename into input_file
record "output.csv" into output_file

record pd.read_csv using input_file into data

when data is not empty then
  
  record data.describe using into stats
  
  display "Data Statistics:"
  display stats
  
  record data.apply using clean_values into cleaned
  record cleaned into final_data
  
  record final_data.to_csv using output_file
  
  chart using final_data from plotlib
  
  display "Processing complete!"
  
otherwise
  display "Error: No data found"
```

Run: `literal do data_pipeline.literal`

---

## What's Next?

- Explore the [QUICK_START.md](QUICK_START.md) for basic examples
- Read [CODING_TUTORIAL.md](CODING_TUTORIAL.md) for language features
- Check [API_COMPLETE_REFERENCE.md](API_COMPLETE_REFERENCE.md) for all functions
- Review [CHANGELOG.md](CHANGELOG.md) for version history

---

**LiteralScript v3.0** - English-Based Programming with True Module Power
