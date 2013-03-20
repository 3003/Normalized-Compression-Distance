#Normalized Compression Distance#
Experiments and research into Normalized Compression Distance (NCD).

##What is NCD?##
NCD, in layman terms, works on the principle that two files which share data patterns compress better when you add them together, than two files which don't share data patterns, since compressors are more efficient when dealing with repeating data patterns.

###Very simple example###
File A contents

	CCCCCCCCCCCC
	
File B contents

	CCCCCCCCCCCA
	
File C contents

	AAAABBBBBBPQ

Using a very basic compressor called a Run-Length Encoder (RLE) we can compress these file contents.

File A contents compressed

	12xC
	
File B contents compressed

	11xC,A
	
File C contents compressed

	4xA,6xB,PQ

To get a similarity measure between files, you add two files together and look at the length of their compression.

File A contents + File B contents

	CCCCCCCCCCCCCCCCCCCCCCCA
	
File A + File B compressed

	23xC,A
	
Which gives a compressed length of 6.

File B contents + File C contents

	CCCCCCCCCCCAAAAABBBBBBPQ

and File A + File B compressed
	
	11xC,5xA,6xB,PQ
	
Which gives a compressed length of 10.

As the files are already of equal length, we don't need normalization to spot that File A and File B are more alike, than File B and File C.

NCD is an approximation. We would like to use the Kolmogorov Complexity (KC) for a string, but KC is incomputable. Better compressors are valuable to increase NCD's accuracy and AI in general, so much so that Marcus Hutter made a price for it [50'000€ Prize for Compressing Human Knowledge](http://prize.hutter1.net/)

###Uses of NCD###
NCD gives a similarity measure between two files or data streams which can be used to cluster, classify, compare, or even fed to autonomous agents.

##clusterchessgames.py##
###description###
Clusters 21 files containing game data from 7 Grandmasters. All games played a Grandmaster with white are stored inside a .txt file. This .txt file is split up in 3 smaller .txt files, which are randomized and stripped of meta-data (like the dates, locations, tournament or player names). 

The challenge is to create 7 clusters containing the game data files belonging to the same Grandmaster. Opponents moves are kept inside the data, which makes less of the data indicative of the Grandmaster's patterns we hope to find. This adds to the challenge.

Expert knowledge or chess domain knowledge isn't required for good results.
###dependancies###
datetime, pprint, random, glob, itertools, and at least one of the following compression libs: zlib, bz2, lzo, pylzma

###sample output###
Using the following 7 Grandmasters, inspired by some of Fischer's favorite opponents:
- (A) Gligoric
- (B) Petrosian
- (C) Reshevsky
- (D) Spassky
- (E) Tal
- (F) Botvinnik
- (G) Larsen

this script gives us the following clusters, together with their fitness/similarity score:

	Using compressor: bz2
	(0.9187782850134746, 'data/chessgames\\C1_.txt', 'data/chessgames\\C2_.txt', 'data/chessgames\\F1_.txt')
	(0.9213097232083918, 'data/chessgames\\D2_.txt', 'data/chessgames\\E1_.txt', 'data/chessgames\\E2_.txt')
	(0.9255006608357625, 'data/chessgames\\B1_.txt', 'data/chessgames\\B2_.txt', 'data/chessgames\\B3_.txt')
	(0.9275354033562815, 'data/chessgames\\G1_.txt', 'data/chessgames\\G2_.txt', 'data/chessgames\\G3_.txt')
	(0.9286958400620074, 'data/chessgames\\A1_.txt', 'data/chessgames\\A2_.txt', 'data/chessgames\\A3_.txt')
	(0.931262816636599, 'data/chessgames\\C3_.txt', 'data/chessgames\\F2_.txt', 'data/chessgames\\F3_.txt')
	(0.9343742509153218, 'data/chessgames\\D1_.txt', 'data/chessgames\\D3_.txt', 'data/chessgames\\E3_.txt')
	Script execution time: 0:00:37

Preliminary observations: Bz2 outperforms other compressors with regards to speed and accuracy. Clustering 15 files or less often results in perfectly correct clusters. Clustering 24 files or more starts to give poor results.

TODO: Look if it is possible to use other cluster algorithms, like k-means, and subdivide the larger clusters using NCD-based clustering.