To run this Jupyter Notebook just press **Run all**.\
Used packages: `numpy`, `math` , `matplotlib`\
The estimated runtime will be $\sim 10-60$ s.\ 

- The function for task 3:

```python
def leapfrog(p0, phi0, N_md, N, beta, J_hat, h, tau=1.0)
```

uses

```python
epsilon = tau / N_md
```

instead of

```Python
epsilon = 1.0 / N_md
```

so that for task 4 the function

```Python
def hmc_step(phi, N_md, N, beta, J_hat, h, rng):
```

can be modified to randomize the trajectory length to avoid resonances:

```Python
tau = rng.uniform(0.5, 1.5) # randomize trajectory length
```
