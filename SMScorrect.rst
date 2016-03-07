SMScorrect
============

Introduction
----------------------

Usage
~~~~~~~~~~~

A LR correction tool writed with C++.

Speed
~~~~~~~~~~

we compare three correct software of PBCR-MHAP, PBCR-SMSAligner and SMScorrect-SMSAligner and the previous software applied the same correct algorithm (falcon consense) by different overlap input result. The corrected LR size (correction size) of SMScorret is much bigger than PBCR-MHAP and PBCR-SMSAligner and the speed of SMScorrect is 4.75-15.64 times faster than PBCR- MHAP  in four real datasets (E.coli, Yeast, A.thaliana, D.melanogaster) and its speed is 4.4-7.69 times faster than PBcR-SMSAligner. Since the overlap input result of PBCR-SMSAligner and SMScorrect-SMSAligner is similar,  SMScorrect is about 7 times faster than falcon consense software. It is surprise that the human correct time is less than 2 days in 32 core computer and the correct speed is very fast.


Correctness
~~~~~~~~~~~~

Based on SMScorrect result, we applied some correct scripts from ftp://ftp.cbcb.umd.edu/pub/data/PBcR/validationScripts.tar.gz to evaluate SMScorrect program by two simualtion dataset (20x E.coli and Yeast) and two real datasets (E.coli and Yeast). 

In 20x simulation datasets, SMScorrect can reach 98.9% accuracy rate and 90% bases of dataset was corrected. In four real datasets, SMSCorrect can reach 99.7% accuracy rate and 98% bases of datasets was corrected. Since sequencing coverage of four real datasets is more than 50X coverage, SMScorrect can better performance. 

These result show that SMScorrect can gain about 99% accuracy and more than 90% total bases.



Instructions for use
~~~~~~~~~~~~~~~~~~~~~~


 ``$ SMScorrect –r [Sequences file name (fastq format)] -t [Number of CPUs] –p [number of corrected sequences] -m4 [output file name (m4 format)] -o [output file name]``

*Options*

::

  -t [number]: parallel CPU core number in the processing. This number should not exceed the logical CPU core numbers of all machines involved in the calculation.
  -o [output]: specify output file name.
  -m4 [m4 format]: specify output file name.
  -p [number]: number of corrected sequences in each correction.
  -r [sequence]: specify sequences file name (FASTA format).


Output
~~~~~~~~~~~~~~~


Each corrected sequence will be outputed as two lines in the result text file. Each line contains multiple fields separated by tab.

Line 1: >[corrected read number]_[corrected start position]_[corrected end position]

Line 2: The corrected sequence of this read.

Here is an example:

::

  >6_25_127

  ATATATTAAATTCGTAGTTACATAGGTAGGGTACAGATTCCGAATATATATGTTTATGCTTCCTTTAAGAATGACTGTCACAAGGTGTCACAGCTTATGCTAAGATATATATTTGGATGATTAATTTGTGATCTTTTGATTTGTCTAACCCAATATTCAAATATTGGTCCATCGTTTATCG


Notices
~~~~~~~~~~

*Memory consumption:*

Calculated by correcting 200000 sequences each time.

::

  Memory consumtion of data compression and loading into memory = amount of original data* 0.25 (i.e. the amount of human data is 160G, then memory consumption required is 40G)

  Running of correction (maximum) = 0.5G*(number of CPUs)

