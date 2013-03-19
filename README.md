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