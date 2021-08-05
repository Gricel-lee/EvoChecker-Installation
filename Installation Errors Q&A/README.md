# Common Problems And Solutions in the Deployment of EvoChecker

## - Error: Error 5: LD_LIBRARY_PATH has not been specified.
![image](https://user-images.githubusercontent.com/63869574/128391061-32caa09a-e9e9-4c17-baa5-0d6a8a576637.png)


### Solution
Select the run file from the **Package Explorer** (on the left). Right click > Run Configuration > Add in the Environment tab the 
- For IOs:
  -  DYLD_LIBRARY_PATH = libs/runtime
-  Linux:
   -  LD_LIBRARY_PATH = libs/runtime

![image](https://user-images.githubusercontent.com/63869574/128394099-9837da0a-80f9-489a-83b2-417c9dd2a5e2.png)

Note: Make sure you add the Variable to the file from where Evochecker is called.

## - Error: Cannot run program “/urs/lib/python”: error=13, Permission denied

Evochecker is configured properly, it evolves and generates the results, but it does not show any graph and error 13 appears:

![image](https://user-images.githubusercontent.com/63869574/128369738-42852e64-b3d4-4a5d-a78c-6608b5d475aa.png)
### Solution
If this error appears, open the config.properties file, and change PYTHON3_DIRECTORY to the command to run python* (in my case, "python3.8")

![image](https://user-images.githubusercontent.com/63869574/128370078-311fad50-950a-4c3b-92b3-fb6a71344adc.png)

\* *Open CMD or terminal and type python3 (or python), if configure properly, it should show the python version:*

![image](https://user-images.githubusercontent.com/63869574/128370975-d370028c-7856-439a-be97-8adb61695379.png)

## - Error: [Traceback (most recent call last):,   File "scripts/plotFront3D.py", line 3, in <module>,     import pandas as pd , ModuleNotFoundError: No module named 'pandas']

If pandas in not install:
  
![image](https://user-images.githubusercontent.com/63869574/128372707-368d5ec1-6ec4-43a2-85de-71d61503c6e9.png)

### Solution
Install pandas from the CMD or terminal, e.g., for Ubuntu:
  sudo apt-get install python3-pandas -y
  
  ![image](https://user-images.githubusercontent.com/63869574/128373066-4f2b80c0-cb92-4b86-9f0b-f7bcd2d1950a.png)

  Note: Make use you install it in the correct python version (it may be: sudo apt-get install **python**-pandas -y)
  
 

  
