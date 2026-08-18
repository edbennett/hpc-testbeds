---
name: "Tursa"
status: in-service
category: production
focus: discipline
focus-detail: "High-Energy Physics"
grouping: "DiRAC"
funders:
- STFC
- UKRI
- DSIT
partitions:
- nodes: 114
  accelerator: "NVIDIA A100 40GB"
  accelerator-count: 4
  manufacturer: "Atos"
  scheduler: "Slurm"
- nodes: 65
  accelerator: "NVIDIA A100 80GB"
  accelerator-count: 4
  manufacturer: "Atos"
  scheduler: "Slurm"
profilers:
- NVIDIA Nsight
modules: Environment Modules 4.1.4
software-installation:
- Manual installation
interconnects:
- Infiniband HDR
- NVLink
reference: https://epcced.github.io/dirac-docs/tursa-user-guide/
---

Tursa is a GPU cluster hosted at [EPCC][epcc]
on behalf of [DiRAC][dirac].
Comprising 181 x Atos BullSequana nodes,
114 with 4 x NVIDIA A100-40GB GPUs
and 65 with 4 x NVIDIA A100-80 GPUs,
it was designed for performing
strong scaling computations in lattice quantum field theory.

GPUs are linked by NVLink within each node,
and each GPU has a dedicated fabric adapter with GPUdirect RDMA,
allowing for very good strong scaling performance..
The machine has also been demonstrated to perform well
for machine learning applications,
including training of large language models.

### Documentation

- <https://epcced.github.io/dirac-docs/tursa-user-guide/>
- <https://www.dirac.ac.uk>

### Gaining access

Access for production workloads is via
an annual call by the DiRAC Resource Allocation Committee.
Seedcorn and benchmarking access is available on an _ad-hoc_ basis
via "Director's discretionary allocations",
requested via email to the DiRAC director.

### Restrictions

Nodes must be allocated in powers of two.
Jobs may run for up to 48 hours while budget is available.
When budget is exhausted,
low-priority access is available for up to four queued jobs at a time,
with a wall-time limit of 24 hours.

[dirac]: <https://dirac.ac.uk>
[epcc]: <https://epcc.ed.ac.uk>
