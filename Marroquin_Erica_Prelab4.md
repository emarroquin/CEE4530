```python
from aide_design.play import*
import scipy
from scipy import optimize
```

#Erica Marroquin
#Prelab 4

###Question 1
1)	Compare the ability of Cayuga lake and Wolf pond (an Adirondack lake) to withstand an acid rain runoff event (from snow melt) that results in 20% of the original lake water being replaced by acid rain. The acid rain has a pH of 3.5 and is in equilibrium with the atmosphere. The ANC of Cayuga lake is 1.6 meq/L and the ANC of Wolf Pond is 70 µeq/L. Assume that carbonate species are the primary component of ANC in both lakes, and that they are in equilibrium with the atmosphere. What is the pH of both bodies of water after the acid rain input? Remember that ANC is the conservative parameter (not pH!). Hint: You can use the scipy optimize root finding function called brentq. Scipy can’t handle units so the units must be removed using .magnitude.

```python
#necessary constants and functions
Kw = 10**(-14)
K1_carbonate = 10**(-6.37)
K2_carbonate = 10**(-10.25)
K_Henry_CO2 = 10**(-1.5)
P_CO2 = 10**(-3.5)

def invpH(pH):
  return 10**(-pH)

def alpha0_carbonate(pH):
   alpha0_carbonate = 1/(1+(K1_carbonate/invpH(pH))*(1+(K2_carbonate/invpH(pH))))
   return alpha0_carbonate

def alpha1_carbonate(pH):
  alpha1_carbonate = 1/((invpH(pH)/K1_carbonate) + 1 + (K2_carbonate/invpH(pH)))
  return alpha1_carbonate

def alpha2_carbonate(pH):
  alpha2_carbonate = 1/(1+(invpH(pH)/K2_carbonate)*(1+(invpH(pH)/K1_carbonate)))
  return alpha2_carbonate

def ANC_closed(pH,Total_Carbonates):
  return Total_Carbonates*(alpha1_carbonate(pH)+2*alpha2_carbonate(pH)) + Kw/invpH(pH) - invpH(pH)

def ANC_open(pH):
  return ANC_closed(pH,P_CO2*K_Henry_CO2/alpha0_carbonate(pH))

#constants from problem statement
pH_acid_rain = 3.5
ANC_cayuga_lake = 1.6*10**(-3)*u.mol/u.L #meq/L
ANC_wolf_pond = 70*10**(-6)*u.mol/u.L #ueq/L
ANC_rain= 10**(-pH_acid_rain)*u.mol/u.L

ANC_cayuga_out = ANC_rain * (1-np.exp(-0.2)) + ANC_cayuga_lake * (np.exp(-0.2))
ANC_wolf_out = ANC_rain * (1-np.exp(-0.2)) + (ANC_wolf_pond*(np.exp(-0.2)))

def ANC_open_cayuga_unitless(pH):
  return (ANC_open(pH)-ANC_cayuga_out.magnitude)

def ANC_open_wolf_unitless(pH):
  return (ANC_open(pH)-ANC_wolf_out.magnitude)

def pH_opencayuga():
  return optimize.brentq(ANC_open_cayuga_unitless, 1, 12)

def pH_openwolf():
  return optimize.brentq(ANC_open_wolf_unitless, 1, 12)

pH_opencayuga()
pH_openwolf()

```

###Question 2
2)	What is the ANC of a water sample containing only carbonates and a strong acid that is at pH 3.2? This requires that you inspect all of the species in the ANC equation and determine which species are important.

The ANC of strong acids are equal to -[H+]. When the pH is low, the concentration of protons is much bigger than those of carbonate, bicarbonate, and hydroxide. Thus in the ANC equation:
$${\text{ANC}} = [HCO_3^ - {\text{] + 2[CO}}_3^{ - 2}{\text{] + [O}}{{\text{H}}^{\text{ - }}}{\text{] - [}}{{\text{H}}^{\text{ + }}}{\text{]}}$$
the -[H+] would dominate.

```python
pH = 3.2
ANC = 10**(-pH)
print('The ANC of a strong acid at pH 3.2 is ',ANC,'.')
```

###Question 3
3)	Why is [H+] not a conserved species?
When the ANC = 0, all additional protons added will stay as protons because there is nothing left for them to react with. Thus, even though ANC is conserved, [H+] is not, because of the additional protons added.
