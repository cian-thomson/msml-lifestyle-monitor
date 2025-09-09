# Contributing to MSML-Lifestyle-Monitor

To ensure a smooth and collaborative workflow, please follow these guidelines.

---

## How to Contribute

### 1. Fork the Repository

Clone your forked repository to work on your changes independently.

### 2. Create a Feature Branch

Create a new branch off the `main` (or `develop`) branch for your feature or bugfix. Use descriptive branch names prefixed with `feature/` or `bugfix/`.
Example:
```bash
git checkout -b feature/image-acquisition
```

### 3. Make Your Changes

- Follow the coding standards and style used in the project.
- Write clear, concise commit messages.
- Test your changes locally before submitting.

### 4. Push Your Branch to Your Fork

```bash
git push origin feature/your-branch-name
```

### 5. Squash Your Commits
Before opening a pull request, squash your commits into a single logical commit. 
To do this, use `git rebase -i` to interactively rebase and combine multiple commits. 
This keeps your commit history clean and organized.

```bash
git rebase -i main
```

Keep:
- One commit per feature or bugfix (where reasonable).
- Descriptive commit messages that follow the guidelines below.

### 5. Open a Pull Request (PR)

- Submit a PR from your feature branch to the main repository’s main branch.
- Describe your changes clearly in the PR description.
- Link any relevant issues or discussion.

## Commit message guidelines

To keep the project history clear and informative, please format your commit messages as follows:

- Start the commit message with a concise summary of the change.
- Optionally include a tag or label in square brackets to indicate the context, such as the branch name, feature, or type of change.
Example:
```
[feature/image-acquisition] Add camera interface and image capture module

Implemented the hardware interface for the camera sensor and added functions to capture and store images. This is the first step towards integrating the image acquisition pipeline.

- Initialised camera communication protocols
- Added image buffer management
- Included basic error handling for sensor read failures
```

### 6. Working with the FPGA Submodule (Optional)
The FPGA module is included as a submodule within this repository. This allows FPGA-related development to be tracked alongside the main project without forcing all contributors to download hardware code or datasets.

- Fork the main repository
When you clone the main repository, the FPGA submodule is not automatically initialized. You need to manually initialize and update the submodule to work with FPGA-related code.

```bash
git clone https://github.com/your-username/msml-lifestyle-monitor.git
cd fpga-msml-lifestyle-monitor
```

Initializing or updating the FPGA submodule (only if needed)
To fetch and work on the FPGA module:

```bash
git submodule update --init --recursive fpga
```

To update the submodule to the latest commit from its remote:

```bash
git submodule update --remote fpga
```

Notes for contributors:
- Software/ML contributors can ignore the FPGA folder; no large datasets or hardware files are required.
- FPGA contributors should initialize the submodule and commit any changes within the fpga/ folder.
- Pulling updates in the main repo does not automatically update the FPGA submodule, preventing unnecessary downloads


## Working with Submodules (e.g., FPGA)

This project uses Git submodules for independent components such as FPGA designs.
Submodules are separate repositories linked into the main repo, and they must be updated in two steps.

### 1. Contribute to the Submodule Repo

- Clone and work on the FPGA (or other) submodule directly.
- Create a feature branch and make your changes.
- Squash commits before opening a PR.
- Open a PR in the submodule repository, get it reviewed, and merge.

### 2. Update the Submodule in the Main Repo

Once the submodule PR is merged, you'll need to update the submodule reference in the main repo. This ensures that your main repo is always pointing to the latest commit in the submodule, but remember: do not directly modify submodule files in the main repository. You should only update the reference to the latest commit from the submodule

```bash
cd submodules/fpga
git checkout main
git pull origin main
cd ../..
git add submodules/fpga
git commit -m "[submodule/fpga] Update to latest main"
git push origin feature/update-fpga-submodule
```

- Open a PR in the main repository to update the submodule pointer.
- This PR should only update the submodule reference, not modify the submodule’s code directly

## Examples of commit and respective messages

1. The subject line should be short and concise—ideally under 50 characters—so it’s easily readable in logs or GitHub UI.
2. It’s also helpful to include an optional format like:
    [type/feature] for features or additions
    [type/bugfix] for fixes
    [submodule] for submodule-related commits

```bash
git add src/camera.c
git commit -m "[feature/image-acquisition] Add camera interface" -m "
Implemented the hardware interface for the camera sensor.

- Initialised I2C communication for camera module
- Added image buffer handling
- Basic error handling for sensor read failures

Fixes #45
"
```

```bash
git add src/decoder.vhdl
git commit -m "[bugfix/fpga-decoder] Fix timing issue in decoder" -m "
Adjusted clock domain crossing in FPGA decoder to avoid metastability.

- Added synchronizer flops for control signals
- Updated constraints file to align with synthesis tool

Fixes #78
"
```

```bash
git add submodules/fpga
git commit -m "[submodule/fpga] Update to latest main" -m "
Pulled in the latest commit from FPGA submodule, which includes:

- Timing fixes for UART module
- New testbench for simulation
"
```

## Information regarding Pull Reqests

To maintain code quality and consistency:

- All changes must be submitted via PR; direct pushes to main are not allowed.
- Commits must be squashed and rebased before PR submission.
- At least one approving review is required before merging.
- PR approvals are dismissed if new commits are pushed — ensure the latest changes are reviewed.
- All review comments and requested changes must be resolved before merging.
- The PR must have a clean, linear commit history (rebase or squash as needed).
- Tests and checks (if applicable) must pass before merging.
- Use “Squash and Merge” or “Rebase and Merge” when merging
- Whenever the term "Clone" is used it is assumed you are cloning your own fork.