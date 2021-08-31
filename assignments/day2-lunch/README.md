# QBB2021 - Day 2 - Lunch Exercise
​
Frequently when dealing with annotation data we will need to translate
one set of identifiers to another according to a mapping. For example,
mapping gene identifiers to protein identifiers for searching a protein
database, or identifying orthologs using an existing orthology database
(e.g. Homologene).
​
Here you will implement a python program to perform such a mapping.
​
## Identifier mapping
​
We're going to be writing a Python script that combs through a file that contains gene IDs and using a second "mapping" file to convert these gene IDs to their corresponding protein IDs.

The file we'll be modifying is a `c_tab` file. The `c_tab` file contains information for a number of genes, including the gene's flybase ID. We want to retain the information for each gene, but convert these gene IDs to their corresponding protein IDs using the mapping file. The mapping file has two columns: the flybase gene ID followed by the UniProt ID. Your script should look through each line of the `c_tab` file and find the corresponding `gene_id` to `protein_id` translation from the mapping file. Finally, your script should print each new edited line, where each line contains all the info for that gene originally in the `c_tab` file, but which now contains the `protein_id` rather than the `gene_id`.

Write a python script (in TextMate) that takes in arguments from the command line. Your script should take three arguments: two files, and a third optional argument that will affect how it behaves.
​
  1. The mapping file `~/qbb2021/data/fly_mapping.txt`
  2. A `c_tab` file from StringTie
      * The `c_tab` file you will use for this exercise is `~/qbb2021/data/SRR072893.t_data.ctab`
  3. See below concerning this
​

Ideally, we'd be able to convert each flybase ID to it's corresponding UniProt ID, HOWEVER, not every flybase ID will be in the mapping file. If the flyabase ID is in the mapping file, your script should print the line from the `c_tab` file, replacing the `gene_id` field with the corresponding `protein_id` from the mapping file (**the UniProt Accession Number**). If the flybase ID is absent, your script should do one of two things depending on the value of the third argument to your function:
​
  1. If you do not pass a third argument to your script, then skip that line. For example, you would call your script with `python my_script.py ~/qbb2021/data/fly_mappping.txt ~/qbb2021/data/SRR072893.t_data.ctab`
  2. If you do pass a third argument, then replace the `gene_id` field with the third argument passed to your script. For example, if you call your script with `python my_script.py ~/qbb2021/data/fly_mapping.txt ~/qbb2021/data/SRR072893.t_data.ctab "missing"` then a line with a `gene_id` not present in the mapping file would have the `gene_id` field filled in with "missing".
​

**Hint:** recall that you’ll want to import sys at the beginning of your script. sys stores all the command-line arguments you pass to your script in a list called `sys.argv`.<br />
For example, if you ran a python script on the command line like this:`$ python myscript.py fly_mapping.txt t_data.ctab` <br />
Then: <br />
`sys.argv[1]` would give you `"fly_mapping.txt"` <br />
`sys.argv[2]` would give you `"t_data.ctab"` <br />
Note that both of these are **strings**!
​
## Advanced Exercise
​
The mapping file was parsed from a much less convenient source file. Download the source file using the following command:
​
```
$ wget "http://www.uniprot.org/docs/fly.txt"
```
​
When you examine the file, you'll see that it is not simply columns separated by tabs. The file has several lines at the top that we have to skip. Luckily the lines we care about all contain "DROME" (a code indicating that the gene originates from Drosophila melanogaster). Create a file containing 2 columns, the first with the flybase ID and the second with the UniProt Accession Number.
​
    - HINT: The columns are each a consistent width.
​
## Submit
​
**DO NOT git add, commit, or push the two input files!**
​
  - your Python script with any instructions needed to run it in a documentation comment
  - your identifier mapping output using each of the two options (in other words, both the output from running `python my_script.py ~qbb2021/data/fly_mappping.txt ~/qbb2021/data/SRR072893.t_data.ctab` and the output from running `python my_script.py ~qbb2021/data/fly_mappping.txt ~/qbb2021/data/SRR072893.t_data.ctab "missing"`)
​
  If you did the advanced exercise, also submit your parsing script.
