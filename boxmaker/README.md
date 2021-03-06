# Box Maker 

The following must be in the path:

`PATH=$PATH:/suppscr/pfaedntner/vanouk/software/packmol`

`AMBERHOME=/gscratch/pfaendtner/vjaeger/software/amber11b`

And acypye.py should be in the directory. 

# Quick Start Guide

you will need to edit boxmaker.inp to reflect the system you are initializing:

```
###INPUT FILE FOR BOXMAKER. INPUTS ARE CASE SENSITIVE. SEE EXAMPLES###

###Solute is not supported for DES

#SIMULATIONS CONTAINING SOLUTE(S).
SOLVENT_TYPE=DES      #Type of solvent. (IL, organic, DES, water, none). IL is ionic liquid.
SOLUTE=start          #pdb of the solute. Protein is the only supported solute now. Should be a pdb.
		      #set PERCENT 
		      #>>You can do a binary mixture of the solvent with water by setting the $PERCENT variable to >0 <<#
		      #>>If you want multiple solutes in one simulation, they can be input as a single pdb file containing all of the molecules.

#SIMULATIONS CONTAINING NO SOLUTE(S)
SOLVENT_BOX=yes       #Do you want to do a simulation of pure solvent? (yes, no) This will override $SOLUTE above.
BOX_X=50              #Size of box in X direction in Angstroms.
BOX_Y=50              #Size of box in Y direction in Angstroms.
BOX_Z=50              #Size of box in Z direction in Angstroms.

#GENERAL PARAMETERS. TRY YOUR BEST TO FILL OUT ALL VARIABLES.
IL_CAT=CHO            #Resname of IL cation. This must be the prefix of all files associated with the cation.(Leave blank if not IL)
IL_AN=CLD             #Resname of IL anion. This must be the prefix of all files associated with the anion. (Leave blank if not IL)
ORG_MOL=EYG           #Resname of the organic solvent or h-bond donating molecule. (Leave blank if not organic or DES)
MOLM=263.76           #Molar mass of the organic molecule or IL pair in amu.
MOLM_HBND=62.07       #Molar mass of the h-donor
DENS=1.12             #Density of the organic molecule, DES, or IL in g/cm^3. Guess 1 if unknown.
PERC_TYPE=mole        #For binary mixtures. Which type of % do you want? (mass, mole, volume) vol may not be supported for DES
PERCENT=33.33         #Percent of solvent you wish to be IL (in DES and IL) or organic (in organic). (20 = 20% w/w or 20% v/v or 20 mol% for example). A solvent box with no water is the integer 100.
AMBER_FF=ff99SBildn   #Name of the amber force field you wish to use. (ff99SBildn, ff99SB, see tleap force fields)
WAT_TYPE=TIP3PBOX     #Type of water model you would like (TIP3PBOX, TIP4PBOX, SPCBOX, see water types in tleap)

BUFFER=12.5           #Space between the solue and the edge of the box in Angstroms.
CUBIC=iso             #iso = cubic, leaving it blank will create a rectangular prism.
GROMACS=yes           #Generate .gro and .top files using acpype.py? (yes, no)
NEUTRALIZE=no         #Neutralize the charge by adding counterions Na+ or Cl-. (yes, no)

DISULFIDE=no          #Are there disulfide bonds in the solute. (yes, no). Works for proteins.
SSBOND_A_1=100        #You must manually input all disulfide bonds with a line for each atom. SSBOND_B_1=120
SSBOND_A_2=25         #(SSBOND_A_#=RESIDUE_NUM, SSBOND_B_#=RESIDUE_NUM). This means that the #th SSBOND is between RESIDUE_NUM and $RESIDUE_NUM.
SSBOND_B_2=40
```

You will need to provide .frcmod, .pdb, and .lib files for boxmaker (these can be generated using ffmaker).

this will typically run fine on an interactive node (do not run on the login nodes):

`source boxmaker.bash`

alternatively you can submit the job to the que:

`qsub boxmaker.pbs`
