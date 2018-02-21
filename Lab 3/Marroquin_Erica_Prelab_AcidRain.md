```python
from aide_design.play import*
```

## Laboratory 3: Acid Rain Pre-Laboratory Questions
### Erica Marroquin

1. How many grams of NaHCO3 would be required to keep the ANC levels in a lake above 50 ueq/L for 3 hydraulic residence times given an influent pH of 3.0 and a lake volume of 4 L, if the current lake ANC is 0 ueq/L?

```python
#constants
residence_time = 15*u.minutes
time = 3*residence_time
time
lake_volume = 4*u.L
ANC_out = 50*(u.umol/u.L)
ANC_in = -0.001*(u.mmol/u.L)
mol_wt_NaHCO3 = 84*(u.mg/u.mmol)

#solving for ANC_o
ANC_o = (ANC_out - ANC_in*(1-np.exp(-time/residence_time)))*(np.exp(time/residence_time))

#solving for mass needed
mass_needed = ANC_o*mol_wt_NaHCO3*lake_volume
print('The mass needed to achieve an ANC level above 50 ueq/L would be ',mass_needed.to(u.mg),'.')

```
