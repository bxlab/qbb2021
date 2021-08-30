# QBB2021 - Day 1 - Lunch Exercises

## Instructions

We will continue exploring the genome annotation files introduced this morning.
These annotations were obtained from the GEP UCSC Genome Browser (with slight modifications[[1](#notes)]).
Information about these datasets can be found by visiting the [Track Configuration page](https://gander2.wustl.edu/cgi-bin/hgTracks?hgTracksConfigPage=configure).
Refer to UCSC Genome Browser for a detailed description of the [BED format](https://genome.ucsc.edu/FAQ/FAQformat.html#format1) and more.

The following exercises provide an opportunity to practice using [The Unix Shell](https://swcarpentry.github.io/shell-novice/) [[Unix Cheat Sheat](http://bxlab.github.io/cmdb-bootcamp/cheatsheet/unix.html)].  You will be required to:

- Navigate and organize the file system
- Construct commands using basic Unix tools
- Save results by redirecting program output
- Edit text files using TextMate.app (or nano, etc.)
- Submit assignments to GitHub

`git push` the results of each exercise after completion (do not wait till the end).

## Exercises

1. Prepare your workspace (HINT: you may want to use `cd`, `mkdir`, and `cp` for these exercises)

    a. Create a `/Users/cmdb/qbb2021-answers/day1-lunch` directory.

    b. Use TextMate.app (or `nano`, etc.) to create a `README.md` file in your new `day1-lunch` directory. You'll be using this README to keep track of the commands you used for this assignment.
    
    c. Make a copy of the following files in your new `day1-lunch` directory.  Check that the size of each file matches the original.
    
    ```
    /Users/cmdb/qbb2021/data/K27me3.bed
    /Users/cmdb/qbb2021/data/K4me3.bed
    /Users/cmdb/qbb2021/data/K9me3.bed
    /Users/cmdb/qbb2021/data/LADs_Kc.bed
    /Users/cmdb/qbb2021/data/S2_9state.bed
    /Users/cmdb/qbb2021/data/dm6.chrom.sizes
    /Users/cmdb/qbb2021/data/fbgenes.bed
    ```
    
    d. Record the commands you used in part C in your `README.md` file. Whenever you record commands in your `README.md` file, note which question (i.e. 1C) those commands were used for.

    e. Record your file sizes by saving the output of `ls` into a file named `directory.txt` (HINT: what flag do you need to use?).
    
    f. git add commit push `directory.txt` and `README.md`.
    
    g. Check your submission on https://github.com.

2. Count features in `.bed` files (HINT: you may want to use `wc` for these exercises)

    a. Create a `feature_count.txt` file that reports the number of features in each of the six .bed files, one per line e.g.
    
    ```
        7516 K27me3.bed
        4909 K4me3.bed
       	   ...
    ```
    
    b. Add your command(s) to `README.md`.
    
    c. Make (at least) two biological observations based on `feature_count.txt`. Add these observations to your `README.md` file (noting that this is for question 2C).
    
    d. git add commit push `feature_count.txt` and `README.md`.

3. Summarize distribution of gene annotations across chromosomes (HINT: you may want to use `cut`, `sort`, and `uniq` for these exercises)

    a. Create a `fbgenes.info` file that summarizes how many genes in `fbgenes.bed` are on each chromosome e.g.
    
    ```
    5708 chr2L
    6112 chr2R
       ...
    ```
    
    b. Add your command(s) to `README.md`.
    
    c. Add two biological observations based on `fbgenes.info` to `README.md`.
    
    d. git add commit push `fbgenes.info` and `README.md`.

4. Generate additional summary statistics using `bedtools summary`

    `bedtools summary` is a great tool to check for biases when examining chromosome distributions.  As this tool is still under development (follow along on [Twitter](https://twitter.com/aaronquinlan/status/1357149157123706882)) please refer to [[2](#notes)] for more details on the output e.g.
    
    ```
    chrom  num_records  total_bp  chrom_frac_genome  frac_all_ivls  frac_all_bp  min  max      mean
    chr3R  7246         78379225  0.22320            0.236          0.234        168  1965857  10816.896
    chr3L  5905         64397032  0.19558            0.192          0.193        181  434041   10905.509
        ...
    ```

    a. Create a `fbgenes.summary10` file that contains the first 10 lines of summary statistics output for `fbgenes.bed` (along with `dm6.chrom.sizes`) by completing the following command (run `man column` to learn how it makes output pretty):

    ```
    bedtools summary <fill in missing parts> | column -t
    ```
    
    b. Add your command(s) to `README.md`.
    
    c. Add two biological observations based on `fbgenes.summary10` to `README.md`.
    
    d. git add commit push `fbgenes.summary10` and `README.md`.

5. Look for chromosomes enriched in genes that overlap K9me3 histone modifications 

    a. Create a `chr-with-fbgenes-k9.txt` file where each line summarizes for a given chromosome how many genes overlap `K9me3.bed` by completing the following command:
    
    ```
    bedtools intersect <fill in missing parts>
    ```
    
    b. Be sure to use the correct option as `bedtools intersect` by default reports "each and every intersection" ([read more](https://bedtools.readthedocs.io/en/latest/content/tools/intersect.html)).

    c. Add your command(s) to `README.md`.
    
    d. Add two biological observations based on `chr-with-fbgenes-k9.txt` to `README.md`.
    
    e. git add commit push `chr-with-fbgenes-k9.txt` and `README.md`.

## Advanced Exercises

1. Visualize the region surrounding Sxl using IGV

    a. Download a copy of the 588 MB file `SRR072893.bam` into your `day1-lunch` directory using the following command.
    
    ```
    wget https://bx.bio.jhu.edu/track-hubs/cmdb/SRR072893.bam
    ```

    b. Create an index file for `SRR072893.bam` that IGV and other programs will require for fast access.
    
    ```
    samtools index /Users/cmdb/qbb2020-answers/day3-lunch/SRR072893.bam
    ```

    c. Start IGV by running `igv`.

    d. Switch the active genome in the upper left from `Human hg19` to `D. melanogaster (dm6)`.
    
    e. Load using `File > Load from File ...` the chromatin information (`K4me3.bed`, `K9me3.bed`, `K27me3.bed`, and `S2_9state.bed`) and RNA abundance in stage 10 male embryo (`SRR072893.bam`).
    
    f. Visualize the region surrounding Sxl by entering `chrX:7,040,000-7,141,000` into the top search box.
    
    g. Adjust read visibility by changing `View > Preferences > Alignments > Visibility range` to 100.

    h. Adjust annotation visibility by holding down the `<CTRL>` key and using your mouse pointer to click on the S2_9state.bed track name to select "Expanded".
    
    i. Create an image named `Sxl-region.png` using `File > Save Image`.
    
    j. Add two biological observations based on this visualization to `README.md`.
    
    k. git add commit push `Sxl-region.png` and `README.md`.

2. Find promoters that overlap two histone modifications

    a. Create a `promoters.bed` file using `bedtools flank` for 200 bp upstream of each gene.
    
    b. Find overlaps with `K4me3.bed` and `K9me3.bed`.
    
    c. Visually verify and create an image named `promoter-k4-k9.png`.
    
    d. Add two biological observations and your command(s) to `README.md`.    
    
    e. git add commit push `promoter-k4-k9.png` and `README.md`.

3. Explore the modENCODE 9-state Model

    State 5 is described as "Actively transcribed exon on the male X chromosome (dosage compensation)" [[ref](https://gander2.wustl.edu/cgi-bin/hgTrackUi?hgsid=108550_w9o9f6bmUUMVFa8WRxX1h72rgwPF&g=S2_9state&hgTracksConfigPage=configure)].  These states are encoded in the fourth column of `S2_9state.bed`

    ```
    chrX	122506	130306	9_17750	1000	+	122506	130306
    chrX	130506	132506	5_17751	1000	+	130506	132506
    chrX	132506	177106	9_17752	1000	+	132506	177106
    chrX	177106	177706	4_17753	1000	+	177106	177706
    ```

    a. Create three new files `state1.bed`, `state2.bed`, `state5.bed` that contain only features corresponding to the specified state (HINT: try using `grep`).
    
    b. Summarize the number of features per chromosome (HINT: you may want to use `cut`, `sort`, and `uniq` for this exercise).
    
    c. Compare the similarity between each state and each histone modification using `bedtools jaccard`.
    
    d. Add two biological observations and your command(s) to `README.md`.    
    
    e. git add commit push `README.md` and any other files of note.

## Additional Possibilities

Keep up the great work if you've gotten this far by trying to:

- Summarize using `bedtools groupby`.
- Explore the `LADs_Kc.bed` annotation file.
- Find other datasets from GEP UCSC Genome Browser.

## Notes

1. `bedtools sort -i $FILE | sed -E '/chrUn|random/d'`

2. bedtools summary output columns ([source](https://github.com/arq5x/bedtools2/blob/master/src/summaryFile/summaryFile.cpp))

    - num_records — how many features are annotated on that chromosome
    - total_bp — how many basepairs are annotated on that chromosome (can be larger than the size of the chromosome due to overlapping features)
    - chrom_frac_genome — fraction of the genome that the entire chromosome represents (i.e. chromosome_bp / genome_bp)
    - frac_all_ivls — fraction of all features that are present on that chromosome (i.e. chromosome_features / genome_features)
    - frac_all_bp — fraction of all annotated basepairs on that chromosome (i.e. chr_ann_bp / gen_ann_bp)
    - min, max, mean — statistics for features on that chromosome

