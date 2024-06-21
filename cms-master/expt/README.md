# Example running CMS

This directory contains example input files for running `getdata` and `cms`, which can be adapted for your own use.
To check that your installation of CMS has worked correctly, you can also use these files to run a simple test.

## Working directory

First, make sure you are in the directory expt/.
You should see the directories input_getdata_example/ and input_example/.

## Create links

Second, create links to the executables `cms` and `getdata` by typing:

```bash
ln -s ../src/cms cms
ln -s ../src/getdata getdata
```

## Run `getdata`

Run `getdata` to download oceanographic files needed to run the test by typing:

```bash
./getdata getdata_example 1
```

This will download and format 13 days (1-13 Jan 2016) of surface ocean current data from the [HYCOM global analysis](https://hycom.org/data/glbu0pt08/expt-91pt1).
The resulting formatted nest files will be placed in a new directory: expt_getdata_example/nests/.

## Move nest files

Either move or create a link to the nest files in expt_example/ by typing:

```bash
mv expt_getdata_example/nests expt_example/nests      
```

or:

```bash
ln -s expt_getdata_example/nests expt_example/nests
```

## Run `cms`

Run `cms` using the example input files in input_example/ by typing:

```bash
./cms example
```

If MPI is enabled, run `cms` like this:

```bash
mpirun -n 2 ./cms example
```

In this case, `cms` is run passively for 3 particles released on 3 consecutive days, with no turbulence or IBM.
If the test has worked correctly, you should get an output file called traj_file_1.nc in expt_example/output/.
An example output file for the test is given in expt_example/example_output/ called traj_file_example.nc with which to compare your results.
In this case, all 3 particles leave the nest domain at its northern edge (30 degrees N), giving exit code -1:

```
lat:
25			25			25
26.0429439544678	25.9986038208008	25.9510612487793
27.2221393585205	27.1033649444580	26.9621620178223
28.2905960083008	28.0978984832764	27.9721889495850
29.3731212615967	29.0351200103760	28.9407062530518
29.9981384277344	29.9468173980713	29.8478507995605
NaN			29.9916267395020	29.9765014648438
NaN			NaN			NaN
NaN			NaN			NaN
NaN			NaN			NaN
NaN			NaN			NaN

lon: 
280			280			280
280.182220458984	280.218933105469	280.255859375000
280.356109619141	280.399017333984	280.367797851563
280.321624755859	280.327362060547	280.348907470703
280.134094238281	280.118408203125	280.200622558594
280.033691406250	279.903564453125	279.920562744141
NaN			279.896148681641	279.875854492188
NaN			NaN			NaN
NaN			NaN			NaN
NaN			NaN			NaN
NaN			NaN			NaN

exitcode:
-1
-1
-1
```

Note that there may be small differences in lat/lon between operating systems or compilers used.
You can also plot the output using cms-master/postproc/draw_traj_netcdf.m and compare with the example given at /expt_example/output/traj_file_example.jpg.
