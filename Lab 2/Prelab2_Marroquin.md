```python
from aide_design.play import*
```
## Laboratory 2 Pre Lab Questions
### Erica Marroquin

1. You need 100 mL of a 1 µM solution of zinc that you will use as a standard to calibrate an atomic adsorption spectrophotometer. Find a source of zinc ions combined either with chloride or nitrate (you can use the internet or any other source of information). What is the molecular formula of the compound that you found?
 - Zinc chloride, ZnCl2

 Zinc disposal down the sanitary sewer is restricted at Cornell and the solutions you prepare may need to be disposed of as hazardous waste. As an environmental engineering student you strive to minimize waste production. How would you prepare this standard using techniques readily available in the environmental laboratory so that you minimize the production of solutions that you don’t need? Note that we have pipettes that can dispense volumes between 10 μL and 1 mL and that we have 100 mL and 1 L volumetric flasks. Include enough information so that you could prepare the standard without doing any additional calculations. Consider your ability to accurately weigh small masses. Explain your procedure for any dilutions. Note that the stock solution concentration should be an easy multiple of your desired solution concentration so you don’t have to attempt to pipette a volume that the digital pipettes can’t be set for such as 13.6 μL.
```python

#concentration * volume = mass
vol_zinc = 100*(u.mL)
molecular_wt_zncl2 = 136.3 *(u.g/u.mol)
conc_zinc = (10**-6)*(u.mol/u.L) * molecular_wt_zncl2
mass_zinc = conc_zinc * vol_zinc
print('The mass of zinc chloride necessary in a 100mL container would be ',mass_zinc.to(u.ug),'.')
#adding this mass to a 100mL container of distilled water will produce the correct standard without any waste

```
2. The density of sodium chloride solutions as a function of concentration is approximately 0.6985C + 998.29 (kg/m3) (C is kg of salt/m3). What is the density of a 1 M solution of sodium chloride?
```python

#density = mass / volume
molecular_mass_NaCl = 58.4*(u.g/u.mol)
conc_NaCl = molecular_mass_NaCl * 1*(u.mol/u.L)
density_NaCl = 0.6985*conc_NaCl + 998.29*(u.kg/u.m**3)
print('The density is ',density_NaCl.to(u.kg/u.m**3),'.')
