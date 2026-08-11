---
name: "COSMA A100"
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
partitions:
- name: "cosma8-shm"
  nodes: 2
  accelerator: "NVIDIA A100 40GB"
  accelerator-count: 1
  manufacturer: "Dell"
  scheduler: "Slurm"
  benchmarks:
  - type: memory-bandwidth-gb-s
    name: BabelStream
    value: 1352
    parameters:
      array_size: 134217728
      iterations: 100
      precision: FP64
- name: "mad06"
  nodes: 1
  accelerator: "NVIDIA A100 40GB"
  accelerator-count: 1
  manufacturer: "Dell"
  scheduler: "Direct SSH"
interconnects:
- Infiniband HDR200
- Liqid composable fabric
reference: https://cosma.readthedocs.io/en/latest/gpu.html#using-the-composable-a100-gpus
---

## COSMA A100

COSMA (The Compute Optimised System for Modelling and Analysis) is a High Performance Computing facility hosted at Durham University, operated by the Institute for Computational Cosmology on behalf of DiRAC.

The A100 nodes are GPU testbeds within COSMA.

| Node | RAM | CPU | Access |
|------|-----|-----|--------|
| mad04 | 4TB | 128 cores (AMD EPYC) | Slurm (`cosma8-shm`) |
| mad05 | 4TB | 128 cores (AMD EPYC) | Slurm (`cosma8-shm`) |
| mad06 | 1TB | 128 cores (AMD EPYC Milan-X) | Direct SSH |

The A100 GPUs (3 total) are connected via a Liqid composable fabric, allowing them to be moved between these nodes. The default configuration is 1 GPU per node. To request a different configuration, contact cosma-support@durham.ac.uk.

### Documentation

- <https://cosma.readthedocs.io/en/latest/gpu.html#using-the-composable-a100-gpus>
- <https://cosma.readthedocs.io/en/latest/cosma.html>
- <https://www.nvidia.com/en-gb/data-center/a100> 

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

For mad04 and mad05, jobs are submitted via Slurm to the `cosma8-shm` partition:
```bash
#!/bin/bash
#SBATCH --partition=cosma8-shm
#SBATCH --account=do016
#SBATCH --time=01:00:00
#SBATCH --constraint=gpu

nvidia-smi # checks existence of GPU
./gpu_program_to_run
```

`--constraint=gpu` ensures you're given a node with a GPU.

`--include` and `--exclude` can be used as SLURM parameters to specify particular nodes.

For mad06, connect directly via SSH from a login node: `ssh mad06`

nvidia-specific compilers and tools can be loaded from the `nvhpc` module on cosma.
To load this module, check available versions with:
```module av nvhpc```
Then load the desired version with:
```module load nvhpc/VERSION```

### Restrictions

- Maximum wall time: 3 days
- Nodes are non-exclusive by default (shared with other users). Use `--exclusive` if you require the entire node
- CUDA is available via `module load nvhpc/25.11`
