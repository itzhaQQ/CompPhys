To run this Jupyter Notebook just press **Run all**.Used packages: `numpy`, `math` , `matplotlib`The estimated runtime will be $\sim 10-60$ s. For the flowcharts in the markdown-cells: `mermaid` support is recommended to compile.

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

***NOTE:*** Fixed $\tau=1$ measurements referenced in the handwritten PDF come from an earlier diagnostic run. To see those results exchange ``tau = rng.uniform(0.5, 1.5)`` with `tau = 1`
