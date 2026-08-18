---
name: "COSMA CPU Compute Lab"
status: in-service
category: testbed
focus: open
focus-detail: "Prototyping and testing"
grouping: "COSMA"
funders:
- STFC
- Hypertec
partitions:
- name: Intel Sierra Forest
  nodes: 1
  accelerator: "Intel Xeon 6756E"
  accelerator-count: 2
  manufacturer: "Dell"
  scheduler: "Direct SSH"
- name: AMD Turin
  nodes: 1
  accelerator: "AMD EPYC 9755"
  accelerator-count: 2
  manufacturer: "Dell"
  scheduler: "Direct SSH"
- name: AMD Genoa
  nodes: 1
  accelerator: "AMD EPYC 9654"
  accelerator-count: 2
  manufacturer: "Ciara Technologies"
  scheduler: "Direct SSH"
interconnects: []
reference: https://cosma.readthedocs.io/en/latest/cpucomputelab.html
---

## COSMA CPU Compute Lab

COSMA (The Compute Optimised System for Modelling and Analysis) is a High Performance Computing facility hosted at Durham University, operated by the Institute for Computational Cosmology on behalf of DiRAC.

There are three CPU testbed nodes within COSMA:

| Node | RAM | CPU | Access |
|------|-----|-----|--------|
| mad11 | 1TB | 256 cores (Intel Sierra Forest) | Direct SSH |
| mad12 | 1.5TB | 256 cores (AMD EPYC Turin) | Direct SSH |
| mad13 | 1.5TB | 192 cores (AMD EPYC Genoa) | Direct SSH |


### Documentation

- <https://cosma.readthedocs.io/en/latest/cpucomputelab.html>
- <https://cosma.readthedocs.io/en/latest/cosma.html>

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

Connect directly via SSH from a login node; for example, `ssh mad11`

### Restrictions

Since there is no scheduler on these nodes,
you are requested to monitor node usage
(for example,
using the `w` command)
to avoid trampling over other people's benchmarking work.
