## Technical Questions

- Re. "what is security like?", I was mainly meaning "is the cluster secure enough against direct cracking attempts that publishing its network details would not cause much, if any, more security risk?" Users would need this network information (oswald and ssh proxy addresses) to set up remote access themselves on their own devices.

- I think the contents of the document about connecting to Oswald remotely should be in this documentation website. Could we have a copy?

- From your explanation, I take it that `/tmp` isn't accessible directly by any users on any node? Would some HPC applications that assume its existance and that they can read/write files/directories in it have problems? Or can pre-installed apps access it?

- If nodes aren't exclusive, should users of `/local` use their own subdirectory (eg. `/local/bob`) to avoid filename collisions between multiple jobs running on the same node at the same time?
  - As an example: job A writes to `/local/file.out`; job B writes to `/local/file.out`; job A tries to read from `/local/file.out` -> not the data it expected (maybe crash?).

- Also, how are users expected to clear `/local` after use? Only delete the files they know they created, or wipe the drive? If the latter, the same issue with other jobs using the filesystem occurs:
  - As an example: job A writes to `/local/jobA.out`; job B writes to `/local/jobB.out`; job A finishes and wipes `/local/*`; job B tries to read from `/local/jobB.out` -> crash/failure.

- Re. specifying number of nodes required for a job:
  - Say a user had a job that required 80 tasks (eg. it's quite parallelisable, and doesn't take that long if it's highly parallelised). That should take no more than 3 full nodes (28 x 3 = 84). Say Oswald was busy, and didn't have that many full nodes available (for at least a few hours), but did have various partially-occupied nodes available (some cores were free). If that user specified the number of nodes they required was exactly 3, then SLURM couldn't allocate more than 3 nodes, so couldn't allocate their 80 tasks until 3 full nodes were free (which could be hours). However, if they didn't specify the number of nodes it required - only the number of tasks - then SLURM could allocate it across several partially-free nodes (whose running jobs had not made them exclusive) and complete the task much sooner, while avoiding wasting idle cores.
  - Is this a good enough reason to allow omitting the node count?
  - Also, in general, if a user's SLURM job configuration is valid and wouldn't adversely harm system performance, system stability, or other users, then is there any reason to restrict those configurations?

- What is the GPU node used for? Is it just a specialised compute node?
  - How would users specify to use it? By using the relevant --gpu* options to SLURM?

- What is the visualisation node used for?
  - If it's for running GUI apps, how would users go about running GUI apps on it? Via another chained SSH connection (your-computer [-> SSH-proxy] -> oswald-head -> visualisation-node)?

## Future Ideas

These are things to think about for the future.

- github organisation?
- moderation? - who? when? how?
  - depends on owner of github organisation that hosts repo

- google analytics?
  - stats about page popularity, etc.
  - management - who?

- use a university email as the sender? would the uni have to do anything?
  - see: https://mailchimp.com/help/limitations-of-free-email-addresses/
