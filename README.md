# BGP Hijacking

<a target="_blank" href="https://cookiecutter-data-science.drivendata.org/">
    <img src="https://img.shields.io/badge/CCDS-Project%20template-328F97?logo=cookiecutter" />
</a>

BGP Hijacking detection

## Project Organization

```
├── LICENSE            <- Open-source license if one is chosen
├── Makefile           <- Makefile with convenience commands like `make data` or `make train`
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default mkdocs project; see www.mkdocs.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── pyproject.toml     <- Project configuration file with package metadata for 
│                         bgp_hijacking and configuration for tools like black
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
├── setup.cfg          <- Configuration file for flake8
│
└── bgp_hijacking   <- Source code for use in this project.
    │
    ├── __init__.py             <- Makes bgp_hijacking a Python module
    │
    ├── config.py               <- Store useful variables and configuration
    │
    ├── dataset.py              <- Scripts to download or generate data
    │
    ├── features.py             <- Code to create features for modeling
    │
    ├── modeling                
    │   ├── __init__.py 
    │   ├── predict.py          <- Code to run model inference with trained models          
    │   └── train.py            <- Code to train models
    │
    └── plots.py                <- Code to create visualizations
```

--------

# Installation and Setup Guide for PyBGPStream on Windows using WSL2

This project uses [PyBGPStream](https://bgpstream.caida.org/) to work with BGP data.  
Since `PyBGPStream` depends on `libBGPStream` (only supported on Linux/macOS), we need to use **WSL2 with Ubuntu 22.04** on Windows.

Follow the steps below to install and configure the environment.

---

## 1. Install WSL2 with Ubuntu 22.04
Open **PowerShell as Administrator** and run:

```powershell
wsl --install -d Ubuntu-22.04
```

After installation is complete, **restart your computer**.

Verify that Ubuntu is installed and running:

```powershell
wsl -l -v
```

Expected output:
```
  NAME            STATE           VERSION
* Ubuntu-22.04    Running         2
```

If Ubuntu is not running version 2, set it manually:
```powershell
wsl --set-version Ubuntu-22.04 2
```

---

## 2. Install dependencies and `libBGPStream` in Ubuntu
Open the **Ubuntu terminal** (either from the Start Menu or by typing `wsl` in PowerShell).

Follow the official CAIDA installation guide:  
[https://bgpstream.caida.org/docs/install/bgpstream](https://bgpstream.caida.org/docs/install/bgpstream)

---

## 3. Move the project to the Ubuntu file system
For best performance, your project **must be inside Ubuntu's file system**, not on Windows' `/mnt/c` path.

If your project currently lives in Windows, copy it to your home directory in Ubuntu:

```bash
mkdir -p /home/<your_user>/projects
cp -r /mnt/c/Users/<your_user>/<your_project_folder> /home/<your_user>/<your_project_folder>/
```

> Replace `<your_user>` with your actual Windows and Ubuntu username.
> Replace `<your_project_folder>` with your actual folder for your project.

---

## 4. Install Python and venv in Ubuntu
In the Ubuntu terminal:

```bash
sudo apt install -y python3 python3-pip python3-venv
```

---

## 5. Create a virtual environment and install PyBGPStream
Navigate to your project folder inside Ubuntu and create a virtual environment:

```bash
cd /home/<your_user>/<your_project_folder>
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install pybgpstream
```

---

## 6. Configure Visual Studio Code to work with WSL
1. Install the **WSL** extension in VS Code.
![alt text](image.png)

2. Open VS Code and press `Ctrl + Shift + P`.
3. Select:
   ```
   WSL: Connect to WSL
   ```
4. Open the project folder located in `/home/<your_user>/<your_project_folder>`.
5. Check that the bottom left corner of VS Code displays:
   ```
   WSL: Ubuntu-22.04
   ```

---

## 7. Set the Python interpreter in VS Code
1. Press `Ctrl + Shift + P` → **Python: Select Interpreter**.
2. Choose the interpreter inside your virtual environment:
   ```
   .venv/bin/python
   ```

If it doesn't appear, manually browse to:
```
/home/<your_user>/<your_project_folder>/Project/.venv/bin/python
```

---

## 8. Configure and use notebooks
To work with notebooks, install Jupyter in your virtual environment:

```bash
source .venv/bin/activate
pip install jupyter ipykernel
python -m ipykernel install --user --name wsl-bgp --display-name "Python (WSL .venv)"
```

Then in VS Code:
1. Open the notebook `test_pybgpstream.ipynb`.
2. In the top-right corner, select the kernel:
   ```
   Python (WSL .venv)
   ```
3. Run the notebook cells to validate that `pybgpstream` works correctly.

---

## Summary
- Use WSL2 with Ubuntu 22.04 to install `libBGPStream`.
- Compile and install `libBGPStream` following the official CAIDA steps.
- Move your project folder to `/home/` inside Ubuntu for better performance.
- Create a virtual environment in Ubuntu and install `pybgpstream`.
- Configure VS Code with the Remote - WSL extension and point it to your Ubuntu virtual environment.
- Install Jupyter in the virtual environment to work with notebooks.
- Run `test_pybgpstream.ipynb` to confirm everything works as expected.