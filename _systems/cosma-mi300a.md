---
name: "COSMA MI300A"
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
  accelerator: "AMD MI300A 128GB"
  accelerator-count: 4
  manufacturer: "AMD"
  scheduler: "Direct SSH"
  benchmarks:
  - type: memory-bandwidth-gb-s
    name: BabelStream
    value: 3648
    parameters:
      array_size: 134217728
      iterations: 100
      precision: FP64
interconnects:
reference: https://cosma.readthedocs.io/en/latest/amdgpu.html#mi300a 
---

## COSMA MI300A

COSMA (The Compute Optimised System for Modelling and Analysis) is a High Performance Computing facility hosted at Durham University, operated by the Institute for Computational Cosmology on behalf of DiRAC.

The MI300A node is a GPU testbed within COSMA.

| Node | RAM | CPU | Access |
|------|-----|-----|--------|
| ga008 | 500GB (unified) | 96 cores (AMD EPYC) | Direct SSH |

The MI300A is an APU (Accelerated Processing Unit). The CPU and GPU are on the same silicon and share physical RAM. Therefore, memory copies between CPU and GPU are not necessary which can improve performance for many applications.

The MI300A node has 4x GPUs. 

### Documentation

- <https://cosma.readthedocs.io/en/latest/amdgpu.html#mi300a>
- <https://cosma.readthedocs.io/en/latest/gpu.html#mi300a>
- <https://www.amd.com/en/products/accelerators/instinct/mi300/mi300a.html>

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

Connect directly via SSH from a login node:
```bash
ssh ga008
rocm-smi
./gpu_program_to_run
```

The AMD ROCm stack can be loaded from the `hipcc` module on cosma.
To load this module, check available versions with:
```module av hipcc```
Then load the desired version with:
```module load hipcc/VERSION```

If your codebase is based on CUDA, you can convert this to HIP using the `hipify` script provided with ROCm.


### Restrictions

- `/cosma5/` is not mounted on ga008. Copy binaries to your home directory first.
- ga008 is a shared resource, please be mindful of other users when running codes.  Use `top` to see running processes or `users` to see who else is logged in.
