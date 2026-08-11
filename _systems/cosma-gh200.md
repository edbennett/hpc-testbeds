---
name: "COSMA GH200"
status: in-service
category: testbed
focus: open
focus-detail: "Prototyping and testing"
grouping: "COSMA"
funders:
- STFC
- DiRAC
- ExCALIBUR
partitions:
- name: "gn002"
  nodes: 1
  accelerator: "NVIDIA GH200"
  accelerator-count: 1
  manufacturer: "NVIDIA"
  scheduler: "Direct SSH"
- name: "gn003"
  nodes: 1
  accelerator: "NVIDIA GH200"
  accelerator-count: 1
  manufacturer: "NVIDIA"
  scheduler: "Slurm"
  benchmarks:
  - type: memory-bandwidth-gb-s
    name: BabelStream
    value: 3500
    parameters:
      array_size: 134217728
      iterations: 100
      precision: FP64
interconnects:
- NVLink-C2C
reference: https://cosma.readthedocs.io/en/latest/gpu.html#grace-hopper
---

## COSMA GH200

COSMA (The Compute Optimised System for Modelling and Analysis) is a High Performance Computing facility hosted at Durham University, operated by the Institute for Computational Cosmology on behalf of DiRAC.

The GH200 (Grace Hopper) nodes are GPU testbeds within COSMA.

| Node | RAM | CPU | Access |
|------|-----|-----|--------|
| gn002 | 480GB (unified) | 72 cores (ARM Grace) | Direct SSH |
| gn003 | 480GB (unified) | 72 cores (ARM Grace) | Slurm (`gracehopper`) |

The GH200 is NVIDIA's "Superchip"; It achieves a CPU+GPU coherent memory model by combing an NVIDIA H100 GPU and an NVIDIA Grace CPU using NVIDIA NVLINK-C2C. 

As the Grace CPU is Arm-based (aarch64), x64 binaries will not run. Code must be compiled on the node itself.

### Documentation

- <https://cosma.readthedocs.io/en/latest/gpu.html#grace-hopper>
- <https://cosma.readthedocs.io/en/latest/cosma.html>
- <https://www.nvidia.com/en-gb/data-center/grace-hopper-superchip>

### Gaining access

Access requires a COSMA account, obtained via the [DiRAC SAFE portal](https://safe.epcc.ed.ac.uk/dirac/).

1. Create a SAFE account with an institutional email.
2. Upload an SSH public key on SAFE. If you do not have one, generate with `ssh-keygen -t ed25519`.
2. Request a login account. This requires selecting a project, either:
- Project `do016` for NVIDIA GPU testbed access.
- A DiRAC project code for a given allocation (provided by a supervisor).
3. **Wait** for the account to be approved by the project manager. Keep an eye on your email!
4. Connect to COSMA via SSH: `ssh username@login8.cosma.dur.ac.uk` (Note: On first login you will be asked to change the password provided in your email)

Visit <https://cosma.readthedocs.io/en/latest/account.html> for more details.
Contact cosma-support@durham.ac.uk for any questions.

### Usage

For gn002, connect directly via SSH from a login node: `ssh mad06`

For gn003, jobs are submitted via Slurm to the `gracehopper` partition:
```bash
#!/bin/bash
#SBATCH --partition=gracehopper
#SBATCH --account=do016
#SBATCH --time=01:00:00

nvidia-smi # checks existence of GPU
./gpu_program_to_run
```

CUDA is available in `/usr/local/cuda-VERSION`.

nvidia-specific compilers and tools can be loaded from the `nvhpc` module on cosma.
To load this module, check available versions with:
```module av nvhpc```
Then load the desired version with:
```module load nvhpc/VERSION```

Grace-Hopper nodes may require alternative toolchains.  
These can be found in `/opt/rh/`

Toolchains can be selected when compiling with nvc++ like so:
```nvc++ --std=c++17 --gcc-toolchain=/opt/rh/gcc-toolset-15 main.cpp```

### Restrictions

- Maximum wall time: 3 days
- x86 binaries will not run. Code must be compiled on the node itself
- No system cmake on nodes. Install cmake using `pip3 install --user cmake` and add `$HOME/.local/bin` to PATH
