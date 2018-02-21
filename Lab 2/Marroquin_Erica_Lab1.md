```python
from aide_design.play import*
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress
```
# Datasheet for Week 2 Lab: Laboratory Measurements
## Erica Marroquin, em628

| Temperature Measurement     | value |
| --------------------------- | ----- |
| Distilled water temperature |   21.86    |

| Pipette Technique (use DI-100 or Ohaus 160 balance) | value  |
| --------------------------------------------------- | ------ |
| Density of water at that temperature                | 997.8  |
| Actual mass of 990 µL of pure water                 | 0.9878 |
| Mass of 990 µL of water (rep 1)                     | 0.9761 |
| Mass of 990 µL of water (rep 2)                     | 0.9826 |
| Mass of 990 µL of water (rep 3)                     | 0.9992 |
| Mass of 990 µL of water (rep 4)                     | 0.9886 |
| Mass of 990 µL of water (rep 5)                     | 0.996  |
| Average of the 5 measurements                       | 0.9885 |
| Standard deviation of the 5 measurements            | 0.0085 |   

| Precision                                              | value |
| ------------------------------------------------------ | ----- |
| Percent coefficient of variation of the 5 measurements |  0.09 |

| Accuracy                            | value |
| ----------------------------------- | ----- |
| average percent error for pipetting |  0.07   |

Percent error for pipetting is calculated as follows:
$100*\frac{\left | mass_{density} - mass_{balance} \right |}{mass_{density}}$

| Measure Density (use DI-800 or Ohaus 400D or Prec. Std) | value |
| ------------------------------------------------------- | ----- |
| Molecular weight of NaCl (g/mol)                                |   58.4    |
| Mass of NaCl in 100 mL of a 1-M solution (g)               |   5.84     |
| Measured mass of NaCl used (g)                              | 5.8444      |
| Measured mass of empty 100 mL flask (g)                     |   22.41     |
| Measured mass of flask + 1M solution (g)                    |   125.76    |
| Mass of 100 mL of 1 M NaCl solution (g)                    |    103.35|
| Density of 1 M NaCl solution (g/L)                           |1039.08       |
| Literature value for density of 1 M NaCl solution       | 1039.08      |
| percent error for density measurement                    |   0    |

| Prepare methylene blue standards of several concentrations | value |
| ---------------------------------------------------------- | ----- |
| Volume of 1 g/L MB diluted to 100 mL to obtain:            |       |
| 1 mg/L MB                                                  |  1 mL     |
| 2 mg/L MB                                                  |  2 mL     |
| 3 mg/L MB                                                  |  3 mL     |
| 4 mg/L MB                                                  |  4 mL     |
| 5 mg/L MB                                                  |  5 mL     |
| Absorbance of unknown at 660 nm                            |  0.2818   |
| Calculated concentration of unknown                        |    2.59   |

| Measure absorbance at 660 nm using a spectrophotometer | value    |
| ------------------------------------------------------ | -------- |
| Absorbance of distilled water                          | 0        |
| Absorbance of 1 mg/L methylene blue                    | -0.0001  |
| Absorbance of 2 mg/L methylene blue                    | 0.1519   |
| Absorbance of 3 mg/L methylene blue                    | 0.3219   |
| Absorbance of 4 mg/L methylene blue                    | 0.5724   |
| Absorbance of 5 mg/L methylene blue                    | 0.7610   |
| Slope at 660 nm (m)                                    | 0.1626   |
| Intercept at 660 nm (b)                                | -0.10542 |
| Correlation coefficient at 660 nm (r)                  |   .996   |
| Calculated concentration of unknown                    | 2.59     |

The equation for the correlation coefficient is as follows:

$r = \frac{\sum xy-\frac{\sum x\sum y}{n}}{\sqrt{\left ( \sum x^{2}-\frac{\left ( \sum x \right )^{2}}{n} \right )\left ( \sum y^{2}-\frac{\left ( \sum y \right )^{2}}{n} \right )}}$

```python
#finding the correlation coefficient by hard coding
array_absorbance = [-0.0001, 0.1519, 0.3219, 0.5724, 0.7610,]
array_concentration = [1, 2, 3, 4, 5]
sum_x = sum(array_concentration)
sum_y = sum(array_absorbance)
sum_xy = 7.364
sum_x_sq = 55
sum_y_sq = 1.033
n = 5
corr_coeff_num = sum_xy-((sum_x*sum_y)/n)
corr_coeff_denom = np.sqrt((sum_x_sq-(((sum_x)**2)/n))*(sum_y_sq - (((sum_y)**2)/n)))
corr_coeff = corr_coeff_num/(corr_coeff_denom)
corr_coeff
```


where x is the concentration of the solute, y is the absorbance, and n is the number of samples.

2. Create a graph of absorbance at 660 nm vs. concentration of methylene blue in Atom using the exported data file. Does absorbance at 660 nm increase linearly with concentration of methylene blue?

