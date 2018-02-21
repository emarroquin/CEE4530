```python
from aide_design.play import*
from scipy import optimize
```

#Erica Marroquin
#Prelab 3

###Question 1
1)	Compare the ability of Cayuga lake and Wolf pond (an Adirondack lake) to withstand an acid rain runoff event (from snow melt) that results in 20% of the original lake water being replaced by acid rain. The acid rain has a pH of 3.5 and is in equilibrium with the atmosphere. The ANC of Cayuga lake is 1.6 meq/L and the ANC of Wolf Pond is 70 µeq/L. Assume that carbonate species are the primary component of ANC in both lakes, and that they are in equilibrium with the atmosphere. What is the pH of both bodies of water after the acid rain input? Remember that ANC is the conservative parameter (not pH!). Hint: You can use the scipy optimize root finding function called brentq. Scipy can’t handle units so the units must be removed using .magnitude.

```Python
pH_acid_rain = 3.5
ANC_cayuga_lake = 1.6 #meq/L
ANC_wolf_pond = 70 #ueq/L


```

###Question 2
2)	What is the ANC of a water sample containing only carbonates and a strong acid that is at pH 3.2? This requires that you inspect all of the species in the ANC equation and determine which species are important.

###Question 3
3)	Why is [H+] not a conserved species?
