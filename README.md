# Neural Networks Workshop for Remote Sensing

Two practical sessions of approximately two hours each introducing neural networks through visual, hands-on Jupyter notebooks, with examples motivated by remote sensing.

**Visual Studio Code is the recommended environment for running the workshop.**

**Instructor:** Efraín Padilla  
**Affiliation:** DLR IMF-ASP

## Workshop outline

The planned structure is deliberately compact and notebook-oriented:

### Day 1 — Neural-network fundamentals

- Fundamentals of optimization
- Linear regression and least squares
- Gradient descent
- Loss functions and the neuron
- Regression and classification with activation functions
- Examples of regression and classification in remote sensing

### Day 2 — Feature Extraction and Bigger Neural Networks

- Inputs: vectors, matrices, cubes, and n-dimensional tensors
- Data space
- Training, validation, and testing
- Optimizers
- Spatial feature extraction
- Spatial-spectral feature extraction

Each session should alternate short explanations with executable cells and visual checkpoints. The notebooks will use small or prepared datasets so that the workshop can run on a CPU; GPU acceleration is optional.

## Requirements

- Python 3.11-compatible computer with internet access.
- For Windows: Windows 10 version 2004 or newer, or Windows 11, with WSL 2.
- [Visual Studio Code](https://code.visualstudio.com/) with the **Python** and **Jupyter** extensions.
- For Windows/WSL: the **WSL** extension for Visual Studio Code.

The supplied [`env.yml`](env.yml) is a Linux-oriented, exported environment. It pins Linux package build strings and includes PyTorch with CUDA 12.4. It is therefore the reference environment for Linux and WSL 2 on an x86_64 machine with a compatible NVIDIA setup. The notebooks should still be designed to run on CPU.

## Install Miniconda

Use the installer matching your operating system and architecture. Initialize Conda during installation.

### Windows with WSL 2

Install Ubuntu/WSL 2 from an elevated PowerShell prompt:

```powershell
wsl --install -d Ubuntu
```

Then, inside the WSL terminal, install Miniconda for Linux x86_64:

```bash
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
source ~/.bashrc
```

For NVIDIA GPU use in WSL, install the current NVIDIA Windows driver that supports WSL GPU compute. A GPU is not required for the workshop.

### Linux

For a standard x86_64 Linux computer:

```bash
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
source ~/.bashrc
```

On an ARM64 Linux computer, replace `Linux-x86_64` with `Linux-aarch64` in the download URL and installer filename. The exported `env.yml` may still require adjustment for ARM64.

### macOS

For Apple Silicon Macs (M1/M2/M3/M4 and later), use the ARM64 installer:

```bash
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh
bash Miniconda3-latest-MacOSX-arm64.sh
source ~/.zshrc
```

The current `env.yml` is not a native macOS environment: its package records target Linux and its PyTorch build targets CUDA. Consequently, the exact file is expected to work on Linux/WSL, but not necessarily on macOS. On macOS, the environment should be regenerated from platform-independent package specifications before the workshop is distributed. Until that portable file is added, do not expect `conda env create -f env.yml` to succeed natively on macOS.

Intel macOS users should consult the [official Miniconda macOS installation page](https://www.anaconda.com/docs/getting-started/miniconda/install/mac-cli-install) for the available legacy installer. The workshop's environment will also need a macOS-compatible regeneration.

## Create the workshop environment

From the project root, activate the environment definition supplied with the repository:

```bash
conda env create --name neural-networks-workshop --file env.yml
conda activate neural-networks-workshop
```

If an environment with that name already exists and you want to update it:

```bash
conda env update --name neural-networks-workshop --file env.yml --prune
conda activate neural-networks-workshop
```

The `prefix:` line at the end of `env.yml` records the original author's installation path. The `--name` option above is intentional: it creates the environment in your own Conda installation rather than using that path.

Verify the main packages:

```bash
python --version
python -c "import numpy, matplotlib, sklearn, torch; print('PyTorch:', torch.__version__); print('CUDA available:', torch.cuda.is_available())"
```

## Use Visual Studio Code

Visual Studio Code is the recommended environment for the workshop. Install the **Python** and **Jupyter** extensions; Windows/WSL users also need the **WSL** extension.

Open the repository in VS Code, using a WSL remote window when applicable, and select the `neural-networks-workshop` Conda environment as the Python interpreter and notebook kernel.

From the repository root, it can also be opened with:

```bash
code .
```

No separate Jupyter server is required; notebooks run through the VS Code Jupyter extension.

## Official installation references

- [Install WSL](https://learn.microsoft.com/en-us/windows/wsl/install)
- [Miniconda on Linux](https://www.anaconda.com/docs/getting-started/miniconda/install/linux-install)
- [Miniconda on macOS](https://www.anaconda.com/docs/getting-started/miniconda/install/mac-cli-install)
- [Conda environments](https://www.anaconda.com/docs/getting-started/working-with-conda/environments)
