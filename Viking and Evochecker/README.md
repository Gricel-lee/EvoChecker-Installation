# Running Evochecker from Viking

## Set up

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
