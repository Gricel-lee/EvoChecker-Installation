# Evochecker - Virtual Machine
Virtual Machine (Ubuntu 64bits) with Evochecker configured and loaded with SafeSCAD.

- Download Virtual Machine from*: https://1drv.ms/u/s!AuG9Dok_F1SMiekevNw29ZE18knqYg?e=RniyXT
- The virtual machine (VM) was run using **VMWare Workstatio 16 Player** (free licence), configured to:

![image](https://user-images.githubusercontent.com/63869574/128170861-d50f6603-d6e2-407e-bfe9-4b5c43881dd7.png)

- Once the VM is turn on, to unlock enter the **Password**: 123456

![image](https://user-images.githubusercontent.com/63869574/128170250-eda2529f-be47-4a0f-9323-b1b7730eb53f.png)

*(download all files in a folder, and select it on VMWare as the VM)

## Run Evochecker
For more information about Evochecker, go to [1].


### A- Run Evochecker

1) Launch Eclipse (shortcut available on Desktop) and select
   workspace: /home/evochecker/Desktop/Eclipse-EvoChecker
   
2) Run evochecker from a main file:

   - **from a different java project:**
   On the Package Explorer, go to RunModel > com.sys > RunEvoTest.java >
   Right Click > Run As > Java Application.
	
   - **from evochecker project:**
   On the Package Explorer, go to Evochecker > src/main/java >
   Main.java > Right Click > Run As > Java Application

### B- Change configuration

1) On the Package Explorer, go to Evochecker > config.properties (below "target" folder)
2) Here you can change the model and properties files: 
     - MODEL_TEMPLATE_FILE = ...
     - PROPERTIES_FILE = ...
     
   the population size:
     - POPULATION_SIZE = ...
     
   the maximum number of evaluations:
     - MAX_EVALUATIONS = ...
     
   among other parameters.
   
  It comes pre-configured to run **SafeSCAD** model, as presented on [2] and discussed in [3]. Models and properties files are saved in the "models" folder and selected by the "MODEL_TEMPLATE_FILE" and "PROPERTIES_FILE" parameters, as mentioned before.


## References
[1] https://www-users.cs.york.ac.uk/~simos/EvoChecker/

[2] Calinescu, R. Alasmari, N., and Gleirscher, M. "Maintaining driver attentiveness in shared-control autonomous driving" presented at 2021 International Symposium on Software Engineering for Adaptive and Self-Managing Systems (SEAMS).

[3] https://www.york.ac.uk/assuring-autonomy/projects/safe-scad/
