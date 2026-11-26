# Computational Physics Sheet 4 — Discussion of numerical results and plots

## Task 1: Markov-chain histories
![[figs/hmc_magnetization_histories.png|500]]

### Numerical results:

|                    | $N_{md} = 100$ | $N_{md} = 4$ |
| ------------------ | -------------- | ------------ |
| Acceptance rate    | $99.97\%$      | $64.61\%$    |
| Mean magnetization | $0.4933$       | $0.4913$     |
### Discussion:
- both HMC sims yield mean magnetizations close expected value $\langle m \rangle \approx 0.49$
- $N_{md} = 100$:
	- acceptance rate is $\sim 99.97\%$ 
	- magnetization history shows relatively slow varying fluctuations with gradual increase/decrease and neighbouring values close to each other -> suggests positive autocorrelation between successive measurements
	- with 100 steps the integration step size is $\varepsilon = \frac{1}{100} = 0.01$ resulting in accurate conservation of numerical Hamiltonian resulting in a high acceptance rate
- $N_{md} = 4$:
	- acceptance rate is $\sim 64.61\%$
	- magnetization frequently jumps between values with some horizontal sections where it remains constant for several iterations
	- with 4 leapfrog steps $\varepsilon = \frac{1}{4} = 0.25$ resulting in a larger step size which can produce larger integration errors and therefore more rejected HMC proposals resulting in a retained previous configuration
---
## Task 2: Autocorrelation
![[figs/hmc_magnetization_autocorrelation.png|500]]

### Numerical results:

| Lag     | $N_{md}=100$ | $N_{md}=4$ |
| ------- | ------------ | ---------- |
| $C(0)$  | 1.0000       | 1.0000     |
| $C(1)$  | 0.8608       | 0.5955     |
| $C(10)$ | 0.2098       | 0.2042     |

### Discussion:

- Initial correlations:
	- for $N_{md}=100$ we get $C(1)\approx 0.86$ which means successive magnetization measurements are strongly positively correlated (as suggested by the history in Task 1 with the more smooth fluctuations)
	- for $N_{md}=4$ we get $C(1)\approx 0.60$ so successive measurements are still correlated but less strongly (more abrupt changes in Task 1)
- Later correlations:
	- curves cross at around $\tau\approx 10$ 
	- blue curve initially decays more slowly
	- $N_{md}=100$ shows strong correlations between nearby measurements followed by rapid decay
	- $N_{md}=4$ weaker initial correlations, but correlations persist across larger range of lags
- a lower lag-1 autocorrelation does not necessarily imply smaller statistical error
---
## Task 3: Blocking/Binning
![[figs/hmc_magnetization_blocked_autocorrelation.png|500]]
![[figs/hmc_standard_error_vs_block_size.png|500]]

### Numerical results:

| Block size $b$ | Number of blocks | $C_b(1)$ | $C_b(10)$ | Standard deviation $\sigma_b$ | Standard error $\Delta\bar{m}_b$ |
| -------------- | ---------------- | -------- | --------- | ----------------------------- | -------------------------------- |
| 1              | 12,800           | 0.8608   | 0.2098    | 0.106444                      | 0.000941                         |
| 2              | 6,400            | 0.8016   | 0.0177    | 0.102715                      | 0.001284                         |
| 4              | 3,200            | 0.6712   | 0.0145    | 0.097541                      | 0.001724                         |
| 8              | 1,600            | 0.4730   | -0.0241   | 0.089211                      | 0.002230                         |
| 16             | 800              | 0.2250   | -0.0066   | 0.077142                      | 0.002727                         |
| 32             | 400              | 0.1180   | 0.0211    | 0.060366                      | 0.003018                         |
| 64             | 200              | 0.0659   | 0.0551    | 0.044256                      | 0.003129                         |
### Discussion:
#### Autocorrelation:
- most informative quantity is lag-1 autocorrelation $C_b(1)$
- decrease from $0.8608 \rightarrow 0.0659$ which means less  correlation between neighboring block averages
- plot shows as b increases the autocorrelation function decays towards zero within fewer blocked-chain steps
- expected because with blocking instead of comparing two neighbouring individual measurements we compare averages of two consecutive groups
#### Standard error:
- standard deviation decreases while estimated standard error increases
- **standard deviation:**
	- each blocked measurement is average of $b$ consecutive measurements: $$m_i^{(b)} = \frac{1}{b} \sum_{j=0}^{b-1}m_{ib+j}$$
	- averaging measurements produces smaller fluctuations, consequently $\sigma_b \downarrow$ as $b\uparrow$
- **standard error:**
	- estimated standard error is $$\Delta\bar{m}_b = \frac{\sigma_b}{\sqrt{N_b}}$$
	- with $N_b=N/b$ as b increases we have fewer block averages
	- with great positive autocorrelation of the original chain, the naive $b=1$ estimate causes an underestimation of the uncertainty
	- blocking accounts for increasingly long-range correlations through variance of block averages -> increases standard error even though standard deviation decreases
- for larger block sizes the estimated standard error begins to approach a plateau 
- estimates for $b=32$ and $b=64$ only differ approx. $3.7\%$ -> suggests that chosen block sizes are becoming sufficiently large to account for most of relevant correlations
