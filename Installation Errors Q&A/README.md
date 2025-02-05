# INSTALLING EVOCHECKER DIRECTLY TO YOUR PC. Common Problems And Solutions.
Currently, Evochecker is available for macOS and Linux.
It can be download at: https://github.com/gerasimou/EvoChecker

The next section has some of the problems found in the installation of the software, as well as their solution.



## - Error: "Module evochecker is not accessible"

### Solution
In the java project where you are calling Evochecker, do not create (or delete) the **module-info.java** file.

## - Error: cannot import EvoChecker library.

![image](https://user-images.githubusercontent.com/63869574/128541873-ccb0f642-6923-4cd0-9c3f-e96bb1df9cf5.png)

### Solution
Right click on the project from where you're calling EvoChecker, go to Build Path > Configure Build Path.

![image](https://user-images.githubusercontent.com/63869574/128542353-a00d6ca4-7650-4b14-88f6-3eec01cc4b94.png)

In the **Projects** tab, add Evochecker project into **Classpath**:

![image](https://user-images.githubusercontent.com/63869574/128542762-c3ad5e95-9f1b-4f2d-8d97-8bc1a60cdff3.png)

Note: Do not get confuse adding it into the **Libraries** instead of **Projects** tab.

If Evochecker is called from another project, make sure to add **evochecker.** when calling the library. All the options from the module should be now available:

![image](https://user-images.githubusercontent.com/63869574/128543214-5e18bf04-b32c-4e4a-985b-ba364745ca6a.png)


## - Error 5: LD_LIBRARY_PATH has not been specifie, and
## - Error: java.lang.UnsatisfiedLinkError: no prism in java.library.path:
![image](https://user-images.githubusercontent.com/63869574/128391061-32caa09a-e9e9-4c17-baa5-0d6a8a576637.png)


### Solution
Select the run file from the **Package Explorer** (on the left). Right click > Run Configuration > Add in the Environment tab the 
- For IOs:
  -  DYLD_LIBRARY_PATH = libs/runtime
-  Linux:
   -  LD_LIBRARY_PATH = libs/runtime

![image](https://user-images.githubusercontent.com/63869574/128394099-9837da0a-80f9-489a-83b2-417c9dd2a5e2.png)

Note: Make sure you add the Variable to the file from where Evochecker is called.

## - Error 5: LD_LIBRARY_PATH "is not recognized (or similar)".
### Solution
Change the Java project to the eclipse-workspace file, this may solve the problem.


## - Error: Path null is a directoryjava.io.FileNotFoundException: resources/config.properties (No such file or directory)

![image](https://user-images.githubusercontent.com/63869574/128543784-ae9fe7a9-a193-4eb6-aeea-cac366d5818e.png)


### Solution
Copy the config.properties to a folder called resources in the project you're calling Evochecker (the one in the Evochecker project can be deleted to avoid confusion). 


## - Error: java.io.IOException: File does not exists! /home/.../models/modelName.pm

![image](https://user-images.githubusercontent.com/63869574/128531880-8fdfcaa7-2f07-4e04-9895-fb2cc2b06066.png)

### Solution
Copy the folder and files to the path it shows, in this example, the folder with the **models** must be copied to the Java project from which Evochecker is called.
In this example, from multi_robot_sys_01 project:

![image](https://user-images.githubusercontent.com/63869574/128532776-3c41defc-8e13-4240-8d67-2e39ba5f647a.png)


## - Error: LD_LIBRARY_PATH has not been specified. On Eclipse: Run > ... > Variable: LD_LIBRARU_PATH; Value: libs/runtimeModel Checking engine...

![image](https://user-images.githubusercontent.com/63869574/128548246-42f45150-6276-4ab2-9050-37a32ab06efc.png)

### Solution
You must copy the **lib** folder into the (java) project from where Evochecker is called:

![image](https://user-images.githubusercontent.com/63869574/128549544-9a663dff-afd4-4977-b457-68e686761e2a.png)


Note: This lib folder contains:

![image](https://user-images.githubusercontent.com/63869574/128549473-19b6f7c4-9732-43c6-9a3f-9efb64f84b16.png)



## - Error: Build path specifies execution environment JavaSE-11. There are no JRE installed…

![image](https://user-images.githubusercontent.com/63869574/128539055-6327a1fa-13c1-48fa-816e-d9942a582299.png)

### Solution

Open **Java Build Path** of the Evochecker project:

![image](https://user-images.githubusercontent.com/63869574/128539518-02bf12a9-1915-4cb5-bcb7-edcf2a8edd48.png)

Select another JRE version, in my case it worked with **Alternative JRE: jre**.

![image](https://user-images.githubusercontent.com/63869574/128539965-b377f0a4-4115-4feb-ac69-a16dcaa4e3ca.png)

Note: It may require cleaning the project on the tab **Project > Clean**.

![image](https://user-images.githubusercontent.com/63869574/128541153-da773398-d6ae-4ed5-a706-e058a1ad4f5b.png)

And refresh:

![image](https://user-images.githubusercontent.com/63869574/128541230-c858fac8-7646-4321-a9ba-164cb79f0668.png)


## - Error: Cannot run program "/usr/local/bin/python3": error 2, No such file or directory

![image](https://user-images.githubusercontent.com/63869574/128546194-093a79dd-8079-49af-affb-cfe744553ad6.png)

### Solution
Find the path to python, for example, in Linux:

![image](https://user-images.githubusercontent.com/63869574/128546444-a526a081-696f-4ed1-b276-f38ddbc7c5a0.png)

Change this path in PYTHON3_DIRECTORY in the config.properties file:

![image](https://user-images.githubusercontent.com/63869574/128546679-28fa7e82-69a3-4e5e-b587-2bd9cabb90fd.png)


## - Error 13: Cannot run program “/urs/lib/python”: error=13, Permission denied

Evochecker is configured properly, it evolves and generates the results, but it does not show any graph and error 13 appears:

![image](https://user-images.githubusercontent.com/63869574/128369738-42852e64-b3d4-4a5d-a78c-6608b5d475aa.png)
### Solution
If this error appears, open the config.properties file, and change PYTHON3_DIRECTORY to the command to run python (in my case, "python3.8")

![image](https://user-images.githubusercontent.com/63869574/128370078-311fad50-950a-4c3b-92b3-fb6a71344adc.png)

Note: Open CMD or terminal and type python3 (or python), if configure properly, it should show the python version, e.g., for 3.7.9:

![image](https://user-images.githubusercontent.com/63869574/128370975-d370028c-7856-439a-be97-8adb61695379.png)


## - Error: [Traceback (most recent call last):,   File "scripts/plotFront3D.py", line 3, in <module>,     import pandas as pd , ModuleNotFoundError: No module named 'pandas']

If pandas in not install:
  
![image](https://user-images.githubusercontent.com/63869574/128372707-368d5ec1-6ec4-43a2-85de-71d61503c6e9.png)

### Solution
Install pandas from the CMD or terminal, e.g., for Ubuntu:
  sudo apt-get install python3-pandas -y
  
  ![image](https://user-images.githubusercontent.com/63869574/128373066-4f2b80c0-cb92-4b86-9f0b-f7bcd2d1950a.png)

  Note: Make use you install it in the correct python version (it may be: sudo apt-get install **python**-pandas -y)
  
 

## - Error: /usr/bin/python3: can't open file 'scripts/plotFront3D.py': [Error 2] No such file or directory
  ![image](https://user-images.githubusercontent.com/63869574/128545208-5a738952-a6ac-46e5-ae90-c1cfb877a16d.png)

  ### Solution
  This appears when the Evochecker is called from another (java) project, which does not have the python file plotFront3D.py. Temporarily, you can copy the folder 'scripts' into the (java) project and run it again. scripts folder contains:
  
![image](https://user-images.githubusercontent.com/63869574/130229656-aa192232-af13-4d52-b593-78dc30000528.png)


## - Error: Parses config file but stops after printing "Starting evolution"
![image](https://github.com/user-attachments/assets/0ba19fac-e520-46ba-bf07-1d6b5755a9d9)

 ### Solution
 Close Eclipse and open it again can solve this problem (even when ran from terminal/ .jar file).


  
