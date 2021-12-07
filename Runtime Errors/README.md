# Error found when running Evochecker

## Returning 0 values
If Evochecker returns 0's in the Front data set (data>name of the problem> NSGAII) even when "0.0" is not a feasible solution, must likely there is a problem that EvoChecker cannot handle.

![image](https://user-images.githubusercontent.com/63869574/145025829-55656696-0d40-4f5d-866c-194dd4ec856d.png)

### Check properties
For instance, for MDP the propeties file should look like:
```
//objective, min
R{"idle"}min=?[F done]
```
If it is written differently, as for DTMC, it won't work:
```
//objective, min
R{"idle"}=?[F done]
```
### Change MAX_EVALUATIONS and POPULATION_SIZE
In the config.properties file, reduce the number of evaluations and population size to a minimum and see if it gives a result. If it does, tune these values[^1].

```
POPULATION_SIZE = 5
MAX_EVALUATIONS = 10
```
Note. In general, select a population size smaller than the number of solutions.


[^1]: EvoChecker seems to return 0's with "big" values of POPULATION_SIZE and/or MAX_EVALUATIONS. These values are dependent on the model. It is not clear why. The user must adjust these values so that they are big enough to return an near-optimal solutions without getting the error of returning 0's.
