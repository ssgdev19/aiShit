# Python, `venv`, and `uv` Explained Using a Calculator App 🧮

Imagine you are building a calculator software.

---

# Step 1: Global Python

First, you install Python on your computer.

Example:

```text id="gbvygo"
Python 3.12
```

This becomes your **main system Python**.

You can use it anywhere:

```bash id="5fpz5t"
python --version
```

Output:

```text id="g74kqy"
Python 3.12
```

Think of this as:

> The main electricity supply of your house ⚡

Everything can use it unless separated.

---

# Problem Without Isolation

You create a calculator app:

```text id="t07k1v"
calculator-app/
```

It needs:

```text id="dzugz3"
numpy==1.26
```

Later you create another project:

```text id="ifq0j5"
ai-project/
```

It needs:

```text id="z9djqk"
numpy==2.0
```

If both use the same global Python:

```text id="z1ivgu"
Global Python
    └── One shared package space
```

then:

* projects can overwrite each other's packages
* updates can break older apps
* dependency conflicts happen

Tiny civil war inside your laptop 🏰⚔️

---

# Step 2: `venv` Enters

`venv` creates an isolated environment for one project.

---

# Calculator App with `venv`

## Create project

```bash id="mx5j08"
mkdir calculator-app
cd calculator-app
```

---

## Create isolated environment

```bash id="l8shj0"
python -m venv .venv
```

Now structure becomes:

```text id="tr85h7"
calculator-app/
│
├── .venv/
```

Inside `.venv`:

* isolated Python executable
* isolated pip
* isolated packages

---

## Activate environment

Linux/macOS:

```bash id="1vl5mo"
source .venv/bin/activate
```

Windows:

```powershell id="l9x93d"
.venv\Scripts\activate
```

Now terminal becomes:

```text id="5saj9x"
(.venv) $
```

Meaning:

> “You are now inside calculator-app’s private Python world.”

---

## Install packages

```bash id="1mj0tw"
pip install numpy
```

Now:

```text id="jndjgi"
calculator-app/.venv/
    └── numpy
```

NOT globally installed.

---

# Important Understanding

`venv` usually uses the SAME Python version as global Python.

If global Python is:

```text id="wn3d7j"
Python 3.12
```

then `.venv` also uses:

```text id="i0q7qe"
Python 3.12
```

but with isolated packages.

---

# Step 3: `uv` Enters 🚀

`uv` modernizes the whole workflow.

Instead of separately using:

* Python
* venv
* pip

`uv` manages everything together.

Think of it as:

> A smart factory manager for Python projects 🏭

---

# Calculator App with `uv`

## Install uv

From [Astral](https://astral.sh?utm_source=chatgpt.com)

Linux/macOS:

```bash id="z1lmhh"
curl -LsSf https://astral.sh/uv/install.sh | sh
```

---

# Create calculator project

```bash id="ph6rrr"
mkdir calculator-app
cd calculator-app
```

---

# Create isolated environment

```bash id="k9v1nd"
uv venv
```

This creates:

```text id="lysdig"
calculator-app/.venv/
```

Same idea as normal `venv`.

---

# Install package

```bash id="0miyow"
uv add numpy
```

Faster and cleaner than pip.

---

# Biggest Superpower of `uv`

`uv` can also install DIFFERENT Python versions.

Example:

```bash id="2hq6vz"
uv python install 3.11
```

Now your machine has:

```text id="2w90vz"
Global Python 3.12
Python 3.11
```

both installed side-by-side.

---

# Create calculator app using Python 3.11

```bash id="57h4yu"
uv venv --python 3.11
```

Now:

```text id="0psmkx"
calculator-app/.venv/
    ├── Python 3.11
    └── numpy
```

while globally your machine still uses:

```text id="73nn4m"
Python 3.12
```

---

# Final Mental Model

```text id="j0c3q2"
SYSTEM
│
├── Global Python 3.12
│
├── calculator-app/
│     └── .venv/
│           ├── Python 3.11
│           └── numpy 1.26
│
└── ai-project/
      └── .venv/
            ├── Python 3.13
            └── torch
```

Each project becomes:

* isolated
* safe
* reproducible
* independent

Like tiny planets orbiting the same computer 🌍🪐🌎

---

# Command Summary

## Traditional (`venv` + `pip`)

### Create environment

```bash id="k31g5h"
python -m venv .venv
```

### Activate

Linux/macOS:

```bash id="9w13of"
source .venv/bin/activate
```

Windows:

```powershell id="vsn7r4"
.venv\Scripts\activate
```

### Install package

```bash id="bl5im8"
pip install numpy
```

---

# Modern (`uv`)

### Install Python version

```bash id="a7n8kt"
uv python install 3.11
```

### Create environment

```bash id="i9mhn9"
uv venv --python 3.11
```

### Install package

```bash id="wt5cf7"
uv add numpy
```

### Run project

```bash id="ypk3na"
uv run main.py
```

---

# One-Line Definitions

| Tool          | Meaning                                                            |
| ------------- | ------------------------------------------------------------------ |
| Global Python | Main Python installed on system                                    |
| `venv`        | Creates isolated environments                                      |
| `pip`         | Installs packages                                                  |
| `uv`          | Modern fast tool that manages Python, venvs, and packages together |
