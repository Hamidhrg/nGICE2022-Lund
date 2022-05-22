<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Shell exercises with example bioinformatics files](#shell-exercises-with-example-bioinformatics-files)
    - [Copying the necessary files to your user directory](#copying-the-necessary-files-to-your-user-directory)
    - [Extracting the contents](#extracting-the-contents)
    - [Inside the directory](#inside-the-directory)
    - [Searching and extracting text](#searching-and-extracting-text)
    - [Scripting exercise](#scripting-exercise)
        - [Your aim](#your-aim)

<!-- markdown-toc end -->

# Shell exercises with example bioinformatics files

We will continue to learn about different shell commands using example files of common formats. Before we start, [here](https://s3.studylib.net/store/data/008273231_1-984843cfa9ca53b32206e54ece8487ba-768x994.png) is a cheat sheet for some common shell commands or operations. If you need to quickly refer back to some command. For more detailed explanation of what a line of command does you can use [this](https://explainshell.com) website. If you paste your command (try one of the commands we covered in the basic part above) it will break it down to the commmand and the arguments used and what they each mean.


## Copying the necessary files to your user directory

There is a zip file called `shell_exercise_data.zip` under `/home/workshop/Users/Etka`. This is a zipped folder containing all the necessary files we are going to work with. Copy this file into your own user directory (`/home/workshop/Users/yourName`)


## Extracting the contents

We will need to extract the contents of this file to be able to access them. Before doing that you can check the file contents by using `less`.

```bash
less shell_exercise_data.zip
```

Now, we can extract this zip archive. You can look at the cheat sheet provided to find out how to uncompress a `.zip` file under linux. Or you can use your favorite search engine.


## Inside the directory

After uncompressing, run `ls` to see if there are any new files or directories in your current working directory. You should see a single folder. Go there and run `ls` once again to see what we've unraveled from this zip file.

```bash
cd example_data
ls
```

There are several files with different file extensions. Some end with `.fa` and some `.tsv`

To see a long list format (one file per line) using ls do this:

```bash
ls -lh
```

    total 36M
    -rw-rw-r-- 1 etka etka  12M maj 21 13:24 Hylephila_phyleus.fa.gz
    -rw-rw-r-- 1 etka etka 621K maj 21 13:27 Hylephila_phyleus_report.tsv
    -rw-rw-r-- 1 etka etka  12M maj 21 13:29 Semomesia_campanea.fa.gz
    -rw-rw-r-- 1 etka etka 583K maj 21 13:30 Semomesia_campanea_report.tsv
    -rw-rw-r-- 1 etka etka  11M maj 21 13:25 Urbanus_proteus.fa.gz
    -rw-rw-r-- 1 etka etka 637K maj 21 13:26 Urbanus_proteus_report.tsv

You can use the [website](https://explainshell.com) I gave you to check what this command does in detail. The names you see before the suffixes `.fa.gz` and `_report.tsv` are 3 different buttterfly names.

Let's first move these file pairs into their dedicated directories to have a much cleaner file structure.

let's first create directories (using the `mkdir` command) for each:

```bash
mkdir Urbanus_proteus
mkdir Hylephila_phyleus
mkdir Semomesia_campanea
```

or in a much more compact way:

```bash
mkdir Urbanus_proteus Hylephila_phyleus Semomesia_campanea
```

Now we can move every file to where it belongs. We can use `mv`

```bash
mv file1 directory1/
```

will move the `file1` under `directory1/`. But we have 6 different files! We can cut our effort in half by just running the `mv` command 3 times instead of 6. We can say the shell "move every file that starts with Urbanus\_proteus to the directory with the same name" and to the same for remaining two species

```bash
mv Urbanus_proteus* Urbanus_proteus/
mv Semomesia_campanea* Semomesia_campanea/
mv Hylephila_phyleus* Hylephila_phyleus/
```

The asterisk character (`*`) here means any other text can appear after it. So it will match everything starting with your species name.

You will see the shell nagging you saying that it couldn't move some files. Since the directory names also start with our species names, it tries to move the directories under themselves! Silly shell :)

But don't worry, now you should have everyting under the right directory. One more check:

```bash
ls -lh
```

    total 12K
    drwxrwxr-x 2 etka etka 4,0K maj 21 14:32 Hylephila_phyleus
    drwxrwxr-x 2 etka etka 4,0K maj 21 14:32 Semomesia_campanea
    drwxrwxr-x 2 etka etka 4,0K maj 21 14:32 Urbanus_proteus

Choose one of the species and go to its directory:

```bash
cd Urbanus_proteus
```

And look into the `.fa.gz` file:

```bash
less Urbanus_proteus.fa.gz
```

It contains transcript sequences from this species.

Also look at the `_report.tsv` file for your selected species.

```bash
less Urbanus_proteus_report.tsv
```

Lines look all jumbled together? Try this:

```bash
less -S Urbanus_proteus_report.tsv
```

    # BUSCO version is: 5.2.2 
    # The lineage dataset is: lepidoptera_odb10 (Creation date: 2020-08-05, number of genomes: 16, number of BUSCOs: 5286)
    # Busco id      Status  Sequence        Score   Length  OrthoDB url     Description
    0at7088 Missing
    1at7088 Duplicated      TRINITY_DN429_c0_g1_i10:1722-16133      9217.8  4980    https://www.orthodb.org/v10?query=1at7088       titin
    1at7088 Duplicated      TRINITY_DN429_c0_g1_i11:398-19228       8415.1  5629    https://www.orthodb.org/v10?query=1at7088       titin
    1at7088 Duplicated      TRINITY_DN429_c0_g1_i12:398-18904       8407.1  5784    https://www.orthodb.org/v10?query=1at7088       titin
    1at7088 Duplicated      TRINITY_DN429_c0_g1_i9:398-18941        8407.0  5784    https://www.orthodb.org/v10?query=1at7088       titin
    2at7088 Missing
    3at7088 Complete        TRINITY_DN550_c0_g1_i1:1137-23984       10752.5 5597    https://www.orthodb.org/v10?query=3at7088       nesprin-1 isoform X1
    4at7088 Complete        TRINITY_DN5304_c0_g1_i11:1-14946        7630.3  4228    https://www.orthodb.org/v10?query=4at7088       uncharacterized protein LOC11038103

Now, it should look much better. This file contains some information about the search of set of genes in the respective .fa file. Columns are separated with tabs. You can see what each column corresponds to by reading the column names in the 3rd line.


## Searching and extracting text

Come to the `Urbanus_proteus` directory (if you selected another species for the previous steps) with me:

```bash
cd ../Urbanus_proteus/
```

Here in the path above `../` corresponds to the *parent directory* of what you currently are.

The report table essentially lists results for each gene (here denoted Busco id) line by line. In the second line of the file it says: "number of buscos: 5286". Let's check this by using our linux-fu skills!

Let's first try checking how many lines this file have.

We will use the program `wc` (short for word count) for this:

```bash
wc -l Urbanus_proteus_report.tsv
```

    5871 Urbanus_proteus_report.tsv

It says there are more lines than there are genes. How come? Including the 3 header lines at the beginning we would expect this file to have 5289 lines.

Look at the file again if you didn't catch the problem:

```bash
less -S Urbanus_proteus_report.tsv
```

There are lines starting with the same gene id! In fact you can see the remark "Duplicated" printed for genes that have multiple lines. Let's be sure that if we count the duplicated lines only one time, there are correct number of lines (5289). To do that first we will extract the first two columns from this "table".

```bash
cut -f1,2 Urbanus_proteus_report.tsv
```

If you want to see if the general format of the output is correct before you actually run your command and fill out your entire screen with output lines, try this:

```bash
cut -f1,2 Urbanus_proteus_report.tsv | head
```

Similar to the redirection (`command > output.txt`) feature we've learned at the beginning. It is also possible to feed the output from one command into another easily by combining two commands with the pipe (`|`) character. `head` is a different command that just prints out first 10 lines of a file (or the input piped into it) try this with the original file:

```bash
head Urbanus_proteus_report.tsv
head Urbanus_proteus_report.tsv | wc -l
```

`wc` can also accept input piped into it!

coming back to column extraction:

```bash
cut -f1,2 Urbanus_proteus_report.tsv | head
```

now, we need a way to de-duplicate lines that have the same exact content.

```bash
cut -f1,2 Urbanus_proteus_report.tsv | head | uniq
```

    # BUSCO version is: 5.2.2 
    # The lineage dataset is: lepidoptera_odb10 (Creation date: 2020-08-05, number of genomes: 16, number of BUSCOs: 5286)
    # Busco id      Status
    0at7088 Missing
    1at7088 Duplicated
    2at7088 Missing
    3at7088 Complete

We got rid of the repeating `1at7088` lines! Remember that for the uniq command to work properly, it expects a sorted input. It just deletes neighboring repating lines. But since here the first two column data was already sorted according to busco id, so we are fine.

Now lets feed the de-duplicated first two columns directly into wc (without the head in between)

```bash
cut -f1,2 Urbanus_proteus_report.tsv | uniq | wc -l
```

Sweet!

Let's now try to get only the 2nd column:

```bash
cut -f 2 Urbanus_proteus_report.tsv | head
```

Let's try to find out how many different categories are there and how many rows belong to each category:

```bash
cut -f 2 Urbanus_proteus_report.tsv | sort | uniq -c
```

       1 # BUSCO version is: 5.2.2 
    3025 Complete
    1028 Duplicated
     263 Fragmented
    1552 Missing
       1 Status
       1 # The lineage dataset is: lepidoptera_odb10 (Creation date: 2020-08-05, number of genomes: 16, number of BUSCOs: 5286)

giving the "-c" (count) argument to `uniq` prints out a nice count for each unique entry. Since we didn't remove the first three header lines, they also appear in the result.

What if we didn't know that this file was formatted nicely and all the gene status information is in the 2nd column? We could've just used a basic text search method inside the file using the command `grep`

Let's try it with the keyword "Complete" on the first 50 lines of this file:

```bash
head -n 50 Urbanus_proteus_report.tsv | grep "Complete"
```

try the same command with `grep -c` and `grep -o` instead of just just writing grep. Observe the behaviour.

It is also possible to do an *inverse search* using grep, meaning getting every line that **does not match** your search term using `grep -v`. Try this too.


## Scripting exercise

Here we will work with combining what we have learned and use it to write a *script*, which essentially a file with lines of shell commands that is executed line after another by the shell.

Before putting our commands into a script, we need to experiment with the different commands and think about what we're going to do with each step.


### Your aim

For each of the three species, lines of the `*_report.tsv` file have information about whether a particular gene was found in the transcriptome fasta files of the species.

Let's remember how the report file looked like:

    3at7088 Complete        TRINITY_DN550_c0_g1_i1:1137-23984       10752.5 5597    https://www.orthodb.org/v10?query=3at7088       nesprin-1 isoform X1
    4at7088 Complete        TRINITY_DN5304_c0_g1_i11:1-14946        7630.3  4228    https://www.orthodb.org/v10?query=4at7088       uncharacterized protein LOC110381036
    33at7088        Complete        TRINITY_DN5904_c0_g1_i1:1-2460  1651.8  752     https://www.orthodb.org/v10?query=33at7088      transformation/transcription domain-ass34at7088        Complete        TRINITY_DN44655_c0_g1_i1:6-6089 3679.6  1759    https://www.orthodb.org/v10?query=34at7088      uncharacterized protein KIAA1109
    36at7088        Complete        TRINITY_DN4786_c0_g1_i1:2-7039  3292.0  2031    https://www.orthodb.org/v10?query=36at7088      histone-lysine N-methyltransferase trit43at7088        Complete        TRINITY_DN54294_c0_g1_i1:2-2587 1998.2  824     https://www.orthodb.org/v10?query=43at7088      histone-lysine N-methyltransferase 2C-l49at7088        Complete        TRINITY_DN12678_c0_g1_i1:62-739 457.9   221     https://www.orthodb.org/v10?query=49at7088      hemocytin
    66at7088        Complete        TRINITY_DN1069_c0_g1_i1:122-7243        4137.9  1873    https://www.orthodb.org/v10?query=66at7088      Pre-mRNA-processing-splicing fa68at7088        Complete        TRINITY_DN23332_c0_g1_i1:0-854  652.7   271     https://www.orthodb.org/v10?query=68at7088      protein furry isoform X1

We've covered the first two columns. The third column is the specific sequence in which the program could find the searched gene. It has the following format:

    sequence_name:start-end

So, not every gene that is found spans the entire `.fasta` entry (a transcript, in this case).

Our task is to extract the sequences (using the span information in the table) from the fasta file for only the "Complete" genes.

-   filter the `_report.tsv` file so that it only contains lines that have the value "Complete" in their second column. Write the result to a file
-   find how to tell `grep` to print the line number (where there was a match) alongside the matched line itself. use this information to print out the line numbers (locations in the file) for the header lines of the fasta. Write the result to another file. Your file should look like this:

    1:>TRINITY_DN54622_c0_g1_i1 len=877 path=[0:0-876]
    17:>TRINITY_DN54606_c0_g1_i1 len=165 path=[0:0-164]
    21:>TRINITY_DN54606_c1_g1_i1 len=348 path=[0:0-347

this information essentially tells you the start and end locations(line-wise) of a transcript within the transcriptome fasta file. For instance, if we want to extract the first gene we need the lines 1-16 of this file.

-   find how to extract a range of lines from a text file using the shell. (Hint: you can do this with appropriate arguments to the program `sed`). To avoid having the headers, you can start a line after where the header is. You should be able to extract a region from the fasta file that corresponds to the sequence of one gene.
-   Now, try to find out how to extract a range of characters from a line. This can be done with `cut -c` (google it) but all the sequence should be in the same physical line for this to work. To delete any line breaks from a file (or data coming through a pipe) we can use `tr -d`. You can google it to find out how to use it.
-   Combine all of these using pipes to extract the sequence for the first gene in the file. A pseudocode of what you will do is shown here: `extract lines m through n of fasta | remove line breaks | get letters (characters) n to m from this single line > extracted_gene.fa`
-   BONUS: Learn how to use loops in bash and loop through every gene in the completed genes list you created to do the above step. (remember to use `>>` instead of `>` so that you don't overwrite the existing data you have on your output file
