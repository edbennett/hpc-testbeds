---
name: Bede
status: in-service
category: production
focus: regional
focus-detail: N8 group universities, and EPSRC-funded projects
grouping: N8CIR
funders:
- N8
- EPSRC
partitions:
- nodes: 32
  accelerator: NVIDIA Tesla V100 32G
  accelerator-count: 4
  manufacturer: IBM
  scheduler: Slurm
- nodes: 4
  accelerator: NVIDIA Tesla T4 16G
  accelerator-count: 4
  manufacturer: IBM
  scheduler: Slurm
- nodes: 6
  accelerator: NVIDIA H100 96GB
  accelerator-count: 1
  manufacturer: Vespertec
  scheduler: Slurm
  name: H100 Verpertec
- nodes: 1
  accelerator: NVIDIA H100 96GB
  accelerator-count: 1
  manufacturer: Supermicro
  scheduler: Slurm
  name: H100 Supermicro
- nodes: 1
  accelerator: NVIDIA H100 144GB
  accelerator-count: 2
  manufacturer: Supermicro
  scheduler: Slurm
interconnects:
- InfiniBand EDR
- NVLink 2.0
reference: https://n8cir.org.uk/bede/
---

<!-- Text shown in comment tags like this will not be visible in the generated page.
     In the block above,
     they should be removed entirely. -->

## Bede

Bede is a supercomputer hosted at Durham University on behalf of N8CIR.
The main supercomputer comprises 32 `gpu` nodes and 4 `infer` running on PowerPC chips. Bede also includes a NVIDIA Grace-Hopper partition, with 7 nodes with a Grace Hopper Superchip with a H100 96GB gpu module, and one node with 2 Grace Hopper Superchips with a H100 144GB gpu module each.

Within each `gpu` node in the original system, the CPU and GPUs are linked to a single NVLink 2.0 bus. Nodes are connected with dual-rail Mellanox EDR Infiniband interconnects. `infer` nodes have GPUs on the PCIe bus. The Grace Hopper Superchips include a 900 GB/s NVLink-C2C within the chip and Mellanox CONNECTX-7 NDR200 Infiniband interconnects between nodes.

### Partition specifications

Note that all Grace Hopper nodes are in the `gh` partition but have two different specifications within the partition. The monster node `gh008` can be requested with the sbatch `--nodelist` argument.

| Partition | Accelerator | RAM | CPU | Connectivity | Access |
|-|-|-|-|-|-|
| `gpu` | 4x Tesla V100 32GB | 512GB DDR4 | 32 cores/4 threads per core @2.7GHz (2xIBM POWER9) | 2x Mellanox EDR Infiniband | Slurm via `login` nodes |
| `infer` | 4x Tesla T4 16GB PCIe | 256GB DDR4 | 40 cores/4 threads per core @2.9GHz (2xIBM POWER9) | 1x Mellanox EDR Infiniband | Slurm via `login` nodes |
| `gh001`-`gh007` | H100 96GB | 480GB LPDDR5X | 72 cores @3.483GHz (NVIDIA Grace ARM Neoverse V2) | 1x Mellanox CONNECTX-7 NDR200 @100Gbps | Slurm via `gh-login` nodes |
| `gh008` | 2x H100 144GB | 960GB LPDDR5X | 144 cores @3.483GHz (2x NVIDIA Grace ARM Neoverse V2) | 2x Mellanox CONNECTX-7 NDR200 @100Gbps | Slurm via `gh-login` nodes |

### Documentation

- <https://bede-documentation.readthedocs.io/en/latest/>
- <https://bede-documentation.readthedocs.io/en/latest/hardware/>
- <https://bede-documentation.readthedocs.io/en/latest/usage>
- <https://www.nvidia.com/en-gb/data-center/grace-hopper-superchip/>

### Gaining access

To gain access to Bede for your project, a request form must be submitted. Project access can be requested by projects from N8 group universities, or through the EPSRC access to HPC programme. Additionally, the EPSRC High End Computing consortia are allocated a portion of compute time on Bede.
Details on these application routes can be found at <https://n8cir.org.uk/bede/accessing-bede/>. Once an application has been successful, the administrators will issue a project code which can be used to get an account on Bede.

For researchers on a project registered on Bede to gain access, you will need to create an EPCC SAFE account at <https://safe.epcc.ed.ac.uk/>, and then request access with the project code which you should be able to get from your project PI. Further details on how to gain access to Bede, and how to make use of the system once you have gained access, are at <https://bede-documentation.readthedocs.io/en/latest/usage>

### Restrictions

The maximum time limit for jobs on production nodes is 2 days. There are no other limits on job size defined, other than the maximum size the hardware can accomodate. Jobs will be scheduled by Slurm with multifactor priority.

Binaries must be compiled for the architecture of the partition used; PowerPC for the main nodes, ARM for the Grace Hopper nodes.
