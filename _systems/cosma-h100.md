---
name: "COSMA H100"
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
  accelerator: "NVIDIA H100 NVL"
  accelerator-count: 1
  manufacturer: "NVIDIA"
  scheduler: "Direct SSH"
  benchmarks:
  - type: memory-bandwidth-gb-s
    name: BabelStream
    value: 3387
    parameters:
      array_size: 134217728
      iterations: 100
      precision: FP64
interconnects:
reference: https://cosma.readthedocs.io/en/latest/gpu.html#h100 
---

## COSMA GH200

COSMA (The Compute Optimised System for Modelling and Analysis) is a High Performance Computing facility hosted at Durham University, operated by the Institute for Computational Cosmology on behalf of DiRAC.

The H100 NVL (Hopper) node is a GPU testbed within COSMA.

| Node | RAM | CPU | Access |
|------|-----|-----|--------|
| gn004 | 510GB | 64 cores (Intel Xeon) | Direct SSH |

The H100 NVL is a high-memory variant of NVIDIA's H100. It is optimised for LLM Inference because of its high memory bandwidth, compute density, and energy efficiency.

### Documentation

- <https://cosma.readthedocs.io/en/latest/gpu.html#h100>
- <https://www.nvidia.com/content/dam/en-zz/Solutions/Data-Center/h100/PB-11773-001_v01.pdf>

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

Connect directly to gn004 via SSH from a login node:
```bash
ssh gn004
nvidia-smi
./gpu_program_to_run
```

nvidia-specific compilers and tools can be loaded from the `nvhpc` module on cosma.
To load this module, check available versions with:
```module av nvhpc```
Then load the desired version with:
```module load nvhpc/VERSION```


### Restrictions

- Shared resource. Before running large jobs, check if others are using the nodes. Access is SSH only, so there is no SLURM queue.  Check running processes using `top`, or logged-in users using `users`
