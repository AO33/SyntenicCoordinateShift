This jupyter notebook/project is essentially a set of functions that will allow for the conversion of one genomes coordinates to another via their syntenic relationship (if it exists)

The program utilizes the syntenic alignment outputs from the program Satsuma to shift coordinates from one genome to another.
Syntenic blocks between the two input genomes are found and defined by Satsuma and written out to two main files...
satsuma_summary.chained.out - The most succinct version of the sytenic blocks with only the coordinates and orientation of the two regions with respect to eachother.
MergeXCorrMatches.chained.out - The same information as the summary.chained.out file, but contains the actual alignment that was found between the two regions. This is the file that is used as input into the coordinate shifting algorithm.

The program works in two steps (with a bit more detailed descriptions later in the notebook) -

Read the reference genome scaffold/chromosome sequences into memory (fastaFilePaths)
Read the MergeXCorrMatches.chained.out file into memory in the form of two interval trees (one for each target and queary genomes) with adjusted genomic coordinates based on the reference genomes
Queary any given Chromosome,position in one genome to find the sytenic region and corresponding base pair in the other genome. There are two functions that accomplish this...
-The first is quearyTree wich will identify the sytenic region/block(s) that the position falls within.
-The second is quearySynBlock which will take the SynBlock object found in the first function, and find the coordinate/base pair information found between genome1 and genome2.
Essentially, the first step of the algorithm takes about 5-10 minutes to run depending on the machine but only needs to be run once eachtime the notebook/script is opened. Then all point quearies are super fast.
The alternative to this would be a database, but there are numerous reasons why we chose not to go that route
