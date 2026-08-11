---
name: "COSMA MI100"
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
- nodes: 1
  accelerator: "AMD MI100"
  accelerator-count: 1
  manufacturer: "AMD"
  scheduler: "Slurm"
  benchmarks:
  - type: memory-bandwidth-gb-s
    name: BabelStream
    value: 947
    parameters:
      array_size: 134217728
      iterations: 100
      precision: FP64
interconnects:
reference: https://cosma.readthedocs.io/en/latest/amdgpu.html
---

## COSMA MI100

COSMA (The Compute Optimised System for Modelling and Analysis) is a High Performance Computing facility hosted at Durham University, operated by the Institute for Computational Cosmology on behalf of DiRAC.

The MI100 node is a GPU testbed within COSMA.

| Node | RAM | CPU | Access |
|------|-----|-----|--------|
| ga004 | 1TB | 128 cores (AMD EPYC Milan 7713) | Slurm (`cosma8-shm2`) |

### Documentation

- <https://cosma.readthedocs.io/en/latest/amdgpu.html>
- <https://cosma.readthedocs.io/en/latest/gpu.html>
- <https://www.amd.com/en/products/accelerators/instinct/mi100.html>

### Gaining access

Access requires a COSMA account, obtained via the [DiRAC SAFE portal](https://safe.epcc.ed.ac.uk/dirac/).

1. Create a SAFE account with an institutional email.
2. Upload an SSH public key on SAFE. If you do not have one, generate with `ssh-keygen -t ed25519`.
3. Request a login account. This requires selecting a project, either:
   - Project `do018` for AMD GPU testbed access.
   - A DiRAC project code for a given allocation (provided by a supervisor).
4. **Wait** for the account to be approved by the project manager. Keep an eye on your email!
5. Connect to COSMA via SSH: `ssh username@login8.cosma.dur.ac.uk` (Note: On first login you will be asked to change the password provided in your email)

Visit <https://cosma.readthedocs.io/en/latest/account.html> for more details.
Contact cosma-support@durham.ac.uk for any questions.

### Usage

Jobs are submitted via Slurm to the `cosma8-shm2` partition:
```bash
#!/bin/bash
#SBATCH --partition=cosma8-shm2
#SBATCH --account=do018
#SBATCH --time=01:00:00
#SBATCH --nodelist=ga004

rocm-smi
./gpu_program_to_run
```

`--nodelist=ga004` ensures allocation the MI100 node (ga005/ga006 have MI210s).

The AMD ROCm stack can be loaded from the `hipcc` module on cosma.
To load this module, check available versions with:
```module av hipcc```
Then load the desired version with:
```module load hipcc/VERSION```

If your codebase is based on CUDA, you can convert this to HIP using the `hipify` script provided with ROCm.

### Restrictions

- Maximum wall time: 3 days
- Nodes are non-exclusive by default (shared with other users). Use `--exclusive` if you require the entire node
