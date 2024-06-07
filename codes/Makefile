.PHONY: run build clean

nproc?=1

run:
	cd apps/barnes && ./BARNES < inputs/n16384-p$(nproc)
	cd apps/fmm && ./FMM  < inputs/input.$(nproc).16384	
	cd apps/ocean/contiguous_partitions && ./OCEAN -p$(nproc)-n258
	#cd apps/ocean/non_contiguous_partitions && ./OCEAN -p$(nproc) -n4
	cd apps/raytrace && ./RAYTRACE -p$(nproc) -m64 inputs/car.env
	cd apps/water-nsquared && ./WATER-NSQUARED < inputs/n512-p$(nproc)
	cd apps/water-spatial && ./WATER-SPATIAL < inputs/n512-p$(nproc)
	cd kernels/cholesky && ./CHOLESKY -p$(nproc) < inputs/tk15.O
	cd kernels/fft && ./FFT -p$(nproc) -m16
	cd kernels/lu/contiguous_blocks && ./LU -p$(nproc) -n512
	cd kernels/lu/non_contiguous_blocks && ./LU -p$(nproc) -n512
	cd kernels/radix && ./RADIX -p$(nproc) n1048576
build:
	$(MAKE) -C apps/barnes
	$(MAKE) -C apps/fmm
	$(MAKE) -C apps/ocean/contiguous_partitions
	$(MAKE) -C apps/ocean/non_contiguous_partitions
	#$(MAKE) -C apps/radiosity
	$(MAKE) -C apps/raytrace
	#$(MAKE) -C apps/volrend
	$(MAKE) -C apps/water-nsquared
	$(MAKE) -C apps/water-spatial
	$(MAKE) -C kernels/cholesky
	$(MAKE) -C kernels/fft
	$(MAKE) -C kernels/lu/contiguous_blocks
	$(MAKE) -C kernels/lu/non_contiguous_blocks
	$(MAKE) -C kernels/radix

clean:
	$(MAKE) -C apps/barnes clean
	$(MAKE) -C apps/fmm clean
	$(MAKE) -C apps/ocean/contiguous_partitions clean
	$(MAKE) -C apps/ocean/non_contiguous_partitions clean
	$(MAKE) -C apps/radiosity clean
	$(MAKE) -C apps/raytrace clean
	$(MAKE) -C apps/volrend clean
	$(MAKE) -C apps/water-nsquared clean
	$(MAKE) -C apps/water-spatial clean
	$(MAKE) -C kernels/cholesky clean
	$(MAKE) -C kernels/fft clean
	$(MAKE) -C kernels/lu/contiguous_blocks clean
	$(MAKE) -C kernels/lu/non_contiguous_blocks clean
	$(MAKE) -C kernels/radix clean
