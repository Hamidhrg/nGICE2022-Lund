# **Reference Genetic Markers**

## **Alignments**

In the first tutorials you have learned the basics of working with different genetic file formats, how to run scripts on a server, a couple of ways to find your markers of interest, align the genetic markers and even you ran a script to assemble a genome (we killed the runs as it takes too much time for this workshop!). Now we are going to see how the reference markers can be created based on the published data for example. To do so we will download various gene sequences from [***NCBI***](https://www.ncbi.nlm.nih.gov/)'s Genbank and align them and create a consensus to use them as references.

In this practice we will go trough the first steps together, we will decide on which markers we can get and then I will give you some time until you have created the alignment for our genes of interest. Here I will not make a step by step guide for this part as you have already seen all of them.

## **Consensus Sequences**

For creating a consensus sequence from an alignment, we can use many tools. Geneious has a very useful application for creating consensus sequences, but it is not a program which is freely available. There exist many free alternatives, but maybe the best one is the command `ConsensusSequence()` from the DECIPHER library in R. You can also do so in other graphical programs as bioedit and seaview, but these applications usually represent limitations which limit the flexibility which is sometimes needed. Here we are going to use *EMBOSS*'s command called `cons`. The syntax of the command is as follows:

```
cons -sequence [PATH TO YOUR ALIGNMENT FILE] -outseq [PATH TO OUTPUT FILE]
```

This syntax include the two obligatory options which are the input and output options. Here we are going to use another option, `-name`. This option will create the header of the generated consensus fasta file. Here we will name it `GeneName_Reference`. For example the command for the gene `COI` should look somethinng like this:

```
cons -sequence COI_aligned.fa -outseq COI_consensus.fa -name COI_Reference
```

Go on and create a consensus for all your alignments. 

----------

As an extra exercise, you can think of writing a loop to create the reference consensus files in a bash script. If you run into problems ask us for help **tomorrow!*** :)
