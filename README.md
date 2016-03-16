Splash-3 Benchmark Suite
========================

Splash-3 is a benchmark suite based on Splash-2 but without data races. It was
first presented at [ISPASS'16](TODO: Not available on IEEE just yet).

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

## Installation

There is no need to install Splash-3. All you need to do is set the `BASEDIR`
variable in `codes/Makefile.config` to point to the full path of the `codes`
directory.

## Tarballs

For tarball releases please visit our website at
[etascale.com](https://argodsm.com/vips%20coherence/splash-3.html).

## Citing Splash-3

To properly cite Splash-3 please cite our ISPASS'16 paper.

	C. Sakalis, C. Leonardsson, S. Kaxiras, and A. Ros, “Splash-3: A
	properly synchronized benchmark suite for contemporary research,”
	in Performance Analysis of Systems and Software (ISPASS), 2016
	IEEE International Symposium On, IEEE, 2016.

## Different Versions

The first release of Splash-3 is tagged as `v3.0`. Small fixes might be
published untagged on the master branch, as long as they do not significantly
affect the performance or other characteristics of the applications. If such
changes were to be published, then a new tag will be created and the master will
no longer be considered to contain version 3.0.

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
please contact Christos Sakalis directly.

---

[1] Steven Cameron Woo, Moriyoshi Ohara, Evan Torrie, Jaswinder Pal Singh, and
Anoop Gupta. 1995. The SPLASH-2 programs: characterization and methodological
considerations. In Proceedings of the 22nd annual international symposium on
Computer architecture (ISCA '95). ACM, New York, NY, USA, 24-36.
DOI=http://dx.doi.org/10.1145/223982.223990 
