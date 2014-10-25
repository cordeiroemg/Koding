
> Analysing GBS data with [Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml)

___

Bowtie 2 tutorial
---------------
___

>Bowtie 2 supports gapped, local, and paired-end alignment modes. Multiple processors can be used simultaneously to achieve greater alignment speed. Bowtie 2 outputs alignments in SAM format.

The difference between bowtie 1 and bowtie 2 is basically the reading length. Bowtie 1 was developed to align 50 pb reads whereas bowtie 2 can align up to 1000 characters long reads. Bowtie 2 handles better pair-ended sequences, has better report and mapping quality, allows overlapping non-quality read alignments. 

Bowtie 2 works best when aligning to large genomes, though it supports arbitrarily small reference sequences. If you are interested in short aliments, less say an amplicon or a chromosome, then tools like MUMmer, BLAST or Vmatch might be a better suit for you. 

##The bowtie 2 aligner
  
>"Alignment" is the process by which we discover how and where the read sequences are similar to the reference sequence. An "alignment" is a result from this process, specifically: an alignment is a way of "lining up" some or all of the characters in the read with some characters from the reference in a way that reveals how they're similar.

bowtie 2 has to mode:

 - *end-to-end alignment*: when all the characters in the read participate of the alignment
 - *local alignment*: when some of the characters at the ends of the read do not participate

#####Paired inputs
>Pairs are often stored in a pair of files, one file containing the mate 1s and the other containing the mates 2s. The first mate in the file for mate 1 forms a pair with the first mate in the file for mate 2, the second with the second, and so on. When aligning pairs with Bowtie 2, specify the file with the mate 1s mates using the -1 argument and the file with the mate 2s using the -2 argument. This causes Bowtie 2 to take the paired nature of the reads into account when aligning them.

###Reporting




    #!/bin/bash
    
    #Generate an index of your fasta genome in your ~/bowtie2_out directory
    
    /homes/bioinfo/bioinfo_software/bowtie2-2.1.0/bowtie2-build ~/bowtie2_out/tca_ref_Tcas_3.0_chrLG7.fa ~/bowtie2_out/tca_ref_Tcas_3.0_chrLG7_IDX
    
    #Generate a SAM file of the fastq reads aligned to your indexed genome in your ~/bowtie2_out directory
    
    /homes/bioinfo/bioinfo_software/bowtie2-2.1.0/bowtie2  -q -x ~/bowtie2_out/tca_ref_Tcas_3.0_chrLG7_IDX -U ~/bowtie2_out/Erick_7N.fastq -S ~/bowtie2_out/result_Alignment_Rd.sam


Using SAMtools:
view
>The view command filters SAM or BAM formatted data. Using options and arguments it understands what data to select (possibly all of it) and passes only that data through. Input is usually a sam or bam file specified as an argument, but could be sam or bam data piped from any other command. Possible uses include extracting a subset of data into a new file, converting between BAM and SAM formats, and just looking at the raw file contents. The order of extracted reads is preserved.
>>    #!/bin/bash
>
    /homes/bioinfo/bioinfo_software/samtools/samtools view -bS ~/bowtie2_out/result_Alignment_Rd.sam > ~/bowtie2_out/result_Alignment_Rd.bam




sort
>The sort command sorts a BAM file based on its position in the reference, as determined by its alignment. The element + coordinate in the reference that the first matched base in the read aligns to is used as the key to order it by. [TODO: verify]. The sorted output is dumped to a new file by default, although it can be directed to stdout (using the -o option). As sorting is memory intensive and BAM files can be large, this command supports a sectioning mode (with the -m options) to use at most a given amount of memory and generate multiple output file. These files can then be merged to produce a complete sorted BAM file [TODO - investigate the details of this more carefully].
 

     #!/bin/bash
        /homes/bioinfo/bioinfo_software/samtools/samtools sort ~/bowtie2_out/result_Alignment_Rd.bam ~/bowtie2_out/result_Alignment_Rd.sorted

Piped

  

     #!/bin/bash
     
            /homes/bioinfo/bioinfo_software/samtools/samtools view -Sb ~/bowtie2_out/result_Alignment_Rd.sam | samtools sort -o - - | samtools rmdup - - | samtools flagstat 


Alternativelly

    /homes/bioinfo/bioinfo_software/samtools/samtools view -Sb ~/bowtie2_out/result_Alignment_Rd.sam | /homes/bioinfo/bioinfo_software/samtools/samtools sort -o - - | /homes/bioinfo/bioinfo_software/samtools/samtools rmdup - - | /homes/bioinfo/bioinfo_software/samtools/samtools flagstat -

##Output
>3012562 + 0 in total (QC-passed reads + QC-failed reads)
0 + 0 duplicates
526 + 0 mapped (0.02%:-nan%)
0 + 0 paired in sequencing
0 + 0 read1
0 + 0 read2
0 + 0 properly paired (-nan%:-nan%)
0 + 0 with itself and mate mapped
0 + 0 singletons (-nan%:-nan%)
0 + 0 with mate mapped to a different chr
0 + 0 with mate mapped to a different chr (mapQ>=5)

