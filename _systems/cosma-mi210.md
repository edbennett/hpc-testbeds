---
name: "COSMA MI210"
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
- nodes: 2
  accelerator: "AMD MI210"
  accelerator-count: 2
  manufacturer: "AMD"
  scheduler: "Slurm"
  benchmarks:
  - type: memory-bandwidth-gb-s
    name: BabelStream
    value: 1250
    parameters:
      array_size: 134217728
      iterations: 100
      precision: FP64
interconnects:
reference: https://cosma.readthedocs.io/en/latest/amdgpu.html
---

## COSMA MI210

COSMA (The Compute Optimised System for Modelling and Analysis) is a High Performance Computing facility hosted at Durham University, operated by the Institute for Computational Cosmology on behalf of DiRAC.

The MI210 nodes are GPU testbeds within COSMA.

| Node | RAM | CPU | Access |
|------|-----|-----|--------|
| ga005 | 1TB | 64 cores (AMD EPYC 7513) | Slurm (`cosma8-shm2`) |
| ga006 | 1TB | 64 cores (AMD EPYC 7513) | Slurm (`cosma8-shm2`) |

The MI210 is built to accelerate deep learning training via mixed-precision capabilities.

### Documentation

- <https://cosma.readthedocs.io/en/latest/amdgpu.html>
- <https://cosma.readthedocs.io/en/latest/gpu.html>
- <https://www.amd.com/en/products/accelerators/instinct/mi200/mi210.html>

### Gaining access

Access requires a COSMA account, obtained via the [DiRAC SAFE portal](https://safe.epcc.ed.ac.uk/dirac/).

1. Create a SAFE account with an institutional email.
2. Upload an SSH public key on SAFE. If you do not have one, generate with `ssh-keygen -t ed25519`.
2. Request a login account. This requires selecting a project, either:
- Project `do018` for AMD GPU testbed access.
- A DiRAC project code for a given allocation (provided by a supervisor).
3. **Wait** for the account to be approved by the project manager. Keep an eye on your email!
4. Connect to COSMA via SSH: `ssh username@login8.cosma.dur.ac.uk` (Note: On first login you will be asked to change the password provided in your email)

Visit <https://cosma.readthedocs.io/en/latest/account.html> for more details.
Contact cosma-support@durham.ac.uk for any questions.

### Usage

Jobs are submitted via Slurm to the `cosma8-shm2` partition:
```bash
#!/bin/bash
#SBATCH -partition=cosma8-shm2
#SBATCH --account=do018
#SBATCH --time=01:00:00
#SBATCH --exclude=ga004

rocm-smi # checks existence of GPU
./gpu_program_to_run
```

`--exclude=ga004` ensures you are allocated an MI210 node within the cosma8-shm2 partition (ga004 has an MI100).

The AMD ROCm stack can be loaded from the `hipcc` module on cosma.
To load this module, check available versions with:
```module av hipcc```
Then load the desired version with:
```module load hipcc/VERSION```

If your codebase is based on CUDA, you can convert this to HIP using the `hipify` script provided with ROCm.

### Restrictions

- Maximum wall time: 3 days
- Nodes are non-exclusive by default (shared with other users). Use `--exclusive` if you require the entire node