```python
# import your file
file = pd.read_csv('4530Lab1MLK.csv')
array = np.array(file)

#searching for row index where wavelength is 660nm
ix = np.where(array == 6.60000000e+02)
idx = ix[0]
correct_absorbance = array[idx]


#putting only the absorbance in an array
only_absorbance = correct_absorbance[0,1:7]

#creating x-axis variables
concentrations = [0,1,2,3,4,5]

#y = mx+ b
#finding slope and intercept at 660nm using scipy
aa = concentrations[1:]
bb = correct_absorbance[0,2:-1]
slope = linregress(aa, bb)[0]
slope
intercept = linregress(aa, bb)[1]
intercept
#r value = 0.973

## plotting
plt.figure('ax',(10,8))
plt.plot(concentrations,only_absorbance,'o')
#plotting a single point for the unknown concentration
plt.plot(2.75,0.2818,'o')
plt.xlabel('Methylene Blue concentration (mg/L)', fontsize=15)
plt.ylabel('Absorbance', fontsize=15)
plt.title('Absorbance at 660nm vs. Concentration of Methylene Blue')
plt.legend(['known values', 'unknown value'], loc = 'best')
plt.show()
print('Figure 1. Graph showing the relationship between methylene blue concentration (from 1-5 mg/L) and absorbance at 660nm.')
```

Yes, absorbance increases linearly with the concentration of methylene blue. As shown on the graph above, once methylene blue is added, the line is almost linear. Based on the graph above, the concentration of the unknown is 2.75 mg/L of methylene blue, which is different than the calculated value of 2.59 mg/L.

3. Plot $\epsilon$ as a function of wavelength for each of the standards on a single graph. Note that the path length is 1 cm. Make sure you include units and axis labels on your graph. If Beer’s law is obeyed what should the graph look like?
- If Beers law is obeyed, each $\epsilon$ should decrease as wavelength increases.

```python
b = 1 * u.cm
#Beers law
  # log(Po/P) = Ebc
# A = Ebc             E = A/(bc)

wavelengths = array[:,0]*(u.nm)
#Using 1 mg/L concentration
conc_1 = 1 * (u.mg/u.L)
absorbance_1 = array[:,2]
epsilon_1 = absorbance_1/(b*conc_1)
#Using 2 mg/L concentration
conc_2 = 2 * (u.mg/u.L)
absorbance_2 = array[:,3]
epsilon_2 = absorbance_2/(b*conc_2)
#using 3 mg/L concentration
conc_3 = 3 * (u.mg/u.L)
absorbance_3 = array[:,4]
epsilon_3 = absorbance_3/(b*conc_3)
#using 4 mg/L concentration
conc_4 = 4 * (u.mg/u.L)
absorbance_4 = array[:,5]
epsilon_4 = absorbance_4/(b*conc_4)
#using 5 mg/L concentration
conc_5 = 5 * (u.mg/u.L)
absorbance_5 = array[:,6]
epsilon_5 = absorbance_5/(b*conc_5)


plt.figure('ax',(10,8))
plt.plot(wavelengths,epsilon_1)
plt.plot(wavelengths,epsilon_2)
plt.plot(wavelengths,epsilon_3)
plt.plot(wavelengths,epsilon_4)
plt.plot(wavelengths,epsilon_5)
plt.xlabel('Wavelength (nm)', fontsize=15)
plt.ylabel('Extinction coefficients', fontsize=15)
plt.title('Epsilon as a Function of Wavelength')
plt.legend(['epsilon 1', 'epsilon_2', 'epsilon_3', 'epsilon_4', 'epsilon_5'], loc ='best')
plt.show()
print('Figure 2. Graph showing epsilon, a constant, as a function of wavelength.')
```


4. Did you use interpolation or extrapolation to get the concentration of the unknown?
- To get the concentration of the unknown, interpolation was used. The concentration was determined first using the y = mx + b equation, and then decided using two close points on the graph (Figure 1).

5. What colors of light are most strongly absorbed by methylene blue?
- Oranges and reds are most strongly absorbed, leaving the blue color of the liquid. As shown on the graph above (Figure 2), the extinction coefficient spikes at around 660nm, which is where red and orange lie on the visible light spectrum.

6. What measurement controls the accuracy of the density measurement for the NaCl solution? What density did you expect (see prelab 2)? Approximately what should the accuracy be?
- The amount of NaCl added controls the accuracy of the density measurement. The literature value for a 1 M NaCl solution is 1039.08 kg/m^3. The accuracy should be within 10% of the literature value, which is was.

7. Don’t forget to write a brief paragraph on conclusions and on suggestions using Markdown.
8. Verify that your report and graphs meet the requirements as outlined in the course materials.

###Conclusions
The exercises in this lab simply and quickly showed how to perform basic yet essential laboratory techniques. In addition to:
  1. Calibrating and using electronic balances
  2. Using signal conditioning boses and data acquisition software
  3. Digital pipetting
  4. Preparing a solution of known concentration
  5. Preparing dilutions, and
  6. Measuring concentrations using a UV-V spectrophotometer

other skills such as extrapolating (or interpolating) data, manipulating equations to graph a certain function, and data analysis using graphs were learned.

###Suggestions
- The laboratory handout was difficult to navigate. Because there were so many different exercises within the handout, and we were not going in order, all of the different exercises seemed to merge together.
