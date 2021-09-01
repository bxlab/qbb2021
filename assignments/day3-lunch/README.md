# QBB2021 - Day 3 - Lunch Exercise

You've done a cardiac mutagenesis screen in *Drosophila melanogaster* and find an interesting cluster of mutations around the position 21,378,950 on chromosome 3R.<br /><br />
You surmise that these mutations may affect the expression of the nearest gene, therefore, you're interested in which protein coding gene is closest to this position.<br /><br />
A `.gtf` file contains a list of features, such as genes and transcripts, that have been identified in an organism's genome (in this case, the genome of *D. melanogaster*). Such a file will be especially useful for this problem. If you're interested in more details about the `gtf` file, check out the appendix at the end of the assignment for [more info](#appendix).

In a new `day3-lunch` directory in terminal, use the following two Unix commands to retrieve the **pre-sorted** `gtf` file you will be working with for this assignment.

```
wget --output-document=BDGP6.Ensembl.81.gtf.gz ftp.ensembl.org/pub/release-81/gtf/drosophila_melanogaster/Drosophila_melanogaster.BDGP6.81.gtf.gz

gunzip BDGP6.Ensembl.81.gtf.gz
```

The end result of those two lines is that you have the **pre-sorted** *D. melanogaster* `.gtf` file from build 81: `BDGP6.Ensembl.81.gtf`

## Main Exercise
### 0: Parse input file

The first step of this problem involves parsing the `.gtf` file. We provide you the code for this below. This code creates `genes`, a list of tuples with the gene names, start positions, and end positions of all the protein-coding genes which are located on a specific chromosome of interest. We suggest printing `genes` before you start coding anything else so that you can see the data you're working with.

```
import sys

gtf_file = sys.argv[1]
mut_chrom = sys.argv[2]
mut_pos = int(sys.argv[3])
f = open(gtf_file)

genes = []
for line in f:
    if line.startswith("#"):
        continue
    fields = line.strip("\r\n").split("\t")
    start = int(fields[3])
    end = int(fields[4])
    if (fields[0] == mut_chrom) and (fields[2] == "gene") and ('gene_biotype "protein_coding"' in line):
        subfields = fields[-1].split(';')
        for field in subfields:
            if "gene_name" in field:
                gene_name = field.split()[1]
        genes.append((gene_name, start, end))
```

### 1: Implement Binary Search
* Find and report the nearest protein coding gene to the position 3R:21,378,950.
* Report the gene's linear genomic distance from 3R:21,378,950.
* How many iterations (a tally), did it take the search procedure to find the nearest gene? Report this.

> Hint: It would be helpful to write a function that computes linear genomic distance. What is the linear genomic distance between a position and a gene if the position is within the gene borders?

## Advanced Exercises
### 1: Annotate the code provided to parse the input `.gtf` file
Comment the provided code, explaining what each line or section of lines is doing.

> Hint 1: Comment on the role that the `gene_biotype` value plays in how the input `.gtf` file is parsed.

> Note, to fully utilize the fact that the annotation file is pre-sorted, the code assumes that the gene's start and stop positions do not depend on strand.

### 2: Find the 20 nearest protein coding genes for 3R:21,378,950
* Report the names of these genes, from closest to furthest away.
* Report their corresponding linear genomic distances from 3R:21,378,950.

### 3: Find the nearest gene of any biotype
> Hint: You will have to adapt the provided parsing code; remember you are no longer limiting your search to just protein coding genes.

* What is the name of this gene?
* What is its biotype?

### 4: Find the nearest protein coding gene for each position in a given list of positions
> Hint: You will again have to adapt the provided parsing code; while once again limiting your search to just protein coding genes, you now may be searching positions on any chromosome. (1) What data structure could you use to save chromosome-specific lists of tuples of the info for protein coding genes? (2) In the parsing conditional statement, are there any conditions you should remove?

Retrieve the list of positions of interest by running this code on the command line:
```
$ wget "https://raw.githubusercontent.com/bxlab/qbb2021/master/assignments/day4-lunch/day3_100_positions.txt"
```

For each position:
* Report the nearest protein coding gene.
* Report how many iterations the search for each position takes.


## Submit
Python script(s) and corresponding output(s).

## Appendix

From running `head` on this example `.gtf` file, you can see that it contains some header lines before the lines with information about features. Feature lines consist of 9 tab-separated columns.
```
#!genome-build BDGP6
#!genome-version BDGP6
#!genome-date 2014-07
#!genome-build-accession NCBI:GCA_000001215.4
#!genebuild-last-updated 2014-09
3R      FlyBase gene    722370  722621  .       -       .       gene_id "FBgn0085804"; gene_version "1"; gene_name "CR41571"; gene_source "FlyBase"; gene_biotype "pseudogene";
3R      FlyBase transcript      722370  722621  .       -       .       gene_id "FBgn0085804"; gene_version "1"; transcript_id "FBtr0114258"; transcript_version "1"; gene_name "CR41571"; gene_source "FlyB
3R      FlyBase exon    722370  722621  .       -       .       gene_id "FBgn0085804"; gene_version "1"; transcript_id "FBtr0114258"; transcript_version "1"; exon_number "1"; gene_name "CR41571"; gene_sou
3R      FlyBase gene    835381  2503907 .       +       .       gene_id "FBgn0267431"; gene_version "1"; gene_name "CG45784"; gene_source "FlyBase"; gene_biotype "protein_coding";
3R      FlyBase transcript      835381  2503907 .       +       .       gene_id "FBgn0267431"; gene_version "1"; transcript_id "FBtr0346770"; transcript_version "1"; gene_name "CG45784"; gene_source "FlyB
3R      FlyBase exon    835381  835491  .       +       .       gene_id "FBgn0267431"; gene_version "1"; transcript_id "FBtr0346770"; transcript_version "1"; exon_number "1"; gene_name "CG45784"; gene_sou
3R      FlyBase CDS     835381  835491  .       +       0       gene_id "FBgn0267431"; gene_version "1"; transcript_id "FBtr0346770"; transcript_version "1"; exon_number "1"; gene_name "CG45784"; gene_sou
```
The columns are described below as well as in further detail [here](https://uswest.ensembl.org/info/website/upload/gff.html).
```
1 - seqname: the name of chromosome  
2 - source: the database or project name feature is from
3 - feature: the feature type name (like gene, transcript, exon, CDS, etc.)
4 - start: the inclusive start position of the feature (numbering starts at 1)
5 - end: the inclusive end position of the feature
6 - score: some floating point value
7 - strand: + for forward, - for reverse
8 - frame: indicates which base is the first base of a codon (indexed from 0)
9 - attribute: this is a semicolon separate list that provides additional feature information such as gene biotype (protein coding, pseudogene, etc.), gene name, gene ID, etc.
```

<!-- - ## Pseudocode for Basic Exercise
```
#Initialization
## define search position
## define search chromosome
## open the file
## skip the header
## if a gene is a protein coding gene on the search chromosome (3R)
## then store gene name, gene start, and gene stop in a list

#Binary search
## define lo = 0
## define hi = len(gene list)-1
## define mid = int((hi+lo)/2) make sure it's int division since you are storing an index!!
## define iteration tally = 0
## define previous_mid = hi+1 or None

## while True:
  ## add one to iteration tally
  ## use mid as an index in your gene list to find gene position
  ## if end < search position
    ## then redefine lo
  ## else
    ## then redefine hi
  ## redefine mid
  ## if mid == previous mid
    ## then compute distance
    ## report gene, distance, and tally
    ## break
  ## redefine previous mid
```
-->
