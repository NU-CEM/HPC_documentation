## Technical Questions

- Can all long options to SBATCH have the option and parameter separated by either a space (eg. `--output hello-mpi-%j.out`) or an `=` (eg. `--output=hello-mpi-%j.out`)?
  - **Reasoning**: We should have consistent usage across the documentation.

- Re. "what is security like?", I was really meaning "is the cluster secure enough against direct cracking attempts that publishing its network details would not cause much, if any, more security risk?"
  - **Reasoning**: I was mainly concerned that some organisations prefer not to have internal or some external addresses publically available to help avoid direct cracking attempts.

- "Oswald only has a presence on the University internal network, so not much point in publishing it’s domain address."
  - I thought users would need the network information (oswald and ssh proxy addresses) to set up remote access themselves on their own devices? Eg. Lucy's setup required her to put these addresses in her ~/.ssh/config file.
  - **Reasoning**: This docs site should help users find out how to access the cluster more quickly (the "accessing oswald" section is for this). I know that HPC system documentation websites generally include this information to help users access the service.

- "There is a document decsribing how to access \[Oswald\] via the SSH Proxy Sevice."
  - Can I have a copy of that document? If not directly, how would I request it?
  - **Reasoning**: I believe this documentation site would be expected to include much of the information within that document relating to remote access (unless it's a security problem).

- Groups:
  - Are there any system groups (in `/etc/group`) in use beyond the linux defaults?
  - Can users request system groups to be created? Or are users expected to share their software/data in other ways if such fine-grained restrictions are needed?
  - **Reasoning**: Mainly the next question ...

- What is the exact default permissions for created files? (I assume directories have the same permissions, plus exec perms.) If the answer to either of the above questions about groups is 'yes', then the default group permissions are important in case they change the group of the file.
  - **Reasoning**: I think it would generally be useful to document file permissions in the context of research, especially as `/home` is shared by all users.

- From your explanation, I take it that `/tmp` isn't accessible directly by any users on any node? (It's part of the OS, which isn't accessible, right?)
  - I presume installed applications can access it, though?
  - **Reasoning**: I would expect that some HPC applications assume its existance and that they can read/write files/directories in it?

- Exclusivity of nodes + `/local` problems?
  - If nodes aren't exclusive, then shouldn't users of `/local` use their own subdirectory (eg. `/local/bob`) to avoid filename collisions between multiple jobs running on the same node at the same time?
  - How are users expected to clear /local after use? only delete the files they know they created, or wipe the drive? If the latter, the same issue with other jobs using the filesystem occurs
  - **Reasoning**: Eg. job A writes to /local/job.out; job B writes to /local/job.out; job A finishes and wipes /local/*; job B tries to read from /local/job.out -> crash/failure.

- Re. specifying number of nodes required for a job:
  - Say a user had a job that required 80 tasks (eg. it's quite parallelisable, and doesn't take that long if it's highly parallelised). That should take no more than 3 full nodes (28*3 = 84). Say Oswald was busy, and didn't have that many full nodes available (for at least a few hours), but did have various partially-occupied nodes available (some cores were free). If that user specified the number of nodes they required was exactly 3, then SLURM couldn't allocate more than 3 nodes, so couldn't allocate their 80 tasks until 3 full nodes were free (which could be hours). However, if they didn't specify the number of nodes it required - only the number of tasks - then SLURM could allocate it across several partially-free nodes (whose running jobs had not made them exclusive) and complete the task much sooner, while avoiding wasting idle cores.
  - Would this be a compelling enough reason to allow users to omit the number of nodes required (so long as they specify the number of tasks)?
  - The above example illustrates just one case where omitting the full set of options you suggest may *improve* oswald's usage. My general question is: If a user's SLURM job configuration is valid and wouldn't adversely harm system performance, system stability, or other users, then what reasons would you (the administrators) have to restrict those configurations (if any)?
  - **Reasoning**: I thought it would be nice to put a minimal jobscript example in the docs to help users understand SLURM a bit better. If there is no reason to restrict valid and reasonable configurations that happen to omit some of your suggested options, then including my suggested minimal example (below) wouldn't be a problem:

    ```
    #!/bin/bash

    #SBATCH --ntasks 80
    #SBATCH --time 60:00:00
    #SBATCH --partition 72hour

    srun -n 80 your_desired_program_or_script
    ```

- What is the GPU node used for? is it just a specialised compute node?
  - How would users specify to use it? By using the relevant --gpu* options to SLURM?
  - **Reasoning**: This info should be included in the docs.

- What is the visualisation node used for? You said about using it for running GUI apps, but I thought it was a compute node (remote/job-based only) - am I wrong?
  - How would users go about running GUI apps on it? Would that be via another chained SSH connection (your-computer [-> SSH-proxy] -> oswald-head -> visualisation-node)?
  - **Reasoning**: This info should be included in the docs.

## Future Ideas

**Note**: These are things to think about for the future that cannot be answered right now.

- github organisation?
- moderation? - who? when? how?
  - depends on owner of github organisation that hosts repo

- google analytics?
  - stats about page popularity, etc.
  - management - who?

- use a university email as the sender? would the uni have to do anything?
  - see: https://mailchimp.com/help/limitations-of-free-email-addresses/
