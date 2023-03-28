# forcefield

General description

a.This program is writen by fortran90 on visual studio2019 without any using of extern library

b.This program uses force field method to first give a energy of a given hydrocarbon(the structure could be branced or cycled) and then use Metropolis algorithm to do subsequent energy minimization.

c.all theses parameters and formula related to forcefield calculation used in this program are found in literature "J. Am. Chem. SOC. 1995, 117, 5179-5197" and the final units of the energy is kcal

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
!********************************************************************************************************
!********************************************************************************************************
!********************************************************************************************************
structure of program

First, the main program call a subroutine called "readfile" in module driven

Second,the main program use functions called "Stretch", "Bending","Torsional","Electrostatic","vdw" in module calculate respectly, these function will return stretch energy, bending energy,torsional energy, electrostatic energy and Van-der Walls energy of the whole molecule 

Third, the main add stretch energy, bending energy,torsional energy, electrostatic energy and Van-der Walls energy together to get the total energy of the molecule

Fourth, the main program use call a subroutine called "converge" in module Metropolis. The subroutine "converge" will generate a file contains the minimization energy and minimized geometry of the molecule and print the minimized energy on screen

!****************************************************************************************************************************************************************

detailed explanation of the role of each module and each subroutine

module driven:
         this module cantains one subroutine called "readfile" and five public variables called position(:,3), distance(:,:),bonds(:,:),  atom_total_num, atom_carbon_num. 
         
Role and input of the subroutine "realfile"
Input: when you use this subroutine, you should input the file name you want to read as a string, and be sure the string length is smaller than 40
Role: this subroutine first read the file based on the input file name, then assigning value to the five public variables(position(:,3), distance(:,:),bonds(:,:),  atom_total_num, atom_carbon_num)

Role of the five public variables(position(atom_total_num,3), distance(atom_total_num,atom_total_num+1),bonds(atom_total_num,atom_total_num+1),  atom_total_num, atom_carbon_num) in module driven:

a.the five public variables are only shared with the main program, and the main program used them as parameter. the reason I do not write functions to return these public variables to main program is for save memory space and make the code short, improve the code efficiency.

b.position(atom_total_num,3)

role: used to store the coordinates of each atom
size: atom_total_num × 3, atom_total_num,1 for x, atom_total_num,2 for y,atom_total_num,3 for z

shape: x1,y1,z1                                                                                                                                                         
       x2,y2,z2                                                                                                                                                        
       x3,y3,z3                                                                                                                                                        
       ........                                                                                                                                                         
       xn,yn,zn  (n = atom_total_num)                                                                                                                                
!*************************************************************************************************************************************************************

module func:
this module contains 7 functions called "Stretch_Energy"," Bending_Energy","Torsional_Energy","Electrostatic_Energy","Vdw_Energy","getTorsionAngle","getBendingAngle"

Important: "Stretch_Energy"," Bending_Energy","Torsional_Energy","Electrostatic_Energy","Vdw_Energy" are just computational formula of force field. And in this program module func is just an extension part of module calculate, all these functions in module func could not be used individually.









