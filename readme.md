# Python Development Environment Setup

This repository contains configuration files and instructions for setting up a consistent Python development environment using Conda. The setup includes separate environments for Spyder and Jupyter Lab IDEs, which can connect to project-specific environments.

## Table of Contents
- [Initial Setup](#initial-setup)
- [IDE Environment Setup](#ide-environment-setup)
  - [Spyder Setup](#spyder-setup)
  - [Jupyter Setup](#jupyter-setup)
- [Project Environment Setup](#project-environment-setup)
- [Common Issues](#common-issues)
- [Useful Commands](#useful-commands)

## Initial Setup

1. Install Anaconda or Miniconda from [https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)

2. Clone this repository:
```bash
git clone [repository-url]
cd [repository-name]
```

3. Update conda:
```bash
conda update conda
```

## IDE Environment Setup

### Spyder Setup

1. Create the Spyder environment:
```bash
conda env create -f spyder_ide.yml
```

2. Activate and launch Spyder:
```bash
conda activate spyder_ide
spyder
```

### Jupyter Setup

1. Create the Jupyter environment:
```bash
conda env create -f jupyter_ide.yml
```

2. Activate and launch Jupyter Lab:
```bash
conda activate jupyter_ide
jupyter lab
```

## Project Environment Setup

For each new project, follow these steps:

1. Create a new environment YAML file following this template:
```yaml
name: your_project_name
channels:
  - conda-forge
  - defaults
dependencies:
  # Required for IDE connectivity - do not modify these
  - python=3.12
  - ipykernel          # required for Jupyter connectivity
  - spyder-kernels=3.0 # required for Spyder connectivity
  
  # Add your project-specific packages below
  # Examples:
  - numpy
  - pandas
  - matplotlib
  - pip
  
  # If you need packages from pip, add them here
  - pip:
    - special-package
```

2. Create the environment:
```bash
conda env create -f your_project_name.yml
```

3. Register the environment as a kernel:
```bash
conda activate your_project_name
python -m ipykernel install --user --name your_project_name --display-name "Python (your_project_name)"
```

### Connecting IDEs to Project Environment

#### Spyder
1. Go to Tools → Preferences → Python interpreter
2. Select "Use the following Python interpreter:"
3. Find your project environment path using:
```bash
conda activate your_project_name
python -c "import sys; print(sys.executable)"
```
4. Enter the path in Spyder's interpreter settings

#### Jupyter Lab
1. Launch Jupyter Lab from jupyter_ide environment
2. Create new notebook
3. Click Kernel → Change kernel
4. Select your project environment from the list

## Common Issues

### Spyder Kernel Issues
If you get a spyder-kernels version error:
```bash
conda activate your_project_name
conda install spyder-kernels=3.0
```

### Jupyter Kernel Not Showing
If your project kernel doesn't appear in Jupyter:
```bash
conda activate your_project_name
python -m ipykernel install --user --name your_project_name --display-name "Python (your_project_name)"
```

### Finding Environment Paths
To find your environment path:
```bash
conda activate your_project_name
python -c "import sys; print(sys.executable)"
```

## Useful Commands

List all environments:
```bash
conda env list
```

List all available Jupyter kernels:
```bash
jupyter kernelspec list
```

Remove a kernel:
```bash
jupyter kernelspec remove kernel_name
```

Update environment after changing .yml file:
```bash
conda env update -f environment.yml --prune
```

Export environment to YAML:
```bash
conda env export > environment.yml
```

## Directory Structure

```
.
├── README.md
├── spyder_ide.yml
├── jupyter_ide.yml
└── example_environments/
    └── example_project.yml
```
