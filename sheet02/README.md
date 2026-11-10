**!! Before running the code make sure to set different values for  `n_therm`, `n_meas` and `h_vals` or the code will run for ~ 40 min depending on the setup.!!**

- ***Task 3***
  Runtime with set values: $\sim 25$ mins
  The simulation ran for the *magnetization vs. h* - plots in the PDF (for better analysis) with:

```Python
h_vals = np.unique(np.concatenate([
    np.linspace(-1, 1, 11), # magnetic field values
    np.linspace(-0.2, 0.2, 17) # more values around h=0
]))
n_therm = 2000
n_meas = 5000
```

The code is documented in the .ipynb file (with sections dividing each task) and the PDF is for discussion and analysis tasks.

- ***Task 4***
  Runtime with set values: $\sim 5$ mins
  The simulation ran for the *energy vs. h* -plots with:

```Python
J_vals = np.linspace(0.25, 2.0, 25)
L_vals = [4, 8, 12, 16, 20]

n_therm = 1000
n_meas = 3000
```

- ***Task 5***
  Runtime with set values:  $\sim 5$ mins
  The simulation ran for the *abs. mean magnetization vs inverse coupling strength* - plot with:

```Python
J_vals = np.linspace(0.25, 1.0, 31)
L_vals = [4, 8, 12, 16, 20] 

n_therm = 2000
n_meas = 5000
```

- ***Task 6***
  Runtime with set values: $\sim 6$  mins
  The simulation ran for the specific heat vs. J -plots with:

```Python
J_vals = np.sort(np.unique(np.concatenate([
    np.linspace(0.25, 1.0, 31),
    np.linspace(0.38, 0.50, 25) #smaller increments near J_c
])))
L_vals = [4, 8, 12, 16, 20] 

n_therm = 1000
n_meas = 3000
```
