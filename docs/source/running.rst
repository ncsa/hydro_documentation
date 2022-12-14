.. _running:

Running 
==================

.. _slurm:

Running Batch Jobs (Slurm)
----------------------------

User access to the compute nodes for running jobs is available via a
batch job. Hydro uses the `Slurm Workload
Manager <https://slurm.schedmd.com/overview.html>`__ for running batch
jobs. See the sbatch section for details on batch job submission.

Please be aware that the interactive nodes are a shared resource for all
users of the system and their use should be limited to editing,
compiling and building your programs, and for short non-intensive runs.


An interactive batch job provides a way to get interactive access to a
compute node via a batch job. See the srun or salloc section for
information on how to run an interactive job on the compute nodes. Also,
a very short time *test* queue provides quick turnaround time for
debugging purposes.

To ensure the health of the batch system and scheduler users should
refrain from having more than 1,000 batch jobs in the queues at any one
time.

There is currently 1 partition/queue named normal. The normal
partition's default wallclock time is 4 hours with a limit of 7 days.
Compute nodes are not shared between users.

sbatch
~~~~~~

Batch jobs are submitted through a *job script* using the sbatch
command. Job scripts generally start with a series of SLURM *directives*
that describe requirements of the job such as number of nodes, wall time
required, etc… to the batch system/scheduler (SLURM directives can also
be specified as options on the sbatch command line; command line options
take precedence over those in the script). The rest of the batch script
consists of user commands.

The syntax for sbatch is:

sbatch [list of sbatch options] script_name

The main sbatch options are listed below. Refer to the sbatch man page
for options.

-  | The common resource_names are:
   | --time=\ *time*

   time=maximum wall clock time (d-hh:mm:ss) *[default: maximum limit of
   the queue(partition) submittied to]*

   --nodes=\ *n*

   --ntasks=\ *p* Total number of cores for the batch job

   --ntasks-per-node=\ *p* Number of cores per node (same as ppn under
   PBS)

   | n=number of 16-core nodes *[default: 1 node]*
   | p=how many cores(ntasks) per job or per node(ntasks-per-node) to
     use (1 through 16) *[default: 1 core]*

   | Examples:
   | --time=00:30:00
   | --nodes=2
   | --ntasks=32
   | or
   | --time=00:30:00
   | --nodes=2
   | --ntasks-per-node=16

   **Memory needs:** The compute nodes have 256GB.

   | Example:
   | --time=00:30:00
   | --nodes=2
   | --ntask=32
   | --mem=118000
   | or
   | --time=00:30:00
   | --nodes=2
   | --ntasks-per-node=16
   | --mem-per-cpu=7375

Useful Batch Job Environment Variables

+-----------------+---------------------+-----------------+-----------------+
| Description     | SLURM               | Detail          | | PBS           |
|                 | Environment         | Description     |   Environment   |
|                 | Variable            |                 |   Variable      |
|                 |                     |                 | | *(no longer   |
|                 |                     |                 |   valid)*       |
+=================+=====================+=================+=================+
| JobID           | $SLURM_JOB_ID       | Job identifier  | $PBS_JOBID      |
|                 |                     | assigned to the |                 |
|                 |                     | job             |                 |
+-----------------+---------------------+-----------------+-----------------+
| Job Submission  | $S                  | By default,     | $PBS_O_WORKDIR  |
| Directory       | LURM_SUBMIT_DIR.    | jobs start in   |                 |
|                 |                     | the directory   |                 |
|                 |                     | the job was     |                 |
|                 |                     | submitted from. |                 |
|                 |                     | So the cd       |                 |
|                 |                     | $S              |                 |
|                 |                     | LURM_SUBMIT_DIR |                 |
|                 |                     | command is not  |                 |
|                 |                     | needed.         |                 |
+-----------------+---------------------+-----------------+-----------------+
| Machine(node)   | $SLURM_NODELIST     | variable name   | $PBS_NODEFILE   |
| list            |                     | that containins |                 |
|                 |                     | the list of     |                 |
|                 |                     | nodes assigned  |                 |
|                 |                     | to the batch    |                 |
|                 |                     | job             |                 |
+-----------------+---------------------+-----------------+-----------------+
| Array JobID     | $SLU                | each member of  | $PBS_ARRAYID    |
|                 | RM_ARRAY_JOB_ID.    | a job array is  |                 |
|                 | $SLUR               | assigned a      |                 |
|                 | M_ARRAY_TASK_ID.    | unique          |                 |
|                 |                     | identifier (see |                 |
|                 |                     | the `Job        |                 |
|                 |                     | Arrays <        |                 |
|                 |                     | https://campusc |                 |
|                 |                     | luster.illinois |                 |
|                 |                     | .edu/resources/ |                 |
|                 |                     | docs/user-guide |                 |
|                 |                     | /#jobarrays>`__ |                 |
|                 |                     | section)        |                 |
+-----------------+---------------------+-----------------+-----------------+

