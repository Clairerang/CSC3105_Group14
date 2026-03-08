
## Quick Setup: 
1. Install `uv` package manager

    `python -m pip install uv        # this installs uv at global level`

2. Create a virutal enviornment
   
    `conda create -n uwb python=3.10 -y`

3. Activate the virutal enviornment

    `conda activate uwb`

4. Install required packages

    `uv sync                         # installs all required packages from uv.lock`

5. Start jupyter notebook

    `uv run jupyter-lab              # this starts jupyter notebook with integrated kernal from uv`