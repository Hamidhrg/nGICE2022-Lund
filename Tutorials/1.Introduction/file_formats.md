<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Common bioinformatics file formats](#common-bioinformatics-file-formats)
    - [Files to store sequence data](#files-to-store-sequence-data)
        - [fasta](#fasta)
        - [fastq](#fastq)
    - [Input/Output file formats for some phylogenetic software](#inputoutput-file-formats-for-some-phylogenetic-software)
        - [PHYLIP](#phylip)
        - [NEXUS](#nexus)
        - [Clustal](#clustal)
        - [newick](#newick)
    - [Unsorted](#unsorted)
        - [SAM/BAM](#sambam)

<!-- markdown-toc end -->

# Common bioinformatics file formats

Let's take a break from all this shell stuff and learn a little bit about some of the most common file formats useful for basic bioinformatics and some related to phylogenetic software. After learning these file formats we will do more shell learning with them.

Below you will see them grouped in arbitrary categories, but as you will soon notice, these categories are not mutually exclusive it is just a way of grouping them.


## Files to store sequence data


### fasta

Can only store sequence data and metadata

(information in the header, lines starting with `>`)

```text
>Sequence1|Information Can Have Spaces or|any_character
ATGCATGCATCTAGCTAGCTGCTAGCTAGCTTCTCTACGTAGCTGCTAGTTATGCTAG
ATCGATGCTAGCTACGTACGATATGCTGATCGTAGCTAGCTATCGCGCATCGAATCTA
ATGTGTGTGCATGCTACTTCTCTTCTTTTATAAATAGTCGTTGCAGTAGCTGTTGTAG
>Sequence2|Information_better_not_have_spaces
ATCGATGCTAGCTACGTACGATATGCTGATCGTAGCTAGCTATCGCGCATCGAATCTA
ATGCATGCATCTAGCTAGCTGCTAGCTAGCTTCTCTACGTAGCTGCTAGTTATGCTAG
ATGGGCGCGTATAACAAAACGTGTGTGCATGCTACTTCTCTTCTTTTATAAATAGTCG
>Sequence2a|same_as_above_but_one_line
ATCGATGCTAGCTACGTACGATATGCTGATCGTAGCTAGCTATCGCGCATCGAATCTAATGCATGCATCTAGCTAGCTGCTAGCTAGCTTCTCTACGTAGCTGCTAGTTATGCTAGATGGGCGCGTATAACAAAACGTGTGTGCATGCTACTTCTCTTCTTTTATAAATAGTCG
```


### fastq

In addition to the sequence data and header, confidence regarding the individual base calls can be stored.

```text
@SRR10859690.153 D00256:780:CBRY8ANXX:6:2210:14373:3531/1
TGCAGTCGTTGAGCATCCTCGCGGCTCCTCACCGCCCGAG
+
BBFFFFFFFFFBFFFFFFFFFFFFFFFFFFFFFBBFFFFF
```

Notice that sequence and quality lines (4th line above) are separated by `+`

```text
@HEADER
SEQUENCE
+
QUALITYS
```

But why?

A fastq file can have very long sequences (and therefore long quality lines as well). See the example below.

```text
@HEADER
SEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCE
+
QUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYS
```

In that case, it is allowed to have sequence and quality information spanning multiple physical lines in the file.

```text
@HEADER
SEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCE
SEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCE
SEQUENCESEQUENCESEQUENCESEQUENCESEQUENCESEQUENCE
+
QUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYS
QUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYS
QUALITYSQUALITYSQUALITYSQUALITYSQUALITYSQUALITYS
```

This makes a dedicated separator line necassary.


## Input/Output file formats for some phylogenetic software


### PHYLIP

This file format stores a multiple sequence alignment (MSA). The original and *strict* format needs that labels for the input sequences to have a fixed length of 10 and padded with spaces if the original text is shorter than this length. There are also "relaxed" versions where sequence labels are allowed to have any length.

Below is an example "strict" phylip file taken from [scikit-bio python package](http://scikit-bio.org/docs/0.4.2/generated/skbio.io.format.phylip.html)

          5    42
    Turkey    AAGCTNGGGC ATTTCAGGGT GAGCCCGGGC AATACAGGGT AT
    Salmo gairAAGCCTTGGC AGTGCAGGGT GAGCCGTGGC CGGGCACGGT AT
    H. SapiensACCGGTTGGC CGTTCAGGGT ACAGGTTGGC CGTTCAGGGT AA
    Chimp     AAACCCTTGC CGTTACGCTT AAACCGAGGC CGGGACACTC AT
    Gorilla   AAACCCTTGC CGGTACGCTT AAACCATTGC CGGTACGCTT AA

Of course, since this file stores aligned sequences, the part after labels need to have the same length as each other (although not limited to a specific bp of length).


### NEXUS

This is a very general file format that can hold various kinds of information in defined "blocks". It can store an alignment (in a "DATA" block), information about subsets of the alignment (partitions), a tree and other things.

    #NEXUS
    begin data;
    dimensions ntax=5 nchar=9332;
    format datatype=dna missing=? gap=-;
    matrix
    Epiphragma_mediale_SRR13856859         -----------caattcgatttaaat
    Euphylidorea_dispar_SRR11470044        --------nnnnnnnnnnnnnnnnnn
    Liogma_simplicicornis_SRR3441821       --------nnnnnnnnnnnnnnnnnn
    Metalimnobia_quadrinotata_SRR11948539  -----------caattcggtttaaat
    Nephrotoma_quadrifaria_SRR12518809     -----------caattcgatttaaat
    ;
    end;
    
    begin sets;
    charset aligned/16S_Ref = 1-1435;
    charset aligned/ND1_Ref = 1436-2407;
    charset aligned/ND5_Ref = 2408-4167;
    end;

This example file was cut in random places to fit to screen to give you an idea of the general file structure and not actually a valid file.


### Clustal

This is another file format to store MSAs. Sequence lines needs to be wrapped at 60th character.

    CLUSTAL W (1.82) multiple sequence alignment
    
    abc   GCAUGCAUCUGCAUACGUACGUACGCAUGCAUCA
    def   ----------------------------------
    xyz   ----------------------------------
    
    abc   GUCGAUACAUACGUACGUCGUACGUACGU-CGAC
    def   ---------------CGCGAUGCAUGCAU-CGAU
    xyz   -----------CAUGCAUCGUACGUACGCAUGAC

example taken from [scikit-bio python package](http://scikit-bio.org/docs/0.4.2/generated/skbio.io.format.clustal.html)


### newick

This is a standard plain-text format to store trees. Below is an example newick string and the represented tree in graphical representation, taken from [PHYLIP documentation](https://evolution.genetics.washington.edu/phylip/newick_doc.html)

    (((One:0.2,Two:0.3):0.3,(Three:0.5,Four:0.3):0.2):0.3,Five:0.7):0.0;

          +-+ One
       +--+
       |  +--+ Two
    +--+
    |  | +----+ Three
    |  +-+
    |    +--+ Four
    +
    +------+ Five

A dummy example explaining each element:

    ((Leaf1:length,Leaf2:length):internal_length,Leaf3:length):length_to_root;


## Unsorted


### SAM/BAM

SAM (Sequence Alignment/Map) is a tabular format that can hold extensive information about reads mapped to a reference sequence. Including the read's header (see the fastq example before), where in reference it mapped, if it was part of a pair, if it mapped in reverse strand, how many mismatches were there in the mapping, what was the read's sequence and quality information, etc.

It is hard to explain every field of this format here, but I suggest the interested reader to go to the [format specification](https://samtools.github.io/hts-specs/SAMv1.pdf) document and look at it.

here is an example staring with some header lines and ending with 4 reads' records

```text
@HD     VN:1.5  SO:unsorted     GO:query
@SQ     SN:ND5_Ref      LN:1734
@SQ     SN:COI_Ref      LN:1536
@SQ     SN:16S_Ref      LN:1386
@SQ     SN:ND4_Ref      LN:1340
@SQ     SN:CytB_Ref     LN:1137
@SQ     SN:ND2_Ref      LN:1038
@SQ     SN:ND1_Ref      LN:949
@PG     ID:bowtie2      PN:bowtie2      VN:2.4.5        CL:"/usr/local/sw/bowtie2-2.4.5-linux-x86_64/bowtie2-align-s --wrapper basic-0 -p 3 --very-sensitive-local -x /home/etka/workshop2022/map_to_reference/bwt-indices/MtRef7genes --passthrough -1 /home/etka/workshop2022/reads_fastq/SRR11470044/SRR11470044_1.fastq.gz -2 /home/etka/workshop2022/reads_fastq/SRR11470044/SRR11470044_2.fastq.gz"
SRR11470044.23045       83      ND4_Ref 318     22      8S66M77S        =       318     -157    TTTAGAAGAATAAATTTATTATTATTTTATTTATTTTTTGAAAGAAGATTAATTTCTACATTATTTTTAATTATGACACTGGTTAGGAGCCAGAGAACCGAACAAGTTTTGTTTGAATGAATTTTTGTTTTTGTTTATGCTTCGCTAATAC        JAJFJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJFJFFJJJJJJJJJJJJJJJJJJJJJJJ<JJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJ7JJJJJJFFFAA        AS:i:105        XN:i:1  XM:i:4  XO:i:0  XG:i:0  NM:i:4  MD:Z:12T33C1C2N14       YS:i:107       YT:Z:CP
SRR11470044.23045       163     ND4_Ref 318     22      14S66M71S       =       318     157     CTTACTTTTAGAAGAATAAATTTATTATTATTTTATTTATTTTTTGAAAGAAGATTAATTTCTACATTATTTTTAATTATGACACTGGTTAGGAGCCAGAGAACCGAACAAGTTTTGTTTGAATGAATTTTTGTTTTTGTTTATGCTTCGC        AAFFFJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJFFFFJFJFJJJ<JJJJFJJJJJJJJFFAFJJJFJJJJJ<JJJJ-AAJJJJJAJFJJ<JJJFJJJFAJJJFJF7AJJAJFJJJJJJJJJJJJJJJJAJJJJA<        AS:i:107        XN:i:1  XM:i:4  XO:i:0  XG:i:0  NM:i:4  MD:Z:12T33C1C2N14       YS:i:105       YT:Z:CP
SRR11470044.27307       83      COI_Ref 841     24      29S122M =       841     -153    TAAACATTTTAGTGAAAAATAGTGGACTTTTAGGATTTGTAGTGTGAGCTCATCATATATTTACCGTTGGTATAGATGTAGATACCCGTGCATATTTTACATCAGCAACAATAATTATTGCTGTTCCAACCGGAATCAAAATTTTTAGTTG        JJJFJFJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJFJJJJJJJJJJJJJJJJJJJJFFFAA        AS:i:153        XN:i:1  XM:i:12 XO:i:0  XG:i:0  NM:i:12 MD:Z:9A1T2N20A5A8T5T2A2T8T29T5T14     YS:i:149 YT:Z:CP
SRR11470044.27307       163     COI_Ref 841     24      31S120M =       841     153     AGTAAACATTTTAGTGAAAAATAGTGGACTTTTAGGATTTGTAGTGTGAGCTCATCATATATTTACCGTTGGTATAGATGTAGATACCCGTGCATATTTTACATCAGCAACAATAATTATTGCTGTTCCAACCGGAATCAAAATTTTTAGT        AAFFFJJJJJJJJJJJJJJJJJJJJJJJJJJJJJFFJJJJJJJFJFJFFJJJJJFJJJJJJJJJJJJJJJFAJJJJFJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJFJJJJJJJJJJJJJJJJJJJJJJJJFJJFJ        AS:i:149        XN:i:1  XM:i:12 XO:i:0  XG:i:0  NM:i:12 MD:Z:9A1T2N20A5A8T5T2A2T8T29T5T12     YS:i:153 YT:Z:C
```

and the BAM is the binary (non human readable) version of SAM that if sorted and indexed properly, allows for random access really fast. Like, getting all the reads that overlap with a certain reference sequence region and printing them. The program `samtools` can be used to do all these operations and the SAM->BAM conversion.
