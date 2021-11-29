# Running Evochecker from Viking

## Set up

## Executable file
You must create an EvoChecker.sh file with the following:

```
#!/bin/bash
#SBATCH --time=00:40:00 # Time limit hrs:min:sec
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
where _
--time_
For LD_LIBRARY_PATH, _USER_ is your Viking user, _scratch_ is the design Viking folder to run files, _EvoCheckerViking/ScadV2/libs/runtime_ is the path to the runtime folder, _config.properties_ is the Evochecker properties file. 


## Run file

- First, the .sh file must be executable so do: chmod u=rwx,g=r-x,o=r-x 

![image](https://user-images.githubusercontent.com/63869574/143779349-bcbdcc6f-2159-467e-bbf7-799542f215e2.png)

- To run the shell file, use **sbatch** fileName.sh

## Error
If you get a file saying 
```
Accepting from port: 8888
java.lang.UnsatisfiedLinkError: /mnt/lustre/users/gnvf500/EvoCheckerViking/ScadV2/libs/runtime/libprism.so: /lib64/libstdc++.so.6: version `CXXABI_1.3.8' not found (required by /mnt/lustre/users/gnvf500/EvoCheckerViking/ScadV2/libs/runtime/libprism.so)
```

??

