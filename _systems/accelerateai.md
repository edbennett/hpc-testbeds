---
name: "AccelerateAI"
status: in-service
category: production
focus: regional
focus-detail: "Wales"
grouping: "Supercomputing Wales"
funders:
- ERDF
- Welsh Government
partitions:
- nodes: 6
  accelerator: "NVIDIA A100 40GB"
  accelerator-count: 8
  manufacturer: "Atos"
  scheduler: "Slurm"
profilers:
- NVIDIA Nsight
- Intel VTune/Advisor
modules: Lmod 9.2
software-installation:
- Manual installation
- Spack
- EasyBuild
interconnects:
- Infiniband HDR
- NVLink
reference: https://sa2c.github.io/AccelerateAI
---

## AccelerateAI

AccelerateAI is a GPU cluster hosted at Swansea University.
Comprising 6 x Atos BullSequana nodes,
each with 8 x NVIDIA A100 GPUs,
it serves the machine learning needs of Wales.
It forms part of the Supercomputing Wales infrastructure.

GPUs are linked by NVLink in pairs.
Using more than 2 GPUs in parallel requires data transfer over the system bus.

### Documentation

- <https://sa2c.github.io/AccelerateAI>
- <https://portal.supercomputing.wales>

### Gaining access

Access is restricted to members of the Supercomputing Wales partner institutions
and their external collaborators.
Access is initially via a user account and project request
to the [MySCW Service][myscw],
where access to AccelerateAI should be mentioned explicitly.

### Restrictions

By default,
jobs may use up to 4 GPUs.
Runs with more than 4 GPUs may be enabled
when evidence of scalability of a project's work to 4 GPUs is demonstrated,
since the system is not designed for scalability to large GPU counts,
and many problems will not scale well.

Jobs may run for up to 48 hours.

[myscw]: <https://my.supercomputing.wales>
