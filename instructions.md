# Clean VS Code Setup for Multiple Tutorial Folders (Each with Its Own `.venv`)

This repository is educational. Each folder is independent and contains its own `requirements.txt`.

To run any example, you must first create a local virtual environment using **uv** inside that specific folder.

---

# Step 1 — Create a uv Environment (Required First)

When you want to run a tutorial:

```bash
cd <tutorial-folder>
uv venv
uv pip install -r requirements.txt
```

### Example

```bash
cd agents/building-blocks
uv venv
uv pip install -r requirements.txt
```

This creates a local `.venv` inside that folder and installs only the dependencies required for that example.

Each tutorial folder is fully isolated.

---

# Step 2 — VS Code Configuration (Per Folder)

Each tutorial folder should contain:

```
tutorial-folder/
├── .venv/
├── .vscode/
│   └── settings.json
├── requirements.txt
└── your_code.py
```

Inside each tutorial folder, create:

```
.vscode/settings.json
```

If Finder blocks dot-folders, create it from Terminal:

```bash
mkdir .vscode
touch .vscode/settings.json
```

Then add:

```json
{
  "python.defaultInterpreterPath": "${workspaceFolder}/.venv/bin/python",
  "python.terminal.activateEnvironment": true
}
```

`${workspaceFolder}` automatically refers to that specific tutorial folder.

So every folder points to its own `.venv`.

---

# Step 3 — Use a Multi-Root Workspace (Recommended)

1. Open VS Code
2. File → Add Folder to Workspace…
3. Add each tutorial folder
4. File → Save Workspace As… at repo root

Now each folder keeps its own interpreter automatically.

---

# Important Rules

* Always run `uv venv` inside the tutorial folder first.
* Only add `.vscode/settings.json` to folders that have their own `.venv`.
* Do not put this configuration at the repo root unless you want a single global environment.

---

# Result

* Clean isolation per tutorial
* No interpreter confusion
* No import squiggles
* Scalable structure for many examples
