
> Analysing GBS data with [Stacks](http://creskolab.uoregon.edu/stacks/)

___

STACKS tutorial
---------------
___
>Stacks is a software pipeline for building loci from short-read sequences, such as those generated on the Illumina platform. Stacks was developed to work with restriction enzyme-based data, such as RAD-seq, for the purpose of building genetic maps and conducting population genomics and phylogeography.

This tutorial will be divided in two parts:

 1. Population genomics
 2. Genetic map
___
___


## denovo_map.pl ##
This program perform a sequence of steps:

ustacks: The unique stacks program will take as input a set of short-read sequences and align them into exactly-matching stacks.
    Comparing the stacks it will form a set of loci and detect SNPs at
    each locus using a maximum likelihood framework (Hohenlohe et al.,
    2010).

`ustacks -t file_type -f file_path [-d] [-r] [-o path] [-i id] [-m min_cov] [-M max_dist] [-p num_threads] [-R] [-H] [-h]`
       

cstacks: A catalog can be built from any set of samples processed by the ustacks or pstacks programs. It will create a set of consensus loci, merging alleles together. In the case of a genetic cross, a catalog would be constructed from the parents of the cross
    to create a set of all possible alleles expected in the progeny of
    the cross.

 `cstacks -b batch_id -s sample_file [-s sample_file_2 ...] [-o path] [-n num] [-g] [-p num_threads] [--catalog path] [-h]`

 sstacks: Sets of stacks constructed by the ustacks or pstacks programs can be searched against a catalog produced by cstacks. In  the case of a genetic map, stacks from the progeny would be matched against the catalog to determine which progeny contain which parental alleles.

Running the denovo_map.pl program 

`denovo_map.pl -p path -r path [-s path] -o path [-t] [-m min_cov] [-M mismatches] [-n mismatches] [-T num_threads] [-A type] [-O popmap] [-B db -b batch_id -D "desc"] [-S -i num] [-e path] [-d] [-h]`

submitting the job as:

```
#!/bin/bash

qsub -l h_rt=00:10:00 -l mem=10G -pe single 1 /homes/cordeiroemg/Rd_seq/denovo_stacks.sh
```
The pipe the run *denovo_map.pl* is:

``````denovo_map.pl \
 -D "Population RAD-Tag Samples" \
 -o ./stacks \
 -s ./homes/cordeiroemg/Rd_seq/Erick_7N.fastq \
 /homes/cordeiroemg/Rd_seq/Erick_T1.fastq
``````

>-D is a description
>-o is the output path
>-s is the sample path to be processed


##References

Hohenlohe PA, Bassham S, Etter PD, Stiffler N, Johnson EA, Cresko WA. 2010. Population genomics of parallel adaptation in threespine stickleback using sequenced RAD tags. PLoS Genetics, 6(2):e1000862.