.. _sample-batch-script:

Here is a sample Batch script:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:: 
   
   #!/bin/bash
   ### set the wallclock time
   #SBATCH --time=00:30:00

   ### set the number of nodes, tasks per node, and cpus per task for the job
   #SBATCH --nodes=3
   #SBATCH --ntasks-per-node=1
   #SBATCH --cpus-per-task=16

   ### set the job name
   #SBATCH --job-name="hello"

   ### set a file name for the stdout and stderr from the job
   ### the %j parameter will be replaced with the job ID.
   ### By default, stderr and stdout both go to the --output
   ### file, but you can optionally specify a --error file to
   ### keep them separate
   #SBATCH --output=hello.o%j
   ##SBATCH --error=hello.e%j

   ### set email notification
   ##SBATCH --mail-type=BEGIN,END,FAIL
   ##SBATCH --mail-user=username@host

   ### In case of multiple allocations, select which one to charge
   ##SBATCH --account=xyz

   ### For OpenMP jobs, set OMP_NUM_THREADS to the number of
   ### cpus per task for the job step
   export OMP_NUM_THREADS=4

   ## Use srun to run the job on the requested resources. You can change --ntasks-per-node and
   ## --cpus-per-task, as long as --cpus-per-task does not exceed the number requested in the
   ## sbatch parameters
   srun --ntasks=12 --ntasks-per-node=4 --cpus-per-task=4 ./hellope



See the sbatch man page for additional environment variables available.

srun
~~~~~~

The srun command initiates an interactive job on the compute nodes.

For example, the following command:

``srun --time=00:30:00 --nodes=1 --ntasks-per-node=16 --pty /bin/bash``

will run an interactive job in the ncsa queue with a wall clock limit of
30 minutes, using one node and 16 cores per node. You can also use other
sbatch options such as those documented above.

After you enter the command, you will have to wait for SLURM to start
the job. As with any job, your interactive job will wait in the queue
until the specified number of nodes is available. If you specify a small
number of nodes for smaller amounts of time, the wait should be shorter
because your job will backfill among larger jobs. You will see something
like this:

``srun: job 123456 queued and waiting for resources``

Once the job starts, you will see:

``srun: job 123456 has been allocated resources``

and will be presented with an interactive shell prompt on the launch
node. At this point, you can use the appropriate command to start your
program.

When you are done with your runs, you can use the exit command to end
the job.

scancel
~~~~~~~~~~~~~~~~~

The scancel command deletes a queued job or kills a running job.

-  scancel JobID deletes/kills a job.

Job Dependencies
~~~~~~~~~~~~~~~~~~~

Job dependencies allow users to set execution order in which their
queued jobs run. Job dependencies are set by using the ??dependency
option with the syntax being ??dependency=<dependency type>:<JobID>.
SLURM places the jobs in *Hold* state until they are eligible to run.

The following are examples on how to specify job dependencies using the
afterany dependency type, which indicates to SLURM that the dependent
job should become eligible to start only after the specified job has
completed.

On the command line:

``sbatch --dependency=afterany:<JobID> jobscript.pbs``

In a job script:

::

   #!/bin/bash
   #SBATCH --time=00:30:00
   #SBATCH --nodes=1
   #SBATCH --ntasks-per-node=16
   #SBATCH --job-name="myjob"
   #SBATCH --output=myjob.o%j
   #SBATCH --dependency=afterany:<JobID>

In a shell script that submits batch jobs:

