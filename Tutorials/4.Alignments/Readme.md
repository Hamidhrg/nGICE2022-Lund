# Alignments

As Niklas explained this morning, in an alignment, each column is a homologous position in all the different sequences. In this exercise we are going to align the gene sequences you have obtained. To do so we will use one of the most common aligners in use presently, [MAFFT](https://mafft.cbrc.jp/alignment/software/). To do so you can call the program by typing `mafft` in the comandline (when this program is installed in your server).

Let first navigate into a folder named *Tutorial4* in `Users/Hamid/` where you have the result of your last practice (I have gathered all the results from all of you, and some more, here). Create a directory to store the sequence files called `ToAlign` in you own user account. You could probably remember that this can be done with the command `mkdir`. To do so remember to go back into your User directory. So your command should be something like the following:

```
mkdir ToAlign
```
And create a directory inside to store the alignments called `Aligned`:

```
mkdir ToAlign/Aligned
```

After you created these directories you should copy (cp command) all the files from `Users/Hamid/Tutorial4` to the `ToAlign` directory. Remember the syntax of `cp` command:

```
cp [PATH TO FILE YOU WANT TO COPY] [PATH TO WHERE YOU WANT TO COPY IT]
```

Now lets talk about the aligner we are going to use. The `mafft` program use the following syntax:

```
mafft [options] input > output
```

For the options we will be using an option telling the program to use the default parameters which are good enough for our simple examples. This option is defined by `--auto`. Another parameter we will be defining is the number of CPUs the command can use, you define that with `--thread` option. Here we will give the command `3` CPUs, so it will be `--thread 3`. The input is the relative (or absolute) path to your sequence file which you want to align. This is the same for the output. Here we will use the **output** to name the output file something informative, for example `[NAME OF THE GENE]_aligned.fa`. For example to align the *COI* genethe command you will be using should be the following:

```
mafft --auto --thread 3 COI.fa > Aligned/COI_aligned.fa
```

Now repeat this for every gene changing the gene names :)

When you have finished aligning every gene we are going to transfer the alignment files to our own computers using *FileZilla* and check the alignments using *Aliview*.



--------------------
## Extra Exercise
If you finished fast try to take a look at it in the class, if not check it after the course. 

You can do everything we did for each gene separately using a loop script. In the last step you have created a directory named `ToAlign`. Navigate into this directory and check the structure of it. While in the directory list and see the files. We could use the patterns you see here to write a script like the following:

```
#! /bin/bash

## We will use mafft
mkdir -p aligned

for gene in `ls ToAlign`;
do
	gene=${gene%%.fa}
	mafft --auto --thread 3 ToAlign/${gene}.fa > aligned/${gene}_alignedAgain.fa
done

```
Try to go through the different parts of the script and google the different parts to understand how it works.
