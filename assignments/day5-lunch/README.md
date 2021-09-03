# QBB2020 - Day 5 - Lunch Exercise

## Instructions

Create a new directory `/Users/cmdb/qbb2021-answers/day5-lunch`.  Answer each question below by creating a new Jupyter Notebook for each question.  Be sure to:

- Use Markdown to create section headers and add narrative about things you found confusing, useful, or interesting.
- Annotate each plot with a title, axis labels, legends, etc. as appropriate.
- `git commit` after each question.

## Exercises

1. Download SNP genotype data that I obtained from the 1000 Genomes Project here:

https://www.dropbox.com/s/p2ef992kl2jmmis/matrix_1kg.txt?dl=0

Note that these are real data, just subset (to some random markers on chromosome 1) and slightly reformatted to save you some trouble. Each row represents a single SNP, while each column represents a single individual. The "0", "1", and "2" entries in the matrix indicate the count of ALT alleles a given sample possesses at a given SNP. Because humans are diploids, they can possess either 0, 1, or 2 copies of a given alternate allele.

2. Load the data into a pandas data frame. Calculate the "alternate allele frequency for each SNP. This is defined as the total number of counts of alternate alleles divided by the total number of chromosomes in the population (i.e., the number of samples x 2). Plot the allele frequency spectrum (a histogram of the allele frequencies across SNPs).

3. Subset the data frame to "common variation", where the alternate allele frequency is between 0.05 and 0.95.

4. Perform principal components analysis to cluster the samples based on their SNP genotypes. Plot your samples on the first and second principal components.
  - HINT: Your figure should have 2548 data points.

## Advanced Exercise

5. Download metadata describing the 1000 Genomes samples here: 

ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20130502/integrated_call_samples_v3.20130502.ALL.panel

6. By intersecting these metadata with your principal component scores, color the PCA plot according to population, superpopulation, and sex (3 separate plots).
  - HINT: Use the pandas `merge` function to merge the principal component data frame with your PCA output, using "sample" as the shared column to merge `on`.
  
7. Try plotting the first three principal components together on a 3D scatter plot.
  - HINT: See https://matplotlib.org/mpl_toolkits/mplot3d/tutorial.html
  