::

   #!/bin/bash
   JOB_01=`sbatch jobscript1.sbatch |cut -f 4 -d " "`
   JOB_02=`sbatch --dependency=afterany:$JOB_01 jobscript2.sbatch |cut -f 4 -d " "`
   JOB_03=`sbatch --dependency=afterany:$JOB_02 jobscript3.sbatch |cut -f 4 -d " "`
   ...

**Note:** Generally the recommended dependency types to use are after,
afterany, afternotok and afterok. While there are additional dependency
types, those types that work based on batch job error codes may not
behave as expected because of the difference between a batch job error
and application errors. See the dependency section of the sbatch manual
page for additional information (man sbatch).

Job Arrays
~~~~~~~~~~~~

If a need arises to submit the same job to the batch system multiple
times, instead of issuing one sbatch command for each individual job,
users can submit a job array. Job arrays allow users to submit multiple
jobs with a single job script using the ??array option to sbatch. An
optional slot limit can be specified to limit the amount of jobs that
can run concurrently in the job array. See the sbatch manual page for
details (man sbatch). The file names for the input, output, etc. can be
varied for each job using the job array index value defined by the SLURM
environment variable SLURM_ARRAY_TASK_ID.

A sample batch script that makes use of job arrays is available in
/projects/consult/slurm/jobarray.sbatch.

**Notes:**

-  | Valid specifications for job arrays are
   | --array 1-10
   | --array 1,2,6-10
   | --array 8
   | --array 1-100%5 (a limit of 5 jobs can run concurrently)

   ::

       

-  You should limit the number of batch jobs in the queues at any one
   time to 1,000 or less. (Each job within a job array is counted as one
   batch job.)

-  Interactive batch jobs are not supported with job array submissions.

-  For job arrays, use of any environment variables relating to the
   JobID (e.g., PBS_JOBID) must be enclosed in double quotes.

-  To delete job arrays, see the
   `scancel <https://slurm.schedmd.com/job_array.html#scancel>`__
   command section.

Translating PBS Scripts to Slurm Scripts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following table contains a list of common commands and terms used
with the TORQUE/PBS scheduler, and the corresponding commands and terms
used under the `Slurm scheduler <https://www.msi.umn.edu/slurm>`__. This
sheet can be used to assist in translating your existing PBS scripts
into Slurm scripts to be read by the new scheduler, or as a reference
when creating new Slurm job scripts.

User Commands
$$$$$$$$$$$$$$$

+----------------------+----------------------+---------------------------------+
| **User Commands**    | **PBS/Torque**       | **Slurm**                       |
+======================+======================+=================================+
| Job submission       | qsub [script_file]   | sbatch [script_file]            |
+----------------------+----------------------+---------------------------------+
| Job deletion         | qdel [job_id]        | scancel [job_id]                |
+----------------------+----------------------+---------------------------------+
| Job status (by job)  | qstat [job_id]       | squeue [job_id]                 |
+----------------------+----------------------+---------------------------------+
| Job status (by user) | qstat -u [user_name] | squeue -u [user_name]           |
+----------------------+----------------------+---------------------------------+
| Job hold             | qhold [job_id]       | scontrol hold [job_id]          |
+----------------------+----------------------+---------------------------------+
| Job release          | qrls [job_id]        | scontrol release [job_id]       |
+----------------------+----------------------+---------------------------------+
| Queue list           | qstat -Q             | squeue                          |
+----------------------+----------------------+---------------------------------+
| Node list            | pbsnodes -l          | sinfo -N OR scontrol show nodes |
+----------------------+----------------------+---------------------------------+
| Cluster status       | qstat -a             | sinfo                           |
+----------------------+----------------------+---------------------------------+

Environment
$$$$$$$$$$$$

================ ============== ====================
**Environment**  **PBS/Torque** **Slurm**
================ ============== ====================
Job ID           $PBS_JOBID     $SLURM_JOBID
Submit Directory $PBS_O_WORKDIR $SLURM_SUBMIT_DIR
Submit Host      $PBS_O_HOST    $SLURM_SUBMIT_HOST
Node List        $PBS_NODEFILE  $SLURM_JOB_NODELIST
Q                $PBS_ARRAYID   $SLURM_ARRAY_TASK_ID
================ ============== ====================

