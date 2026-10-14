# DevOps Assignment 6: Jenkins Integration with GitHub

## What this project does

This is a small demo project used to show how Jenkins can automatically
pull source code from a GitHub repository and run a build/test pipeline
against it.

Files:
- `index.html` — a simple styled web page ("Hello from DevOps Demo").
- `app.py` — a Python script that prints a greeting and the current time.
- `Jenkinsfile` — a declarative Jenkins pipeline with three stages:
  `Checkout`, `Build`, and `Test`.

## What the pipeline does

1. **Checkout** — Jenkins clones this repository's `main` branch from
   GitHub into the Jenkins workspace.
2. **Build** — runs `python3 app.py` to simulate a build step and confirm
   the script runs correctly.
3. **Test** — runs `python3 -m py_compile app.py`, a basic sanity check
   that the Python file compiles without syntax errors.
4. **Post actions** — prints a success message if all stages pass, or a
   failure message if any stage fails.

## How to run it

### Option A: Freestyle Jenkins job
1. Create a Freestyle project in Jenkins.
2. Point its Source Code Management at this repo's GitHub URL, branch
   `main`.
3. Add an "Execute shell" build step: `ls && python3 app.py`.
4. Click "Build Now" and check the Console Output.

### Option B: Pipeline job (recommended)
1. Create a Pipeline project in Jenkins.
2. Set its definition to "Pipeline script from SCM", pointing at this
   repo and the `Jenkinsfile` at the repo root.
3. Click "Build Now" — Jenkins will check out the code and run the
   Checkout, Build, and Test stages automatically.

## Requirements

- Jenkins (with the Git, GitHub, and Pipeline plugins installed)
- Git
- Python 3
