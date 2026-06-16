# Learning how to use uv

## 1. Create a new project

There are two common ways to create a project with uv.

### Case 1: Create a new project folder

```bash
uv init <project_name>
```

Example:

```bash
uv init new_app
```

### Case 2: Initialize uv inside an existing project directory

```bash
uv init
```

You can also explicitly define the project type:

```bash
uv init <project_name> --<project_type>
```

For example:

```bash
uv init my_library --lib
```

This tells uv what type of project you are creating.

---

## 2. Understand the project files

After creating the project, uv creates a file called:

```text
pyproject.toml
```

This file contains information about the project, including its dependencies.

Another important file is:

```text
uv.lock
```

The **uv.lock** file stores more detailed information about the exact dependency versions used in the project.

To see the dependency tree, use:

```bash
uv tree
```

---

## 3. Add dependencies

To add one or more libraries to the project, use:

```bash
uv add <library_name>
```

Example:

```bash
uv add numpy
```

You can also add multiple libraries at the same time:

```bash
uv add <library_1> <library_2>
```

Example:

```bash
uv add numpy pandas
```

If you already have a requirements file, you can add dependencies from it:

```bash
uv add -r <requirements_file_name>
```

Example:

```bash
uv add -r requirements.txt
```

---

## 4. Virtual environment behavior

With uv, you usually do not need to create the `.venv` directory manually.

When you run:

```bash
uv add <library_name>
```

uv automatically creates the virtual environment if it does not already exist.

The virtual environment is usually created here:

```text
.venv
```

---

## 5. Activate and deactivate the virtual environment

### macOS/Linux

```bash
source .venv/bin/activate
```

### Windows PowerShell

```powershell
.venv\Scripts\Activate.ps1
```

### Windows CMD

```cmd
.venv\Scripts\activate.bat
```

To deactivate the virtual environment:

```bash
deactivate
```

---

## 6. Run Python files with uv

To run a Python file inside the virtual environment, use:

```bash
uv run <file_name.py>
```

Example:

```bash
uv run main.py
```

Even if you delete the `.venv` directory, you can still run:

```bash
uv run <file_name.py>
```

uv will recreate the virtual environment automatically and then run the file.

Cool!

---

## 7. Use `uv sync`

`uv sync` installs the exact dependencies from:

```text
uv.lock
```

into:

```text
.venv
```

This is especially useful after cloning a project from GitHub.

Typical workflow:

```bash
git clone <repo_url>
cd <repo_name>
uv sync
uv run <file_name.py>
```

So, when you clone a repo, you can use `uv sync` to install the dependencies and then run the code inside the virtual environment.

---

## 8. Remove dependencies

To uninstall a dependency from the project, use:

```bash
uv remove <dependency_name>
```

Example:

```bash
uv remove numpy
```

---

## 9. Install global tools

Some Python packages provide command-line executables that you may want to use globally.

For these, use:

```bash
uv tool install <tool_name>
```

Example:

```bash
uv tool install ruff
```

This installs the tool globally, not just inside the project virtual environment.

---

## 10. Uninstall global tools

To uninstall a globally installed tool, use:

```bash
uv tool uninstall <tool_name>
```

Example:

```bash
uv tool uninstall ruff
```

---

## 11. Upgrade tools

To upgrade one tool, use:

```bash
uv tool upgrade <tool_name>
```

Example:

```bash
uv tool upgrade ruff
```

To upgrade all installed tools, use:

```bash
uv tool upgrade --all
```

---

## 12. Run tools temporarily

Sometimes you want to use a tool temporarily without installing it.

You can use:

```bash
uv tool run <tool_name> <command_of_that_tool>
```

The shorter version is:

```bash
uvx <tool_name> <command_of_that_tool>
```

Example:

```bash
uvx ruff check .
```

This runs the tool temporarily without permanently installing it.