Job Specifications
$$$$$$$$$$$$$$$$$$$$$$

+----------------------+----------------------+----------------------+
| **Job                | **PBS/Torque**       | **Slurm**            |
| Specification**      |                      |                      |
+======================+======================+======================+
| Script directive     | #PBS                 | #SBATCH              |
+----------------------+----------------------+----------------------+
| Queue/Partition      | -q [name]            | -p [name] **\*Best   |
|                      |                      | to let Slurm pick    |
|                      |                      | the optimal          |
|                      |                      | partition**          |
+----------------------+----------------------+----------------------+
| Node Count           | -l nodes=[count]     | -N [min[-max]]       |
|                      |                      | **\*Autocalculates   |
|                      |                      | this if just task #  |
|                      |                      | is given**           |
+----------------------+----------------------+----------------------+
| Total Task Count     | -l ppn=[count] OR -l | -n OR                |
|                      | mppwidth=[PE_count]  | --ntasks=ntasks      |
+----------------------+----------------------+----------------------+
| Wall Clock Limit     | -l                   | -t [min] OR -t       |
|                      | walltime=[hh:mm:ss]  | [days-hh:mm:ss]      |
+----------------------+----------------------+----------------------+
| Standard Output File | -o [file_name]       | -o [file_name]       |
+----------------------+----------------------+----------------------+
| Standard Error File  | -e [file_name]       | -e [file_name]       |
+----------------------+----------------------+----------------------+
| Combine stdout/err   | -j oe (both to       | (use -o without -e)  |
|                      | stdout) OR -j eo     |                      |
|                      | (both to stderr)     |                      |
+----------------------+----------------------+----------------------+
| Copy Environment     | -V                   | --export=[ALL \|     |
|                      |                      | NONE \| variables]   |
+----------------------+----------------------+----------------------+
| Event Notification   | -m abe               | --mail-type=[events] |
+----------------------+----------------------+----------------------+
| Email Address        | -M [address]         | -                    |
|                      |                      | -mail-user=[address] |
+----------------------+----------------------+----------------------+
| Job Name             | -N [name]            | --job-name=[name]    |
+----------------------+----------------------+----------------------+
| Job Restart          | -r [y \| n]          | --requeue OR         |
|                      |                      | --no-requeue         |
+----------------------+----------------------+----------------------+
| Resource Sharing     | -l                   | --exclusive OR       |
|                      | nac                  | --shared             |
|                      | cesspolicy=singlejob |                      |
+----------------------+----------------------+----------------------+
| Memory Size          | -l mem=[MB]          | --mem=[mem][M \| G   |
|                      |                      | \| T] OR             |
|                      |                      | -                    |
|                      |                      | -mem-per-cpu=[mem][M |
|                      |                      | \| G \| T]           |
+----------------------+----------------------+----------------------+
| Accounts to charge   | -A OR -W             | --account=[account]  |
|                      | group_list=[account] | OR -A                |
+----------------------+----------------------+----------------------+
| Tasks Per Node       | -l mppnppn           | --ta                 |
|                      | [PEs_per_node]       | sks-per-node=[count] |
+----------------------+----------------------+----------------------+
| CPUs Per Task        |                      | --c                  |
|                      |                      | pus-per-task=[count] |
+----------------------+----------------------+----------------------+
| Job Dependency       | -d [job_id]          | --d                  |
|                      |                      | epend=[state:job_id] |
+----------------------+----------------------+----------------------+
| Quality of Service   | -l qos=[name]        | --qos=[normal \|     |
|                      |                      | high]                |
+----------------------+----------------------+----------------------+
| Job Arrays           | -t [array_spec]      | --array=[array_spec] |
+----------------------+----------------------+----------------------+
| Generic Resources    | -l                   | --                   |
|                      | o                    | gres=[resource_spec] |
|                      | ther=[resource_spec] |                      |
+----------------------+----------------------+----------------------+
| Job Enqueue Time     | -a “YYYY-MM-DD       | --begin=YYY          |
|                      | HH:MM:SS”            | Y-MM-DD[THH:MM[:SS]] |
+----------------------+----------------------+----------------------+

Notebooks
-------------
