# QBB2021 - Day 1 - Evening Exercise

For this assignment we will be working with a [.SAM file](https://samtools.github.io/hts-specs/SAMv1.pdf). SAM files normally begin with header lines which always begin with "@". These are followed by one line per read with the following columns:

|Col|Field|Type|Regexp/Range|Brief description|
|:--|:--|:--|:--|:--|
|1|QNAME|String|[!-?A-~]{1,254}|Query template NAME|
|2|FLAG|Int|[0, 216 − 1]|bitwise FLAG|
|3|RNAME|String|\*\|[:rname:∧*=][:rname:]*|Reference sequence NAME11|
|4|POS|Int|[0, 231 − 1]|1-based leftmost mapping POSition|
|5|MAPQ|Int|[0, 28 − 1]|MAPping Quality|
|6|CIGAR|String|\*\|([0-9]+[MIDNSHPX=])+|CIGAR string|
|7|RNEXT|String|\*\|=\|[:rname:∧*=][:rname:]*|Reference name of the mate/next read|
|8|PNEXT|Int|[0, 231 − 1]|Position of the mate/next read|
|9|TLEN|Int|[−231 + 1, 231 − 1]|observed Template LENgth|
|10|SEQ|String|\*\|[A-Za-z=.]+|segment SEQuence|
|11|QUAL|String|[!-~]+|ASCII of Phred-scaled base QUALity+33|

You will be working with a subset of reads so your code runs fast and will make debugging easier. First, make the folder `/Users/cmdb/qbb2021-answers/day1-evening`. Now you can use `samtools view` to convert the data from BAM to SAM format, followed by the `head` command to extract the first 10,000 lines.

```shell
$ samtools view -h /Users/cmdb/data/results/SRR072893.bam | head -n 10000 > /Users/cmdb/qbb2021-answers/day1-evening/SRR072893.sam
```

**Basic Exercises**

1. Count number of alignments
2. Count number of alignments that match perfectly to the genome (clipped reads don't count)
    - HINT: This is encoded in several ways, including the CIGAR string and [MD optional field](https://samtools.github.io/hts-specs/SAMtags.pdf).
3. Calculate average MAPQ score across all reads
    - HINT: think about string and numeric type conversions
4. Count number of reads that start their alignment on chromosome 2L between base 10000 and 20000 (inclusive)
5. Count how many potential PCR duplicates are present. These are reads that map to the exact same location. Let's assume there is no sequencing error (not a good assumption at all) so PCR duplicates will also have matching CIGAR strings. Also, remember that the first occurance of a read mapped to a given position is NOT a PCR duplicate, only subsequent reads mapped there.
    - HINT: The file is already sorted by coordinates

Submit **two** files to your GitHub repository:

- Python code that produces the answers (`day1-evening.py`)
- Your output (`day1-evening.out`)

Here's one way to catch the output if you use print statements without a file stream:

```shell
$ python day1-evening.py > day1-evening.out
```

**Advanced Exercises**

1. How many reads map to the reverse strand?
    - HINT 1: sam flag 0x10 bit
    - HINT 2: stackoverflow.com/questions/2591483/getting-a-specific-bit-value-in-a-byte-string
2. Determine how many reads have an average quality score >=30
    - HINT 1: fastq wiki phred+33
    - HINT 2: stackoverflow.com/questions/227459/ascii-value-of-a-character-in-python
3. Count the number of indels in mapped reads
    - HINT: This is encoded in the "CIGAR" field

If you do the advanced excercises, submit the **two** advanced files to your GitHub repository:

- Python code that produces the answers (`day1-evening_advanced.py`)
- Your output (`day1-evening_advanced.out`)
