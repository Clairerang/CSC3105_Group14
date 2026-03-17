
## Quick Setup: 
1. Install `uv` package manager

    `python -m pip install uv        # this installs uv at global level`

2. Create a virutal enviornment
   
    `conda create -n uwb python=3.13 -y`

3. Activate the virutal enviornment

    `conda activate uwb`

4. Install required packages

    `uv sync                         # installs all required packages from uv.lock`

    If you already created `.venv` with Python 3.14, delete it first so `uv` can recreate it with Python 3.13.

5. Start jupyter notebook

    `uv run jupyter-lab              # this starts jupyter notebook with integrated kernal from uv`
