# QBB2019 - Day 4 - Homework Exercise

## Human de novo mutations

Data are taken from Halldorsson, B. V., Palsson, G., Stefansson, O. A., Jonsson, H., Hardarson, M. T., Eggertsson, H. P., ... & Gudjonsson, S. A. (2019). Characterizing mutagenic effects of recombination through a sequence-level genetic map. Science, 363(6425). [link](https://science.sciencemag.org/content/363/6425/eaau1043.abstract)

### Load and wrangle the data

1. Read the abstract for this paper to understand the context.

2. Use pandas to load two data tables from this paper, which encode:
- information about the number and parental origin of each de novo mutation detected in an offspring individual (i.e. "proband") [link](https://www.dropbox.com/s/g47l2r2kmjfzst2/aau1043_dnm.tsv?dl=0)
- ages of the parents of each proband [link](https://www.dropbox.com/s/vxc4tw1qv7j4s4h/aau1043_parental_age.tsv?dl=0)

3. Count the number of de novo mutations per proband. The `Phase_combined` column records the inferred parent of origin of the de novo mutation. Break the counts of de novo mutations down into maternally inherited, paternally inherited, and total de novo mutations (including of unknown parental origin). Store these counts in a new pandas dataframe with columns: `Proband_id`, `pat_dnm`, `mat_dnm`, `tot_dnm`.

4. Use the pandas `merge` function to combine the above data frame with the data frame with maternal and paternal ages.

### Fit and interpret linear regression models

5. Plot:
- the count of maternal de novo mutations vs. maternal age
- the count of paternal de novo mutations vs. paternal age

6. Use ordinary least squares `smf.ols()` to test for an association between maternal age and maternally inherited de novo mutations.
- Is this relationship significant?
- What is the size of this relationship?

7. Use ordinary least squares `smf.ols()` to test for an association between paternal age and paternally inherited de novo mutations.
- Is this relationship significant?
- What is the size of this relationship?

8. Plot a histogram of the number of maternal de novo mutations and paternal de novo mutations per proband on a single plot with semi-transparency.

9. Test whether the number of maternally inherited de novo mutations per proband is significantly different than the number of paternally inherited de novo mutations per proband.

### Generalized linear models: Poisson regression

Note that standard linear regression assumes a continuous response variable. When we want to work with response variables that are "counts", such as the number of de novo mutations, we should technically use an approach such as "Poisson regression" that is designed for count data. To fit a Poisson regression model with Python statsmodels, simply use `smf.poisson()` in place of `smf.ols()`.

10. Re-fit the models (questions 6, 7, and 9) above using Poisson regression.

11. The interpretation of parameter estimates from Poisson regression differs from that of OLS. Using the relevant Poisson regression model that you fit, predict the number of paternal de novo mutations for a proband with a father who was 50.5 years old at the proband's time of birth.
- Hint: use Google to learn about interpreting coefficients from Poisson regression.

### Advanced exercises

12. Select a new dataset from those listed at the bottom of this website: https://github.com/rfordatascience/tidytuesday

If not obvious, the corresponding data can generally be found as a `.csv` file in the `tidytuesday/data/<year>/<date>` subdirectory of the GitHub repository.
  
13. Generate figures to explore these data. What patterns do you notice?

14. Pose a question about the data that can be tested with a linear regression model.

15. Fit your model, evaluate the model fit, and test your hypothesis with the `.summary()` method.



