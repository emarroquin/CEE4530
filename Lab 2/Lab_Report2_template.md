```python
from aide_design.play import*
```
## Name
1. Datasheet for Week 2 Lab: Laboratory Measurements

| Temperature Measurement     | value |
| --------------------------- | ----- |
| Distilled water temperature |       |

| Pipette Technique (use DI-100 or Ohaus 160 balance) | value |
| --------------------------------------------------- | ----- |
| Density of water at that temperature                |       |
| Actual mass of 990 µL of pure water                 |       |
| Mass of 990 µL of water (rep 1)                     |       |
| Mass of 990 µL of water (rep 2)                     |       |
| Mass of 990 µL of water (rep 3)                     |       |
| Mass of 990 µL of water (rep 4)                     |       |
| Mass of 990 µL of water (rep 5)                     |       |
| Average of the 5 measurements                       |       |
| Standard deviation of the 5 measurements            |       |

| Precision                                              | value |
| ------------------------------------------------------ | ----- |
| Percent coefficient of variation of the 5 measurements |       |

| Accuracy                            | value |
| ----------------------------------- | ----- |
| average percent error for pipetting |       |

Percent error for pipetting is calculated as follows:
$100*\frac{\left | mass_{density} - mass_{balance} \right |}{mass_{density}}$

| Measure Density (use DI-800 or Ohaus 400D or Prec. Std) | value |
| ------------------------------------------------------- | ----- |
| Molecular weight of NaCl                                |       |
| Mass of NaCl in 100 mL of a 1-M solution                |       |
| Measured mass of NaCl used                              |       |
| Measured mass of empty 100 mL flask                     |       |
| Measured mass of flask + 1M solution                    |       |
| Mass of 100 mL of 1 M NaCl solution                     |       |
| Density of 1 M NaCl solution                            |       |
| Literature value for density of 1 M NaCl solution       |       |
| percent error for density measurment                    |       |

| Prepare methylene blue standards of several concentrations | value |
| ---------------------------------------------------------- | ----- |
| Volume of 1 g/L MB diluted to 100 mL to obtain:            |       |
| 1 mg/L MB                                                  |       |
| 2 mg/L MB                                                  |       |
| 3 mg/L MB                                                  |       |
| 4 mg/L MB                                                  |       |
| 5 mg/L MB                                                  |       |
| Absorbance of unknown at 660 nm                            |       |
| Calculated concentration of unknown                        |       |

| Measure absorbance at 660 nm using a spectrophotometer | value   |
| ------------------------------------------------------ | ------- |
| Absorbance of distilled water                          | 0       |
| Absorbance of 1 mg/L methylene blue                    | -0.0001 |
| Absorbance of 2 mg/L methylene blue                    | 0.1519  |
| Absorbance of 3 mg/L methylene blue                    | 0.3219  |
| Absorbance of 4 mg/L methylene blue                    | 0.5724  |
| Absorbance of 5 mg/L methylene blue                    | 0.7610  |
| Slope at 660 nm (m)                                    |         |
| Intercept at 660 nm (b)                                |         |
| Correlation coefficient at 660 nm (r)                  |         |
| Calculated concentration of unknown                    |         |


2. Create a graph of absorbance at 660 nm vs. concentration of methylene blue in Atom using the exported data file. Does absorbance at 660 nm increase linearly with concentration of methylene blue?

```python
# import your file
file = pd.read_csv('yourfilename.csv')
array = np.array(file)

## do your data analysis here
## How to make an array?
#  x = [1,2,3,4,5]
# python starts at index 0
# x[2] = 3
# you can multiply an array with units
# y = [4,5,6] * u.mg/u.L
## 2-D Arrays
# z = np.array([[1,2,3],[4,5,6],[7,8,9]])
# z[1,2] = 5
# z[2,:] = [7,8,9]

## plotting
plt.figure('ax',(10,8))
plt.plot(concentration,absorbance)
# put in your x and y variables
plt.xlabel('Methylene Blue concentration', fontsize=15)
plt.ylabel('Absorbance', fontsize=15)
plt.show()
```
Your answer to the questions here.

3. Plot $\epsilon$ as a function of wavelength for each of the standards on a single graph. Note that the path length is 1 cm. Make sure you include units and axis labels on your graph. If Beer’s law is obeyed what should the graph look like?
```python
b = 1 * u.cm
## Multiplication of Arrays
# you can multiply and divide arrays by constants!
# x = [1,2]
# y = 3
# z = 4
# a = x/z
# a = [0.25,0.5]
# b = x*y
# b = [3,6]
plt.figure('ax',(10,8))
plt.plot(wavelength,epsilon_1)
# put in your x and y variables
plt.plot(wavelength,epsilon_2)
# put in your x and y variables
plt.plot(wavelength,epsilon_3)
# put in your x and y variables
plt.plot(wavelength,epsilon_4)
# put in your x and y variables
plt.plot(wavelength,epsilon_5)
# put in your x and y variables
plt.xlabel('Wavelength (nm)', fontsize=15)
plt.ylabel('Extinction coefficients', fontsize=15)
plt.show()
```

Your answer to the question here

4. Did you use interpolation or extrapolation to get the concentration of the unknown?
5. What colors of light are most strongly absorbed by methylene blue?
6. What measurement controls the accuracy of the density measurement for the NaCl solution? What density did you expect (see prelab 2)? Approximately what should the accuracy be?
7. Don’t forget to write a brief paragraph on conclusions and on suggestions using Markdown.
8. Verify that your report and graphs meet the requirements as outlined in the course materials.
