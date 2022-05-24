
# **Dataset Generation**


Now you are quite used to work on the comandline, you know the basic bash commands and more importantly, you learned how to look for them online. You also learned about different sequence file formats, how to look for published genomes, download them and extract the markers you are interested in from them. You also know how to align these markers separately, and how to check the alignments manually afterwards. Now we want to merge these separate alignment files into a single file. 

When you append an alignment to the end of another one, where different markers from each organism come one after another, this process is called concatenation. To concatenate different alignment there are few different methods available. Each of them have some pros and some contras. Here we are going to use a program implemented in `BioPython` to do so. One of very useful features of this method is that it creates a `*.nex` alignment file, where you will get two different blocks. the first one will be the *Data* block or your final alignment, and the other block will be a *set* block. In this block the position range of each marker in the alignment will be defined. 

First of all, create a directory under your own name called `ToConcat`. Then `cd` into this directory and copy all the files inside the directory `Users/Hamid/Tutorial6/` in the `ToConcat` directory. This can be done by the following command for example:

```
cp ../../Hamid/Tutorial6/* .
```

These are the alignment we created yesterday, and cleaned. 

Now, go one level up:

```
cd ../
```

and run the following command to call the concatenation scripts with the proper arguments:

```
concat-aln ToConcat/ supergene
```

Running the concatenation script should create the file: `supergene.nex` in your current location. Use Filezilla as explained yesterday, and transfer this file to your own personal computer. Lets take a look at what it contains. Can you recognize the different blocks in it? Now open the concatenated alignment in `Aliview`. Take a look at the alignment, checke if there is any anomality or error in the alignment. Export the alignment by clickin on `File`--> `Save as Phylip (full names and padded)`. We will need the phylip format of the file also! Now I want you to open the nexus file again on a text editor on you own computer (`BBEdit` for mac users and `Notepad++` for windows). We want to create a file which keep the information of the different markers' position, for the program `IQTree`. The file should have the following format:

```
DNA , MarkerName1 = 1 - 69
DNA , MarkerName2 = 70 - 384
DNA , MarkerName3 = 385 - 662
DNA , MarkerName4 = 663 - 1001
```

Remember that what I wrote up there is an example! Use the information in the `set` block of the nexus file to create something similar to that and save it as `MyPartitions.txt`.

We will use these files with the program IQTree in the next practice. So transfer them in your user directory in the server using *FileZilla* again. We will use IQTree to construct phylogenies together. So please create a directory called `IQTreeAnalyses/` and a directory called `Run1` inside it. Also copy your phylip format concatenated alignment file into `Run1/`. Now that we are here, create another directory in `IQTreeAnalyses/` called `Run2` and copy your phylip format concatenated alignment and the `MyPartitions.txt` file into it. In the next tutorial, we will run the analyses together and I will explain the different components of the analysis. So if you have finished before the others... patience is a virtue! :)

