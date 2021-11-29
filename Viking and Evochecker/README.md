# Running Evochecker from Viking

## Setting up Viking

- Connect to the university Internet network. If you are outside of campus, make sure you are connected through a VPN using PulseSecure:

![image](https://user-images.githubusercontent.com/63869574/143794614-5e85dbfa-6508-4c03-abf8-943abbdada8f.png)

- Follow the **Terminal access from a UNIX/LINUX or MAC desktop** section on https://wiki.york.ac.uk/display/RCS/How+to+log+in+to+Viking 

- To access/copy/paste data, see https://wiki.york.ac.uk/display/RCS/Copying+your+data+to+and+from+Viking 

Copy and paste the following files from Evochecker into a "scratch" subfolder[^1] (only the Evochecker.sh file is created in the next section).

![image](https://user-images.githubusercontent.com/63869574/143893682-c9c60585-631c-458e-a8e8-7f3c72be841d.png)

### Change libs folder

- **Replace** the "runtime" subfolder in "libs" for an older version of PRISM provided here[^2]: https://github.com/Gricel-lee/VirtualMachine-Evochecker/tree/main/Viking%20and%20Evochecker/runtime

![image](https://user-images.githubusercontent.com/63869574/143893629-22d0e0fc-6248-4e3d-bf0f-2a6f2c6fc4a0.png)


## Run Evochecker
### Executable file to submit a job
It is recommendable to create a .sh file to submit a job to Viking. 
For Evochecker, we create an EvoChecker.sh file containing:

```
#!/bin/bash
#SBATCH --time=00:50:00 # Time limit hrs:min:sec
#SBATCH --mem=5000
#SBATCH --cpus-per-task=1
module load lang/Java/11.0.2
module load compiler/GCC/8.2.0-2.31.1
module load lang/Python/3.7.0-intel-2018b
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/users/USER/scratch/EvoCheckerViking/ScadV2/libs/runtime
export LD_LIBRARY_PATH
echo "$LD_LIBRARY_PATH"
java -jar EvoChecker.jar config.properties 

```
In LD_LIBRARY_PATH, **USER** is your Viking user; **scratch** is the design Viking folder to run files[^1]; **EvoCheckerViking/ScadV2/libs/runtime** is the path to the runtime folder, **config.properties** is the Evochecker properties file. 



### Run .sh file

- First, the .sh file must be executable so do: chmod u=rwx,g=r-x,o=r-x 

![image](https://user-images.githubusercontent.com/63869574/143779349-bcbdcc6f-2159-467e-bbf7-799542f215e2.png)

- Go to the scratch subfolder where all the Evochecker files are and run it[^3]. The next example is in Windows using PuTTY:

![image](https://user-images.githubusercontent.com/63869574/143894178-ab36e910-8cb0-4a2a-87c0-6e6295b57b84.png)



## Possible Errors
See section **Change libs folder** if you get a file saying:
```
Accepting from port: 8888
java.lang.UnsatisfiedLinkError: /mnt/lustre/users/gnvf500/EvoCheckerViking/ScadV2/libs/runtime/libprism.so: /lib64/libstdc++.so.6: version `CXXABI_1.3.8' not found (required by /mnt/lustre/users/gnvf500/EvoCheckerViking/ScadV2/libs/runtime/libprism.so)
```


[^1]: See _IMPORTANT - Run your jobs from the high performance_ section at https://wiki.york.ac.uk/display/RCS/VK1%29+How+to+access+Viking

[^2]: This is neccesary as the default compiler in Viking is an old version (4.8.5), and forcing Viking to use the "libs/runtime" libraries does not seem to work. "However, to work around this, \[download\] prism version 4.6 and \[...\] replace the prism libraries in the runtime folder", Emad Alharbi. 

[^3]: You can also use "**sbatch** EvoChecker.sh" to sumit a job to Viking. Not tested for Evochecker yet.
