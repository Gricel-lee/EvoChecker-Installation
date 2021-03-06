# Running Evochecker from Viking

## Set up Viking

- Connect to the university Internet network. If you are outside of campus, make sure you are connected through a VPN using PulseSecure:

![image](https://user-images.githubusercontent.com/63869574/143794614-5e85dbfa-6508-4c03-abf8-943abbdada8f.png)

- Follow the **Terminal access from a UNIX/LINUX or MAC desktop** section on https://wiki.york.ac.uk/display/RCS/How+to+log+in+to+Viking 

- To access/copy/paste data, see https://wiki.york.ac.uk/display/RCS/Copying+your+data+to+and+from+Viking 

Copy and paste the following files from Evochecker into a "scratch" subfolder[^1] (EvoChecker.jar is available here, and Evochecker.sh is created in the next section).

![image](https://user-images.githubusercontent.com/63869574/143893682-c9c60585-631c-458e-a8e8-7f3c72be841d.png)

### Change libs folder

- **Replace** the "runtime" subfolder in "libs" for an older version of PRISM provided here[^2]: https://github.com/Gricel-lee/VirtualMachine-Evochecker/tree/main/Viking%20and%20Evochecker/runtime

![image](https://user-images.githubusercontent.com/63869574/143893629-22d0e0fc-6248-4e3d-bf0f-2a6f2c6fc4a0.png)



## Submit an Evochecker job

### Executable .sh file

A .sh file is needed to submit a job to Viking. We create **EvoChecker.sh** containing:

```
#!/bin/bash
#SBATCH --job-name=SafeScad             # Job name use for sending an email and print cmd info
#SBATCH --mail-type=BEGIN,END,FAIL      # Mail events (NONE, BEGIN, END, FAIL, ALL)
#SBATCH --mail-user=youruser@email.com  # Where to send mail
#SBATCH --time=48:00:00                 # Time limit hrs:min:sec (up to 48hr in default nodes)
#SBATCH --mem=5gb                       #Up to 370gb aprox. in default nodes
#SBATCH --cpus-per-task=1               # cpus required (1-15 tested)
module load lang/Java/11.0.2
module load compiler/GCC/9.3.0
module load lang/Python/3.7.0-intel-2018b
export LD_LIBRARY_PATH="/users/USER/scratch/EvoCheckerViking/SafeScadV2/libs/runtime/:$LD_LIBRARY_PATH" #path
export LD_LIBRARY_PATH="/users/USER/scratch/EvoCheckerViking/SafeScadV2/libs/:$LD_LIBRARY_PATH"         #path

echo "$LD_LIBRARY_PATH"
java -jar EvoChecker.jar config.properties
# Other comment out configurations for easier run: #<-------
#java -jar EvoChecker.jar safeSCAD-both-verified-DNNconfig.properties
#java -jar EvoChecker.jar safeSCAD-v1-verified-DNNconfig.properties 
#java -jar EvoChecker.jar safeSCAD-v2-verified-DNNconfig.properties 
#java -jar EvoChecker.jar safeSCAD-with-non-verified-DNNconfig.properties 
#java -jar EvoChecker.jar SafeSCAD-no-DNNconfig.properties
```

In LD_LIBRARY_PATH, **USER** is your Viking user; **scratch** is the design Viking folder to run files[^1] (you MUST use this folder); **EvoCheckerViking/ScadV2/libs/runtime** is the path to the runtime folder, **config.properties** is the Evochecker properties file. 

You can modify the batch parameters if needed (https://wiki.york.ac.uk/display/RCS/Physnodes+-+3%29+Submitting+Jobs+to+the+physics+cluster)

![image](https://user-images.githubusercontent.com/63869574/155792200-b1a3b7ab-8698-432c-be37-7d53a6c40129.png)

You can also add more config.properties files with different parameters. In the example, I added them commented out.


### Run .sh file

First, the .sh file must be executable so do: chmod u=rwx,g=r-x,o=r-x 

![image](https://user-images.githubusercontent.com/63869574/143779349-bcbdcc6f-2159-467e-bbf7-799542f215e2.png)

Go to the scratch subfolder where all the Evochecker files are and run it[^3]

You can use: [^5]
 - ```sbatch EvoChecker.sh``` to sumbit the job to Viking (you can close your session if needed, e.g., PuTTY session closed in Windows)
 - ```.\Evochecker.sh ``` to run the job (cancelled if session ends, e.g., PuTTY session closed in Windows)
 - ```scancel jobID``` to cancel a job 
 - ```scancel -u user``` to cancel all jobs
 - ```sacct``` to check your submitted jobs
 - or ```qstat -u user```
 - or ```squeue --user=user``` (get code if something failed,column "NODELIST (REASON)")
 - or ```squeue --start -u user``` (get the expected time to start job)
 - or ```sacct -u user --format=User,JobID,Jobname,partition,state,time,start,end,elapsed,averss,MaxRss,MaxVMSize,nnodes,ncpus,nodelist```
![image](https://user-images.githubusercontent.com/63869574/155799924-657672e7-5e3e-4526-bf05-4fdf6d8bb5d0.png)

If more than 48hr is require, you can change the default partition: https://wiki.york.ac.uk/display/RCS/VK12%29+Available+Resource+Partitions+and+their+limits

![image](https://user-images.githubusercontent.com/63869574/156606835-cf3fe128-7717-4ab4-9de8-e798cbca9c58.png)



# Possible Errors

### Accepting from port: 8888. java.lang.UnsatisfiedLinkError

See section **Change libs folder** if you get a file saying:
```
Accepting from port: 8888
java.lang.UnsatisfiedLinkError: /mnt/lustre/users/USER/EvoCheckerViking/ScadV2/libs/runtime/libprism.so: /lib64/libstdc++.so.6: version `CXXABI_1.3.8' not found (required by /mnt/lustre/users/USER/EvoCheckerViking/ScadV2/libs/runtime/libprism.so)
```

### Submitted but not running [^5]
Sometimes when a file is submitted, it may not run. Check **squeue --user=user**, column "NODELIST (REASON)"  will display a reason code if your job is being held.
In this example, the only job that is going to be executed is the one with "priority" on the last column. Meaning that it hasn't been schedule given that other jobs are in the queue before with higher priority. The rest of the jobs must be cancelled as they require computing resources that Viking cluster does not have.

![image](https://user-images.githubusercontent.com/63869574/156643316-f4573432-588e-40ad-8c6d-c1e560103580.png)

Check also [^5]:
_If your job has the start time of N/A and/or the REASON column state PartitionConfig, then you probably have requested resources that are not available on the cluster. In the above example job 36 has requested more CPUs than are available for jobs in the cluster._

### Run out of memory
You may need to select a node with bigger memory [^6]. Add ```#SBATCH --partition=himem```.
Make sure you add it before executing the code or it won't be run.

```
#!/bin/bash

#SBATCH --job-name=SafeScad             # Job name use for sending an email and print cmd info
#SBATCH --partition=himem               #<-------
#SBATCH --mail-type=BEGIN,END,FAIL      # Mail events (NONE, BEGIN, END, FAIL, ALL)
#SBATCH --mail-user=youruser@email.com  # Where to send mail
#SBATCH --time=48:00:00                 # Time limit hrs:min:sec (up to 48hr in default nodes)
#SBATCH --mem=1TB                       #<-------
#SBATCH --cpus-per-task=15              # cpus required (1-15 tested)
module load lang/Java/11.0.2
module load compiler/GCC/9.3.0
module load lang/Python/3.7.0-intel-2018b
export LD_LIBRARY_PATH="/users/USER/scratch/EvoCheckerViking/V2ExtraTime/SafeScadV2/libs/runtime/:$LD_LIBRARY_PATH"
export LD_LIBRARY_PATH="/users/USER/scratch/EvoCheckerViking/V2ExtraTime/SafeScadV2/libs/:$LD_LIBRARY_PATH"

echo "$LD_LIBRARY_PATH"

java -jar EvoChecker.jar safeSCAD-both-verified-DNNconfig.properties
```

### Run out of time
As before, you may need to select a node with bigger memory [^6]. Ad
d ```#SBATCH --partition=week```.
Make sure you add it before executing the code or it won't be run.	

## More about Vikings
### Script template [^4]

![image](https://user-images.githubusercontent.com/63869574/148259168-fbf62be9-ab8d-472e-9135-68956205448d.png)

### Managing time [^4]
"#SBATCH --time=02:00:00" 
### Controlling memory [^4]
"#SBATCH --mem=1gb"



[^1]: See _IMPORTANT - Run your jobs from the high performance_ section at https://wiki.york.ac.uk/display/RCS/VK1%29+How+to+access+Viking

[^2]: This is neccesary as the default compiler in Viking is an old version (4.8.5), and forcing Viking to use the "libs/runtime" libraries does not seem to work. "However, to work around this, \[download\] prism version 4.6 and \[...\] replace the prism libraries in the runtime folder", Emad Alharbi. 

[^3]: Not tested for Evochecker yet.

[^4]: https://wiki.york.ac.uk/display/RCS/VK4%29+Job+script+configuration

[^5]: https://wiki.york.ac.uk/display/RCS/VK3%29+Submitting+Jobs+to+Viking

[^6]: https://wiki.york.ac.uk/display/RCS/VK12%29+Available+Resource+Partitions+and+their+limits
