MacroDensity
====================

A set of python scripts to read in a VASP `LOCPOT` and plot the electrostatic potential in a number of ways, including:

* Planar average
* Spherical average
* Atom centred averages

Requirements
------------
[Python](https://www.python.org)

[Matplotlib](http://matplotlib.org) (to plot results on the fly)

[ASE](https://wiki.fysik.dtu.dk/ase/) (for atom centred functionality)


Installation
------------

Download `NewPotentialModule.py`. 
Include this file in your pythonpath or in the directory where you are performing the analysis.

There are several example files included with the package, they are documented below.

#### Mac Installation
- Download by clicking the `Download ZIP` on the right of this page.
- Place it in your preferred installation directory, let's say $home/src
```
mv ~/Downloads/MacroDensity-master.zip .
```
- Unzip the package

```
unzip MacroDensity-master.zip
```
- Add the directory to your PYTHON PATH
```
PYTHONPATH = $HOME/src/MacroDensity-master/:$PYTHONPATH
```
- You are now ready to run the examples listed below

PlanarAverage.py
------------
This example is for plotting the planar average of a potential along a vector (here it is z).
The only variables which need to be set are in the first three lines. Note `LOCPOT.slab` file is just a regular `LOCPOT`.

```
input_file = 'LOCPOT.slab'
lattice_vector = 4.75
output_file = 'planar.dat'
```

The variable lattice vector refers to the lattice vector of the bulk crystal structure in the direction of the plotting. 
It is used to get the macroscopic average, as defined in [Jackson](https://archive.org/details/ClassicalElectrodynamics).

The code is executed as:

```
python PlanarAverage.py
```
This results in a plot of the planar average and an output of the potential called planar.dat.

SphericalAverage.py
------------

This example is for plotting the average potential inside a sphere of given radius. 
It is the method used in our 2014 [JACS](http://pubs.acs.org/doi/abs/10.1021/ja4110073).

The lines which need to be edited for this are below.  
Note `LOCPOT.MiL` is just a regular `LOCPOT` file.

```
input_file = 'LOCPOT.MiL'
cube_size = [2,2,2]    # This size is in units of mesh points
## origin defines the bottom left point of the cube the "0,0,0" point in fractional coordinates
cube_origin = [0,0,0]
```

To run the code simply type:

```
python SphericalAverage.py
```
This results in some outpus telling you the average potential in the volume and the variance of the potential. If the variance is too high it means that you are not sampling a plateau in the potential; typically values below 10e-4 are acceptable.

OnSitePotential.py
------------

This is for calculating the potentials at the sites of a certain atomic nucleus, for example the O nucleii in an oxide. This on site potential calculated this way is equivalent to a Madelung potential and can be useful for predicting electron energy levels (see http://pubs.acs.org/doi/abs/10.1021/ar400115x for details).

The input lines to edit are :

```
potential_file = 'LOCPOT' # The file with VASP output for potential
coordinate_file = 'POSCAR' # The coordinates file NOTE NOTE This must be in vasp 4 format 
species = "O"  # The species whose on-site potential you are interested in 
sample_cube = [5,5,5] # The size of the sampling cube in units of mesh points (NGX/Y/Z)
```

The cube parameter determines the size of the sample area, the units are mesh points, the magnitude of the mesh point is calculated by dividing the appropriate lattice vector by the number of points (NGX/Y/Z in `OUTCAR`).

To run the code simply type:

```
python OnSitePotentail.py
```
The result is a histogram plot using Matplotlib. If you prefer data ouput simply edit the final lines of the script.

PlaneField.py
------------
This plots the countour lines of the iso-surface of an electric field in an arbitrary plane as defined in the preamble part of the file.

```
a_point = [0, 0, 0]
b_point = [1, 0, 1]
c_point = [0, 1, 0]

input_file = 'LOCPOT.slab'
```

The execution is simply:

```
python PlaneField.py
```
This creates a contour plot of the field lines.


To-do
------------

* Add a full description of the input file format.
* Command line argparse.
* Fix percentage to fraction.

Disclaimer
----------
This file is not affiliated with *VASP*. Feel free to use and modify, but do so at your own risk.