# 🎮 Game Project Organizer & Go Compiler

A Python-based automation tool that discovers game projects inside a source directory, organizes them into a target directory, compiles their Go source code, and generates a JSON metadata file containing information about the processed games.

This project demonstrates **Python file-system automation, directory management, subprocess execution, JSON handling, and Go compilation**.

---

## 📌 Features

* 🔍 Automatically searches for directories containing `game` in their name
* 📁 Copies game projects from a source directory to a target directory
* 🔄 Overwrites existing game directories in the target location
* 🏷️ Automatically removes `_game` from directory names
* ⚙️ Detects and compiles `.go` source files
* 🛠️ Uses the Go compiler through Python's `subprocess` module
* 📄 Generates a `metadata.json` file
* 📊 Stores the game names and total number of games processed
* 💻 Works through command-line arguments

---

## 🧰 Technologies Used

* **Python 3**
* **Go**
* `os`
* `json`
* `shutil`
* `subprocess`
* `sys`

---

## 📂 Project Structure

The script expects a source directory containing game directories.

### Example input

```text
source/
├── snake_game/
│   └── main.go
├── pong_game/
│   └── main.go
├── tetris_game/
│   └── main.go
└── README.txt
```

After running the script, the target directory will look something like:

```text
target/
├── snake/
│   ├── main.go
│   └── main
├── pong/
│   ├── main.go
│   └── main
├── tetris/
│   ├── main.go
│   └── main
└── metadata.json
```

The `_game` suffix is removed from the copied directory names.

---

## ⚙️ How It Works

The program follows several steps.

### 1. Find Game Directories

The script searches the source directory for folders containing the word:

```text
game
```

For example:

```text
snake_game
pong_game
space_game
```

These directories are selected for processing.

---

### 2. Rename Game Directories

The `_game` portion of the directory name is removed.

For example:

```text
snake_game → snake
pong_game → pong
```

This creates cleaner directory names in the target folder.

---

### 3. Create the Target Directory

If the target directory does not already exist, the program creates it automatically.

```python
create_dir(target_path)
```

---

### 4. Copy Game Projects

Each discovered game directory is copied to the target directory.

If the destination already exists, it is deleted first and then replaced with a fresh copy.

```python
copy_and_overwrite(src, dest_path)
```

This ensures that the target contains an updated version of each game project.

---

### 5. Compile Go Code

The program searches each copied game directory for a `.go` file.

Once found, it runs:

```text
go build <filename>
```

The compilation is executed using Python's `subprocess` module.

```python
GAME_COMPILE_COMMAND = ["go", "build"]
```

---

### 6. Generate Metadata

After processing the games, the script creates:

```text
metadata.json
```

Example:

```json
{
    "gameNames": [
        "snake",
        "pong",
        "tetris"
    ],
    "numberOfGames": 3
}
```

This provides a simple summary of the games processed by the program.

---

# 🚀 Installation

## Prerequisites

Make sure you have the following installed:

### Python

Python 3 is required to run the automation script.

Check your installation:

```bash
python --version
```

or:

```bash
python3 --version
```

### Go

Go is required because the script compiles `.go` files.

Check your installation:

```bash
go version
```

---

# ▶️ Usage

Run the Python script from the command line using:

```bash
python script.py <source_directory> <target_directory>
```

For example:

```bash
python main.py games compiled_games
```

Where:

* `games` = directory containing the game projects
* `compiled_games` = directory where the processed projects will be placed

---

## 💡 Example

Suppose you have:

```text
project/
├── main.py
└── games/
    ├── snake_game/
    │   └── main.go
    ├── pong_game/
    │   └── main.go
    └── racing_game/
        └── main.go
```

Run:

```bash
python main.py games compiled_games
```

The program will:

1. Find `snake_game`
2. Find `pong_game`
3. Find `racing_game`
4. Remove `_game` from their names
5. Copy them into `compiled_games`
6. Compile the Go source files
7. Generate `metadata.json`

Result:

```text
compiled_games/
├── snake/
├── pong/
├── racing/
└── metadata.json
```

---

# 🧠 Code Overview

The project is divided into several functions.

| Function                    | Purpose                              |
| --------------------------- | ------------------------------------ |
| `find_all_game_paths()`     | Finds game directories               |
| `get_name_from_paths()`     | Removes `_game` from directory names |
| `create_dir()`              | Creates the target directory         |
| `copy_and_overwrite()`      | Copies game directories              |
| `make_json_metadata_file()` | Creates the metadata JSON file       |
| `compile_game_code()`       | Finds and compiles Go files          |
| `run_command()`             | Executes shell commands              |
| `main()`                    | Controls the overall workflow        |

---

# 🔧 Configuration

The script uses constants to define how it identifies and builds game projects.

```python
GAME_DIR_PATTERN = "game"
GAME_CODE_EXTENSION = ".go"
GAME_COMPILE_COMMAND = ["go", "build"]
```

### `GAME_DIR_PATTERN`

Determines what the script searches for when identifying game directories.

Default:

```python
"game"
```

### `GAME_CODE_EXTENSION`

Defines the source-code extension that the compiler searches for.

Default:

```python
".go"
```

### `GAME_COMPILE_COMMAND`

Defines the command used to compile the Go source code.

Default:

```python
["go", "build"]
```

---

# ⚠️ Important Notes

* The script expects the Go compiler (`go`) to be available in your system's PATH.
* Game directories are identified based on whether their name contains `game`.
* The current implementation searches only the immediate subdirectories of the source directory.
* Existing destination game directories are deleted before being copied again.
* The script currently compiles the first `.go` file it finds in each game directory.
* Go projects with multiple source files or more complex build configurations may require modifications to the compilation logic.

---

# 🎯 Learning Objectives

This project is useful for learning how Python can automate development workflows.

It demonstrates:

* File and directory traversal
* File-system automation
* Directory creation and deletion
* Copying files and directories
* JSON file generation
* Command-line arguments
* Running external programs from Python
* Automating compilation workflows
* Integrating Python with Go development

---

# 📜 License

This project is available for educational and personal use. Add a specific license such as the **MIT License** if you want others to freely use, modify, and distribute the project.

---

# 👨‍💻 Author

**Aryajeet Jadhav**

Built as a Python automation project for managing and compiling Go-based game projects.

