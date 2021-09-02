# QBB2021 - Day 4 - Lunch Exercises

## Instructions

The following exercises build on the plots that we started during the morning session.  Jupyter Notebooks of these plots can be found [here](https://github.com/bxlab/qbb2021/tree/main/assignments/day4-lunch).

To complete these exercises, first create a new directory `/Users/cmdb/qbb2021-answers/day4-lunch`. Inside this directory, create a jupyter notebook for this assignment. Answer each question below by:

- Using Markdown to create section headers and add narrative about things you found confusing, useful, or interesting. You should also use narrative to document why you did something or what sources you used (like where you found an equation or info about matplotlib functions).
- Annotate each plot with a title, axis labels, legends, etc. as appropriate.
  - Check out this cool [gallery/cheatsheet](http://bxlab.github.io/cmdb-bootcamp/gallery/README.html) that a former TA made which you may find useful
- `git commit` after each question.

## Basic Exercises

1. Create an [MA plot](https://en.wikipedia.org/wiki/MA_plot) to visualize RNA-seq data with the average gene abundance on the x-axis and fold-change on the y-axis

    - You may choose any two samples to plot. (Be sure to document which two in your markdown narrative. Perhaps also provide reasoning for why you think the comparison is cool.)
    - To calculate the average gene abundance (or the "A" in MA), you want to find the mean for each gene across the two samples. (Be sure to document your source for the equation you use)
    - To calculate the log ratio (or the "M" in MA), you will similarly find the ratio for each gene between the two samples, and then take the log of the ratio.

1. Update your plot of FBtr0331261 abundance over time with

    - Each sex as a separate series
    - `+` symbols for Stage 14 replicates (data available in `~/qbb2021/data/replicates.csv`)

## Advanced Exercises

1. On your MA plot, highlight the five genes in Figure 3 from [Lott et al., 2011 PLoS Biology](https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1000590) using different colors

1. Generalize the code you used to produce the MA plot, such that it will accept and plot any two specified samples. (*Hint:* Think function)

1. Recreate as much of Figure 3 as possible from [Lott et al., 2011 PLoS Biology](https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1000590), starting with sisA