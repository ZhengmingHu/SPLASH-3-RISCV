Splash-3 Benchmark Suite
========================

Splash-3 is a benchmark suite based on Splash-2 but without data races. It was
first presented at [ISPASS'16](TODO: Link to IEEE when possible).

The version found here is a refined version of the one used in the ISPASS paper.
The main difference is that it is based on the [Modified
Splash-2](http://www.capsl.udel.edu/splash/index.html) suite, which, among other
things, fixes issues related to running Splash-2 on x86-64, as well as lots of
warnings.  While working on the release version of Splash-3 we realized that we
are duplicating a lot of the effort already taken by Modified Splash-2, so we
decided to port our Splash-3 patchset on top of Modified Splash-2. 

Modified Splash-2 also changes every `int` to `long`, which is something that we
only partially did for the version discussed in the paper, so we do expect some
differences in the memory footprint of the applications. However, everything
else, such as the algorithms or the synchronization characteristics of the
applications remain unchanged, making the overall performance difference between
this version and the ISPASS version minimal.

## Citing Splash-3

To properly cite Splash-3 please cite our ISPASS'16 paper.

	TODO: Add citation and bibtex (not yet published at this time)

## Different Versions

As of this time, the head of the master branch contains the Splash-3 code. If
changes that significantly affect the synchronization or performance
characteristics are made, the last Splash-3 version will be taged as `v3.0` for
convenience.

It is also possible to access the original and the Modified Splash-2 codes.
They are tagged as `v2.0` and `v2.0M` respectively.

## Recommended Inputs

The following are the recommended inputs for running Splash-3 in a simulator.
The symbol '#' is a placeholder for the number of threads. These inputs are
based on the original Splash-2 characterization paper by Woo et al. [1].

	apps/barnes/BARNES < inputs/n16384-p#
	apps/fmm/FMM < inputs/input.#.16384
	apps/ocean/contiguous_partitions/OCEAN -p# -n258
	apps/ocean/non_contiguous_partitions/OCEAN -p# -n258
	apps/radiosity/RADIOSITY -p # -ae 5000 -bf 0.1 -en 0.05 -room -batch
	apps/raytrace/RAYTRACE -p# -m64 inputs/car.env
	apps/volrend/VOLREND # inputs/head
	apps/water-nsquared/WATER-NSQUARED < inputs/n512-p#
	apps/water-spatial/WATER-SPATIAL < inputs/n512-p# 
	kernels/cholesky/CHOLESKY -p# < inputs/tk15.O
	kernels/fft/FFT -p# -m16
	kernels/lu/contiguous_blocks/LU -p# -n512
	kernels/lu/non_contiguous_blocks/LU -p# -n512
	kernels/radix/RADIX -p# -n1048576

## Removing the locks around some of the "benign" races

Due to popular demand, some of the locks around some of the "benign" assignment
races have been marked as optional. If you want to disable those locks, pass the
option `-DWITH_NO_OPTIONAL_LOCKS` to the compiler. **IT IS HIGHLY DISCOURAGED TO
DO SO. The applications have not been tested without those locks, and even the
"benign" data races can cause undefined behavior.**

## Original source code from the ISPASS'16 paper

If you are interested in the exact source code used for the ISPASS'16 paper,
please contact me.

---

[1] Steven Cameron Woo, Moriyoshi Ohara, Evan Torrie, Jaswinder Pal Singh, and
Anoop Gupta. 1995. The SPLASH-2 programs: characterization and methodological
considerations. In Proceedings of the 22nd annual international symposium on
Computer architecture (ISCA '95). ACM, New York, NY, USA, 24-36.
DOI=http://dx.doi.org/10.1145/223982.223990 
