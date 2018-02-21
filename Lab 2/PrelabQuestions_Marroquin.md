```python
from aide_design.play import*
```
## Laboratory 1 Pre Lab Questions
### Erica Marroquin

1. Why are contact lenses hazardous in the laboratory?

- Contact lenses are hazardous in the laboratory because they can trap foreign materials against the eye, can absorb chemical vapors, and are difficult to take out in the case of an emergency.
2. What is the minimum information needed on the label for each chemical? When are Right-To-Know labels required?
- At minimum, each chemical should have a label with its name, not only the chemical formula, concentration, and date prepared. Right-to-Know labels are required when a chemical is a hazardous material, has corrosive, ignitability, toxic, or reactive characteristics, and is made into a solution or repackaged as a solid or liquid in concentration greater than 1%.
3. Why is it important to label a bottle even if it only contains distilled water?
- Unlabeled chemicals are very difficult to dispose of and can be potentially hazardous. Even if the bottle only contains distilled water, a label will prevent time wasted on figuring out disposal methods and potential hazard.
4. Find an SDS for sodium nitrate.
- Yes.
1. Who created the SDS?
- SDS was created by Fisher Science Education.
2. What is the solubility of sodium nitrate in water?
- Solubility in water is > 100 g/L at 20 degrees C.
3. Is sodium nitrate carcinogenic?
- No.
4. What is the LD50 oral rat?
- LD50 oral rat is > 2000 mg/kg bw.
5. How much sodium nitrate would you have to ingest to give a 50% chance of death (estimate from available LD50 data).
```python
weight = 170 * u.lbs
mass = weight.to(u.kg)
death = weight.to(u.kg) * 2000*(u.mg/u.kg)
print('I would have to ingest more than ',death.to(u.g),' in order to have a 50% chance of death.')
```
10. How much of a 1 M solution would you have to ingest to give a 50% chance of death?
```python
#mass = concentration * volume
#volume = mass / concentration
molecular_weight = 84.99*(u.g/u.mol)
conc = 1*(u.mol/u.L) * molecular_weight
ingestion_volume = death / conc
print('I would have to ingest ',ingestion_volume.to(u.L),' in order to have a 50% chance of death.')

```
11. Are there any chronic effects of exposure to sodium nitrate?
- There could be delayed lung effects after short term exposure.

12. You are in the laboratory preparing chemical solutions for an experiment and it is lunchtime. You decide to go to CTB to eat. What must you do before leaving the laboratory?
- Close and label all chemical containers. Even if wearing gloves, one should still wash their hands and arms before leaving. Make sure that there is nothing that could cause a potentially hazardous situation, such as leaving a pump running or forgetting to close a cap.
