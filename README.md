# ECLT
A software tool for exact computation of probability of population sequences under coalescent model

ECLT is a program that computes the exact coalescent likelihood for a set of aligned DNA sequences, assuming the infinite sites model. If you use this tool or want to know how exactly ECLT works, cite or read the following paper:

[1] Y. Wu, Exact Computation of Coalescent Likelihood for Panmictic and Subdivided Populations under the Infinite Sites Model, in IEEE/ACM Transactions on Computational Biology and Bioinformatics, vol. 7, no. 4, pp. 611-618, October 2010, doi: 10.1109/TCBB.2010.2.

For background, read the following books:

[2] J. Wakeley. Coalescent Theory: An Introduction. Roberts and Company Publishers, Greenwood Village, CO., 2008.

# Build ECLT
Building ECLT should be very easy. First decompress the code and type "make" to build the executable (under the main source directory). You may need to do "chmod" to make the executable have permission to run on your platform. That should be it!

# How to prepare input, run and get the results?

ECLT takes one input file, which contains the DNA sequences. Here is an example: 

0.0  0.2  0.4  0.6 0.8

00010

00010

00010

00000

00000

01100

10000

10001


First line: a list of positions (integer or fractions), showing the genomic positions of the sites. Right now, ECLT does not use this information, but can be useful in the future extensions.

Each DNA sequence should be listed in a single line, and also must be coded as binary (i.e. 0 or 1). Do not put spaces between the sites.

To run ECLT, you can start with:

./ECLT example-input.dat

Note that ECLT needs the mutation paramter, \theta. By default, \theta is set to 2.0. To choose your own \theta to say 4.0, use:

./ECLT -t4.0 example-input.dat

Moreover, ECLT also allows you to compute likelihood for a grid of points. For example, if you want to calculate likelihood for a grid of theta values, starting from 2.0, with increment of 0.1 and number of theta to be 20, use:

./ECLT -st2.0 -it0.1 -nt20 data.dat

Since computing exact likelihood is often memory intensive, ECLT allows you restrict the number of states to keep by -A<k> option. If this option is chosen, then ECLT aborts once the needed state is over the set threshold. For example, if you want to limit kept states to be under 60000, use:
./ECLT -A60000 data.dat

By default, the ancestral state (the root) of the genealogy is assumed to be the majority sequence: take the majority allele at each position. You can also set your own root by -R option. For example, if you want to set root to be 00100, use:
./ECLT -R00100 data.dat.

Be careful: you need to pick a valid root that satisfying the infinite site model. Also ensure the root is the same length as the input sequence.

At this moment, if you want to compute the likelihood for an unrooted tree, you need to manually add up likelihood for each possible root. In future releases, this will be  automatically done.


# Extensions      

Like program Genetree by Griffiths, ECLT has also been extended to support subdivided population. The model is the colored coalescent model.  The extension is more difficult to build, since it needs some third-party code. Source code available under request. Read my paper (Wu, TCBB, 2010) for more details.

# Contact      
Please send bug reports and technical questions to Yufeng Wu at 
<yufeng.wu@uconn.edu>.
