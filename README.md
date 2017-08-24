
NetCDF swap optimization for Little Endian machine

By historical reason, NetCDF stores arrays in Big Endian layout so data layout should be changed on Little Endian machine.
In old days when UNIX is used almost everywhere, it is not a problem since UNIX is Big Endian and there is no Endian swap is needed for this machine. But now almost all servers are running Linux which is Little Endian machine so this kind of Endian is some bottleneck for NetCDF.

NetCDF's own Endian swap routine is rude implementation and it is hard to vectorize.
So changing the default Endian swap routine with some bit operation will show better performance on Linux machine and could be vectorized with some compilers.

In NetCDF 4.x release, there is still OLD implementation of Endian swap routine in classic interface as well.
So you can apply patch file for NetCDF 3.6.3 version and/or NetCDF 4.4.1.1 version.

    $ cd /path/to/NetCDF_source/libsrc
    $ patch < netcdf_{NetCDF_version}_swap.patch


