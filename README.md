# forcefield

General description

a.This program is writen by fortran90 on visual studio2019 without any using of extern library

b.This program uses force field method to first give a energy of a given hydrocarbon(the structure could be branced or cycled) and then use Metropolis algorithm to do subsequent energy minimization.

c.all teses parameter related to forcefield used in this prigram are found in literature "J. Am. Chem. SOC. 1995, 117, 5179-5197" and the final units of the energy is kcal

d.Van-der Walls’ interactions between two atoms whose distance smaller than 4A are not calculated. Because if two atoms close together, the Van-der Walls’ interactions has been included in Stretch,Bending and Torsional energy. Because when calculate Torsional energy, it cross three bonds and the three bonds distance are almost 4A

f.In this program, I only calculate the Bending and Torsional energy between carbon carbon atom , not calculate the carbon hydrogen's Bending and Torsional energy

e.input file format, one example is for methane(CH4)
!*************************************************************************
5

C      -0.964831852126      -0.691462827481      -0.000000000062    
H      -0.782365337661      -1.372751578831       0.856342065276    
H      -1.767889039149      -1.109936546833      -0.640897047230    
H      -1.275127188280       0.303959353789       0.378974418443    
H      -0.033945843010      -0.587122537140      -0.594419436427    
!*********************************************************************
The first line is the total atom number in the molecular
The second line is empty.
From the third line, the first letter indicate the atom type,then follow the coordination of this atom
f.the input document need to be put in the same file with the program
