## How to Run Conda in Google Colab Without Restarting the Kernel

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/karagol-taner/Colab-Conda-Seamless-Setup/blob/main/colab_conda_norestart.ipynb)

Typically, installing Conda on Google Colab requires a frustrating kernel restart before the system recognizes the `conda` command. You can bypass this completely.

Here is the exact workflow to install Miniconda, create an environment, and use your bioinformatics tools immediately in a single run.

### Step 1: Install Miniconda & Update PATH
Run this block in a cell to download Miniconda, install it silently in batch mode, and make it instantly available to the current session.

``` python
#1. Download and install Miniconda silently
!wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
!bash /content/Miniconda3-latest-Linux-x86_64.sh -b -p /root/miniconda3

#2. Dynamically add Conda to the system PATH
import os
os.environ["PATH"] += os.pathsep + "/root/miniconda3/bin"
```

### Step 2: Create the Environment
Now you can use `conda` right away. Let's accept the Terms of Service, create an environment, and install our toolkit. 

```python
#3. Accept Anaconda agreements
!conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main
!conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/r

#4. Create the environment and install tools
conda create -n env_name python=3.10 -y -q
!source /root/miniconda3/bin/activate env_name

!conda install -c bioconda -c conda-forge \
    ..... \
    ..... -y -q

import os
os.environ["PATH"] += os.pathsep + "/root/miniconda3/envs/env_name/bin"
!source /root/miniconda3/bin/activate env_name
```

### Step 3: Add the Environment to PATH

```python
#5. Add the new environment's executables to the path
os.environ["PATH"] += os.pathsep + "/root/miniconda3/envs/env_name/bin"
```

You can now run your command-line tools directly in any subsequent cell.
