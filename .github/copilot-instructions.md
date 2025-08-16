# Copilot instructions for this repository

These instructions make AI coding agents productive in this codebase. Follow the repo’s conventions and the user’s environment strictly.

## Environment and shell (Windows + PowerShell 7 + venv)
- All terminal commands must target PowerShell 7.
- Always create and use the local venv before running Python to avoid missing packages.

```powershell
# Create and activate venv (Windows, PowerShell 7)
python -m venv venv
.\venv\Scripts\Activate.ps1
# Install baseline dependencies for this repo
pip install --upgrade pip
pip install -r requirements_py3.txt
```

Notes:
- Many sections import extra libs not in requirements_py3.txt (e.g., scikit-learn, hiddenlayer). If ImportError occurs, install into the venv:
```powershell
pip install scikit-learn hiddenlayer
```
- Some examples use graphviz; if you hit runtime errors after `pip install graphviz`, you may also need the Graphviz system package installed and on PATH.

## Big picture
- This is a course-style repo with many self-contained examples organized by section folders (e.g., `030_ModelingIntroduction/`, `045_Classification/`, …).
- Each topic typically has paired files with suffixes `*_start.py/.ipynb` and `*_end.py` showing before/after solutions.
- There is no central package, build, or test harness; you run individual scripts or notebooks per section.

## Common patterns across sections
- PyTorch model structure: define an `nn.Module`, a loss (often `nn.MSELoss()`), and an optimizer (often `torch.optim.SGD`).
  - Example: `030_ModelingIntroduction/20_LinReg_Batches_start.py` and `30_LinReg_DatasetDataloader_start.py`.
- Training loops track `losses`, sometimes `slope` and `bias` from `model.named_parameters()`.
- Data comes from small CSVs (local or remote, e.g., cars dataset via a gist). Expect code to do simple Pandas/Numpy to Torch conversions.
- Model save/load is demonstrated via `torch.save(model.state_dict(), 'model_state_dict.pth')` and `model.load_state_dict(torch.load(...))` (see `030_ModelingIntroduction/40_LinReg_ModelSavingLoading_end.py`).
- Scripts often use Spyder/VS Code cell markers `#%%` for interactive execution.

## How to run examples
- Notebooks: open `.ipynb` in VS Code, select the venv kernel, then run cells.
- Scripts: run from the repo root or cd into the section folder to keep relative paths working.

```powershell
# Activate venv for the session
.\venv\Scripts\Activate.ps1

# Run a script (example: save/load state dict demo)
python .\030_ModelingIntroduction\40_LinReg_ModelSavingLoading_end.py

# Run a numpy-only scratch example
python .\015_NeuralNetworkFromScratch\nn_scratch_start.py
```

## Data and files
- Some data is bundled (e.g., `015_NeuralNetworkFromScratch/heart.csv`); others are fetched from the web (requires internet).
- Saved artifacts (e.g., `model_state_dict.pth`) are written into the current working directory; run from the same folder (or adjust paths) to avoid NotFound/Permission issues.

## Dependencies to know
- Baseline: see `requirements_py3.txt` (torch, torchvision, ipykernel, seaborn, requests, psutil, kaleido, graphviz, torchmetrics).
- Frequently used but not always pre-pinned: scikit-learn (used in `nn_scratch_start.py`), hiddenlayer (occasionally imported for graph viz). Install on demand in the venv.

## Conventions you should mirror
- Keep code examples minimal and self-contained inside each section folder.
- Prefer CPU for portability (README’s conda flow uses cpuonly). If offering CUDA usage, guard with `torch.cuda.is_available()` and keep it optional.
- Use clear variable names seen across the repo: `X`, `y_true`, `NUM_EPOCHS`, `BATCH_SIZE`, `losses`.
- Use Seaborn when visualizing training/metrics, consistent with the examples.

## Workflow guidance for agents
- Explanations must be in Markdown; tag code with the correct language fences (powershell, python).
- When proposing commands, always activate the venv in the same snippet before running Python.
- Don’t ask to “continue to iterate”; complete tasks end-to-end within the instructions you have.
- Respect the section structure; don’t introduce a monorepo build or test framework.

## Key reference files
- `README.md`: environment setup (also lists conda as an alternative).
- `requirements_py3.txt`: Python dependencies used across many sections.
- Example patterns: `030_ModelingIntroduction/20_*`, `30_*`, `40_*` and `015_NeuralNetworkFromScratch/nn_scratch_start.py`.
