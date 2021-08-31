# QBB2021 - Day 2 - Evening Exercise

## Heuristic sequence alignment

The first step in alignment algorithms like BLAST and FASTA is to find
candidate alignment "seeds" using a dictionary-like index. Here we will
implement the two first steps of such a matcher.

Start by creating the folder `/Users/cmdb/qbb2021-answers/day2-evening`.

## Data

Use `/Users/cmdb/qbb2021/data/droYak2_seq.fa` as your **query** sequence and `/Users/cmdb/qbb2021/data/subset.fa` from this afternoon as your **target** sequence. You can copy these directly to your answer directory like this:

```Bash
$ cp /Users/cmdb/qbb2021/data/droYak2_seq.fa /Users/cmdb/qbb2021-answers/day2-evening/
$ cp /Users/cmdb/qbb2021/data/subset.fa /Users/cmdb/qbb2021-answers/day2-evening/
```
## FASTA Reader

While in your `qbb2021-answers/day2-evening/` directory, `wget` the FASTA parser file we wrote together in the afternoon lecture.

```
wget https://raw.githubusercontent.com/bxlab/qbb2021/main/assignments/day2-homework/fasta_reader.py .
```

Then, you should import the function into your homework script using the following:

```python
from fasta_reader.py import FASTAReader
```

You would then have access to your `FASTAReader` function.

## Basic Exercise: Extend k-mer counter to k-mer matcher

Implement a script that finds matching _k_-mers between a single query
sequence and a database of targets. The matcher should take three
arguments:

```
kmer_matcher.py <target.fa> <query.fa> <k>
```

Where `target.fa` is the database containing one or more sequences,
`query.fa` is the sequence to align (assume just one sequnce), and
`k` is the _k_-mer size (an integer).

The script should find _k_-mer matches and for each write:

```
target_sequence_name    target_start    query_start k-mer
```

At the beginning of your python script, you should include the code below, which will get your query and target sequences with `FASTAReader`. You will not ever need to use `FASTAReader` yourself.

```
from fasta_reader import FASTAReader

# Load sequences
target_seqs = FASTAReader(open(target_fname))
query_seqs = FASTAReader(open(query_fname))
# We only need the first query sequence
query_seq = query_seqs[0][1]

# Loop through target_seqs
for ident, sequence in target_seqs:
...
```

### Submit
Run the program for `k=11` and submit:

1. your scripts (fasta parser and kmer_matcher)
2. the first 1000 lines of the script output

## Advanced Exercise: Extend matches

Based on your kmer matcher, create `kmer_match_extender.py` which for each
matched _k_-mer will extend downstream to find the longest exact match.
Print the matches ordered from longest to shortest. Do not report more than one sequence covering any given query position.

The script should write the following columns:

```
target_sequence_name    target_start    query_start k-mer
```

    - HINT: A k+1-mer will have a matching kmer at target t_pos and t_pos + 1 for q_pos and q_pos + 1.

If you really want a challenge, check for both forward and reverse-compliment query sequence k-mers and find the longest matches.
