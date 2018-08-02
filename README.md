# VASP_DOS_extractor
------------------
# Simple description:

Pymatgen-based python script to extract density of states (DOS) and projected DOS from vasprun.xml file
  
# What does this do:
This script replaces one of the most common use of p4vasp: extracting DOS data from VASP (http://cms.mpi.univie.ac.at/vasp/) output, which is a density functional theory (DFT) calculation program. Though p4vasp is with intuitive GUI, extracting DOS data can easily take time especially when the number of atom, band, and energy grid are larger. Note that you should install pymatgen (http://pymatgen.org/) before using this script.
  
# The process with p4vasp usually happens as follows:
  - Download xml file to local computer (often over 100 MB)
  - Open p4vasp and open xml file
  - Plot element or individual atom of interest to plot the local projection of DOS (PDOS). (This process takes most of the time)
  - Export data to designated filename. 

# With DOS_extractor.py, these four process can be done with one command line:
  $ python DOS_extractor.py [xml_filename] [output_filename] [List_of_elements_to plot_PDOS] [List_of_atoms_to_plot_PDOS]
[xml_filename]: name of vasprun.xml file.
[output_filename]: name of data containing DOS. Format basically follows the exported data from p4vasp, but in the line1, this code prints header starting with # showing the Band gap, and list of data in the output file.
[List_of_elements_to_plot_PDOS]: The elements are separated by space.
[List_of atoms_to_plot_PDOS]: The atoms are separated by space.

For example, if you want to extract PDOS of all elements in Sr2Fe2O5, and Fe1 atom, you might do the command as follows.
  $ python DOS_extractor.py vasprun.xml Sr2Fe2O5.dat Sr Fe O Fe1
  
# The output file, Sr2Fe2O5.dat will be look like as follows (basically same with p4vasp format):
'# BandGap: 0.348, Label: Spin up/down for Total, Sr, Fe, O, Fe1
-59.5136	0.0000  <-- This is start of the first block
-59.4556	0.0000
.
.
.
9.9503	-0.0000
10.0082	-0.0000  <-- This is end of the first block

-59.5136	0.0000  <-- This is start of the second block
-59.4556	0.0000
.
.

Left column of each block is energy grid, and the right column is the DOS.
In this example, there will be 10 blocks with Total DOS (up-spin/down-spin), Sr (up-spin/down-spin), Fe (up-spin/down-spin), O (up-spin/down-spin), and Fe1 (up-spin/down-spin). If the system was non-magnetic calculation, there will be 5 blocks by not including down-spin DOS.
