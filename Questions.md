## Technical Questions

### Little Questions

- what does "IB" mean in "1GB/10GB/IB"
- `--output=hello-mpi-%j.out`
- what is the debug queue's maximum wallclock time? (1 minute or 1 hour?)

### Others

- what is Oswald's security like?
- is public visibility of addresses ok?
  - should we publish its domain address (oswald.campus.unn.ac.uk)?
  - should we publish information about how to get remote access to it (through garrett)?
    > once we figure this out ourselves ^_^

- what filesystems are available on Oswald? In particular:
  - general:
    - is the 1TB SSD accessible?

    - is there a /home?
      - is this the 185TB HDD on the head node?
      - are files shared across user folders?

    - is there a /tmp and $TMPDIR?
      - is this the 120GB SSD on each (normal) compute node?
      - otherwise, how big is it?

    - where is the 88TB of Lustre storage mounted on compute nodes?
      - I presume it's not available from the head node?

    - is there any scratch storage?

  Basically:

  - what storage is available?
    - where is it mounted on the different nodes?

  - what are the specs/policies of each of those mounts?
    - speed?
    - parallel (yes/no)
    - quotas?
      - per user
      - over time
      - any more?
    - backups?
    - instructions for use?
    - anything else?

- how is exclusivity configured?
  - https://slurm.schedmd.com/cons_res_share.html
    - exclusive = if one job reserves them, other jobs can't use them
    - oversubscribe option allows sharing nodes
      - uses least-loaded algorithm - favors unit of resource (nodes, or something else with below plugin) that is currently allocated the fewest jobs

    - trade-off: individual job performance vs. system utilisation

  - https://slurm.schedmd.com/cons_res.html
    - usually per-node (these plugins change that)

  - https://slurm.schedmd.com/srun.html
    - `--oversubscribe`
    - used to be called `--share` - https://hpcc.umd.edu/hpcc/help/jobs.html

  - for eg:
    - CPU cores
    - RAM
    - disk space
    - etc.

- would allowing default job script options be acceptable?
  - some of them are somewhat sensible, depending on the job

  - in particular, do you need to specify the number of nodes, as the default is 'as many as are needed'

- other compilers? - cray? AOCC?
  - why to people use various different compilers anyway? (apart from for binary compat, eg. with libs)

## Mixed Tech/Policy Questions

- github organisation?
- moderation? - who? when? how?
  - depends on owner of github organisation that hosts repo

- google analytics?
  - stats about page popularity, etc.
  - management - who?

- use a university email as the sender? would the uni have to do anything?
  - see: https://mailchimp.com/help/limitations-of-free-email-addresses/

## Policy Questions

- working directly on the head?
  - see my warning - https://nu-cem.github.io/HPC_internship_2021/quickstart/running-jobs

## Research Questions

- what fields of research is Oswald used in?
