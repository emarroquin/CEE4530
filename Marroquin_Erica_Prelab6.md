```python
from aide_design.play import*
```

### Erica Marroquin
### CEE 4530
### Pre-laboratory #6: Gas Transfer

---

#### Question 1
1. Calculate the mass of sodium sulfite needed to reduce all the dissolved oxygen in 4 L of pure water in equilibrium with the atmosphere and at 30 deg C.

The mass of sodium sulfite necessary can be determined by stoichiometry:

$$4L H_2O * \frac{7.7mg O_2}{L}* \frac{1 mol O_2}{32000 mg O_2}* \frac{2 mol Na_2SO_3}{1 mol O_22}* \frac{126000mg Na_2SO_3}{1 mol Na_2SO_3}$$

where 7.7 $\frac{mg O_2}{L}$ is the amount of dissolved oxygen water can hold at 30 $^{\circ}$ C.

```python
mass_sodium_sulfite = (4*7.7*2*126000)/(32000) * (u.mg)
print(mass_sodium_sulfite)
```
The mass of sodium sulfite needed is 242.6 mg to reduce all the dissolved oxygen.

#### Question 2
2. Describe your expectations for dissolved oxygen (DO) concentration as a function of time during your reaeration experiment. Assume you added enough sodium sulfite to consume all of the oxygen at the start of the experiment. What would the shape of the curve look like?

As the sodium sulfite was added, the DO concentration will dip to zero from the initial DO concentration, Co. Then, as time went on, the DO concentration will start to decrease from zero until the concentration of saturated DO is reached. The dip will look like a negative exponential, and then increase in the form of a square root, tapering off at DOsat.

#### Question 3
3. Why is ${\widehat{k}}_{\nu, l}$ not zero when the gas flow rate is zero? How can oxygen transfer into the reactor even when no air is pumped into the diffuser?

${\widehat{k}}_{\nu, l}$ is the volumetric gas transfer coefficient. The is not a function of gas flow rate; it is only a function of oxygen diffusion coefficient (D), the interface surface area (A), the liquid volume (V), and the thickness of the laminar boundary layer ($\delta$).
$${\widehat{k}}_{\nu, l} = f(D, \delta, A, V)$$
$${\widehat{k}}_{\nu, l} = \frac{AD}{V \delta}$$

This oxygen transfer happens even when there is no air pumped into the diffuser because oxygen transfor occurs at any open boundary. So, this can happen at the surface of the reactor, even if it is very small, instead of just at the diffusers.

#### Question 4
4. Describe your expectations for ${\widehat{k}}_{\nu, l}$ as a function of gas flow rate. Do you expect a straight line? Why?

As gas flow rate ($Q_{air}$) increases, the molar transfer rate of oxygen through the diffuser (${\dot{n}}_{gas, O_2}$) also increases. Assuming this causes an increase in the oxygen diffusion coefficient (D), thus I expect  ${\widehat{k}}_{\nu, l}$ to increase linearly.

#### Question 5
5. A dissolved oxygen probe was placed in a small vial in such a way that the vial was sealed. The water inside the vial was sterile. Over a period of several hours the dissolved oxygen concentration gradually decreased to zero. Why?

The dissolved oxygen probe reduces oxygen to water. If the vial was sealed, then no new oxygen can enter it; there is a finite amount of oxygen in the water. Once all of the dissolved oxygen in the vial has been reduced to water, and since the oxygen is not being replenished, the dissolved oxygen concentration will eventually reach zero.
