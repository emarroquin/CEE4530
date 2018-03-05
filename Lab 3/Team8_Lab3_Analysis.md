```python
from aide_design.play import*
```

# Lab 3: Acid Rain
### Team 8: Erica Marroquin, Jonathan Harris, Sung Min Kim

#### Question 1
Plot measured pH of the lake versus hydraulic residence time (t/$\theta$).

```python
file = pd.read_csv('AcidRain_Test1.csv')
array = np.array(file)

#constants
residence_time = 15*u.min
time = array[:,1] * u.s
pH = array[:,3]
hydraulic_residence_time = time/residence_time.to(u.s)

#plotting graph of ph vs hydraulic residence time
plt.figure()
plt.plot(hydraulic_residence_time,pH,'-')
plt.xlabel('Hydraulic Residence Time (dimensionless)')
plt.ylabel('pH of Lake')
plt.title('pH of Lake vs. Hydraulic Residence Time')
plt.savefig('pHgraph.png')
plt.show()
```

![pHgraph](https://github.com/jdh345/CEE4530/blob/master/AcidRain/pHgraph.png?raw=true)


```python
Kw = 10**(-14)
K1_carbonate = 10**(-6.37)
K2_carbonate = 10**(-10.25)
K_Henry_CO2 = 10**(-pH)
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

a_0 = alpha0_carbonate(pH)
a_1 = alpha1_carbonate(pH)
a_2 = alpha2_carbonate(pH)
```
#### Question 2
Assuming that the lake can be modeled as a completely mixed flow reactor and that ANC is a conservative parameter, equation 1.21 can be used to calculate the expected ANC in the lake effluent as the experiment proceeds. Graph the expected ANC in the lake effluent versus the hydraulic residence time (t/$\theta$) based on the completely mixed flow reactor equation with the plot labeled (in the legend) as “conservative ANC.”

```python
import Environmental_Processes_Analysis as EPA

ANCAcidRain = -(10**(-3))
ANC_0 = .001854

def ANC_out(t):
  return ANC_0*2.71828**(-t) + ANCAcidRain*(1-2.71828**(-t))

def ANC_closed(pH,Total_Carbonates):
  return Total_Carbonates*(alpha1_carbonate(pH)+2*alpha2_carbonate(pH)) + (Kw/invpH(pH)) - invpH(pH)

def ANC_open(pH):
  denom = (P_CO2*K_Henry_CO2)/(alpha0_carbonate(pH))
  return ANC_closed(pH, denom)

#plotting expected ANC in the lake effluent vs hydraulic residence time
plt.figure()
plt.plot(hydraulic_residence_time, ANC_out(hydraulic_residence_time.magnitude),
  hydraulic_residence_time, ANC_closed(pH,ANC_0),
  hydraulic_residence_time,ANC_open(pH))
plt.xlabel('Hydraulic Residence Time (dimensionless)')
plt.ylabel('ANC Concentration (eq/L)')
plt.title('ANC Concentration of Lake vs. Hydraulic Residence Time')
plt.legend(['Closed ANC', 'Conservative ANC', 'Open ANC'], loc = 'best')
plt.savefig('ANCexpected.png')
plt.show()
```
![EffluentANC](https://github.com/jdh345/CEE4530/blob/master/AcidRain/ANCexpected.png?raw=true)

#### Question 3
If we assume that there are no carbonates exchanged with the atmosphere during the experiment, then we can calculate ANC in the lake effluent by using equation 1.11 describing the ANC of a closed system. Calculate the ANC under the assumption of a closed system and plot it on the same graph produced in answering question #3 with the plot labeled (in the legend) as “closed ANC.”

```python
def ANC_closed(pH,Total_Carbonates):
  return Total_Carbonates*(alpha1_carbonate(pH)+2*alpha2_carbonate(pH)) + (Kw/invpH(pH)) - invpH(pH)
```
Plot is shown on the graph in #2.

#### Question 4
If we assume that there is exchange with the atmosphere and that carbonates are at equilibrium with the atmosphere, then we can calculate ANC in the lake effluent by using equation 1.15 describing the ANC of an open system. Calculate the ANC under the assumption of an open system and plot it on the same graph produced in answering question 3 with the plot labeled (in the legend) as “open ANC.”

```python
def ANC_open(pH):
  denom = (P_CO2*K_Henry_CO2)/(alpha0_carbonate(pH))
  return ANC_closed(pH, denom)
```
Plot is shown on the graph in #2.


#### Question 5
Analyze the data from the 2nd experiment and graph the data appropriately. What did you learn from the 2nd experiment?

```python
file2 = pd.read_csv('AcidRain_Test2.csv')
array2 = np.array(file2)
time2 = array2[:,1]*u.s
pH2 = array2[:,3]

plt.figure()
plt.plot(hydraulic_residence_time,pH,'g-',label='First Experiment')
plt.plot(hydraulic_residence_time,pH2,'r-',label='Second Experiment')
plt.xlabel('Hydraulic Residence Time (dimensionless)')
plt.ylabel('pH of Lake')
plt.title('pH of Lake vs. Hydraulic Residence Time')
plt.legend()
plt.savefig('pHgraphcompared.png')
plt.show()

plt.figure()
plt.plot(hydraulic_residence_time, ANC_out(hydraulic_residence_time.magnitude),
  hydraulic_residence_time, ANC_closed(pH2,ANC_0),
  hydraulic_residence_time,ANC_open(pH2))
plt.xlabel('Hydraulic Residence Time (dimensionless)')
plt.ylabel('ANC Concentration (eq/L)')
plt.title('ANC Concentration of Lake vs. Hydraulic Residence Time')
plt.legend(['Closed ANC', 'Conservative ANC', 'Open ANC'], loc = 'best')
plt.savefig('ANCexpected2.png')
plt.show()

plt.figure()
plt.plot(hydraulic_residence_time, CT_out(hydraulic_residence_time.magnitude),
  hydraulic_residence_time, closed_CT(ANC_out(hydraulic_residence_time.magnitude),pH2),
  hydraulic_residence_time, equilibrium_CT(pH2))
plt.xlabel('Hydraulic Residence Time (dimensionless)')
plt.ylabel('Concentration of Carbonate Species (mg/L)')
plt.legend(['Conservative CT', 'Closed CT', 'Equilibrium CT'], loc = 'best')
plt.savefig('ConservativeCT2.png')
plt.show()
```

![pHcompared](https://github.com/jdh345/CEE4530/blob/master/AcidRain/pHgraphcompared.png?raw=true)
![ANCexpected2](https://github.com/jdh345/CEE4530/blob/master/AcidRain/ANCexpected2.png?raw=true)
![ConservativeCT2](https://github.com/jdh345/CEE4530/blob/master/AcidRain/ConservativeCT2.png?raw=true)

For the second experiment, the team slowed down the speed of the stir bar in the lake. The graphs are very similar between the two experiments, and the stir bar had no significant impact. The team hypothesizes that if the stir bar was turned off completely, then there would be a noticeable difference between the two experiments.
