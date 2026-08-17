---
name: "COSMA A30"
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
- nodes: 8
  accelerator: "NVIDIA A30"
  accelerator-count: 1
  manufacturer: "NVIDIA"
  scheduler: "Slurm"
  benchmarks:
  - type: memory-bandwidth-gb-s
    name: BabelStream
    value: 822
    parameters:
      array_size: 134217728
      iterations: 100
      precision: FP64
interconnects:
- CerIO composable fabric
reference: https://cosma.readthedocs.io/en/latest/gpu.html#dine2
---

## COSMA A30

COSMA (The Compute Optimised System for Modelling and Analysis) is a High Performance Computing facility hosted at Durham University, operated by the Institute for Computational Cosmology on behalf of DiRAC.

The A30 nodes form part of the DINE2 cluster, a GPU testbed within COSMA.

| Node | RAM | CPU | Access |
|------|-----|-----|--------|
| gc001-008 | 2TB | 64 cores (Intel Sapphire Rapids) | Slurm (`dine2`) |

8 A30 GPUs are shared across 8 nodes via a CerIO composable fabric, allowing GPUs to be dynamically allocated between nodes on request. Contact cosma-support@durham.ac.uk for specific configurations.

### Documentation

- <https://cosma.readthedocs.io/en/latest/dine2.html>
- <https://cosma.readthedocs.io/en/latest/gpu.html#dine2>
- <https://www.nvidia.com/en-gb/data-center/products/a30-gpu/>

### Gaining access

Access requires a COSMA account, obtained via the [DiRAC SAFE portal](https://safe.epcc.ed.ac.uk/dirac/).

1. Create a SAFE account with an institutional email.
2. Upload an SSH public key on SAFE. If you do not have one, generate with `ssh-keygen -t ed25519`.
3. Request a login account. This requires selecting a project, either:
- Project `do015` for DINE2 testbed access.
- A DiRAC project code for a given allocation (provided by a supervisor).
4. **Wait** for the account to be approved by the project manager. Keep an eye on your email!
5. Connect to COSMA via SSH: `ssh username@login8.cosma.dur.ac.uk` (Note: On first login you will be asked to change the password provided in your email)

Visit <https://cosma.readthedocs.io/en/latest/account.html> for more details.
Contact cosma-support@durham.ac.uk for any questions.

### Usage

Jobs are submitted via Slurm to the `dine2` partition:
```bash
#!/bin/bash
#SBATCH --partition=dine2
#SBATCH --account=do015
#SBATCH --time=01:00:00

nvidia-smi
./gpu_program_to_run
```

nvidia-specific compilers and tools can be loaded from the `nvhpc` module on cosma.
To load this module, check available versions with:
```module av nvhpc```
Then load the desired version with:
```module load nvhpc/VERSION```


### Restrictions

- dine2 nodes mount `/dine` not `/cosma5`. Copy binaries to `/dine/data/<project>/<username>/`.
- Maximum wall time: 3 days
