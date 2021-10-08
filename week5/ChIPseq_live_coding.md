
### Get example data

The data for this example exercise are taken from https://angus.readthedocs.io/en/2017/chip-seq.html, and the original publication:

Chen, X et al. (2008), Integration of external signaling pathways with the core transcriptional network in embryonic stem cells. Cell. Jun 13;133(6):1106-17.

The data include ChIP-seq of the transcription factor Oct4 (`oct4.fastq`) in mouse embryonic stem cells, as well as a control sample (`gfp.fastq`). Due to time constraints and since you've mapped reads before, I've already mapped and sorted the reads.

```bash
wget https://bx.bio.jhu.edu/data/msauria/cmdb-data/chipseq_data.tgz
```

Unpack the data with `tar xzf chipseq_data.tgz` and you should see two files, `Oct4.bam` and `gfp.bam`.


### Call ChIP-seq peaks

Next, let's call ChIP-seq peaks using macs2. We're going to need to specify a custom genome size since the data is restricted to chr1. We also want to get bedgraph files to look at read coverage.

```bash
macs2 callpeak -t Oct4.bam -c gfp.bam --name=Oct4 --gsize=138000000 --bdg
```

Running macs2 will produce the following 6 files:

`Oct4_peaks.xls`: is a tabular file which contains information about called peaks. You can open it in excel and sort/filter using excel functions. Information include position, length and height of detected peak etc.

`Oct4_peaks.narrowPeak`: is BED6+4 format file which contains the peak locations together with peak summit, p-value and q-value. You can load it directly to UCSC genome browser.

`Oct4_summits.bed`: is in BED format, which contains the peak summits locations for every peaks. The 5th column in this file is -log10p-value the same as NAME_peaks.bed. If you want to find the motifs at the binding sites, this file is recommended. The file can be loaded directly to UCSC genome browser. But remember to remove the beginning track line if you want to analyze it by other tools.

`Oct4_model.r`: is an R script which you can use to produce a PDF image about the model based on your data. Load it to R by: $ Rscript NAME_model.r Then a pdf file NAME_model.pdf will be generated in your current directory. Note, R is required to draw this figure.

`Oct4_treat_pileup.bdg`: A pileup of shifted reads from the treatment files.

`Oct4_control_lambda.bdg`: The calculated local lambda background (windowed) from the control files.


### Load it all into IGV

Launch `igv` and load the following files:

1. Oct4_peaks.narrowPeak
2. Oct4_treat_pileup.bdg
3. Oct4_control_lambda.bdg


### Extract the top 100 peak sequences

In order to get the top peaks, we'll need to sort by the p-values (eigth column) in reverse order (largest first since the scores are -log transformed) in the narrowPeak file. Then we need to select only the first 100 lines.

```bash
sort -k8,8nr Oct4_peaks.narrowPeak > Oct4_sorted.narrowPeak
head -n 100 Oct4_sorted.narrowPeak > Oct4_top100.narrowPeak
```

Next, we'll need a way to get the sequence for each of these intervals. Luckily bedtools makes this easy.

`bedtools getfasta` https://bedtools.readthedocs.io/en/latest/content/tools/getfasta.html

```bash
bedtools getfasta -fi /Users/cmdb/data/genomes/mm10.fa -bed Oct4_top100.narrowPeak > Oct4_top100.fa
```


### Motif finding

Now that we have the sequences, let's see if there is a motif that is enriched in these sequences. For this, we're going to use the `meme` suite of tools. 

http://meme-suite.org/doc/meme-chip.html











