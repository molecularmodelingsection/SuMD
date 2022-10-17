# SuMD
Python code to run Supervised Molecular Dynamics (SuMD) simulations
N.B.: the Python code to analyze SuMD trajectories can be found at github.com/molecularmodelingsection/SuMD-analyzer

Reference publication:  
**"Investigating RNA-Protein Recognition Mechanisms through Supervised Molecular Dynamics (SuMD) Simulations."**  
Pavan M., Bassani D., Sturlese M., Moro S. (under peer review at *NAR Genomics and Bioinformatics*)

SuMD is a Python code that can be utilized to perform Supervised Molecular Dynamics simulations. The algorithm is deeply explained is the works of Sabbadin et. al (2014)<sup>1</sup>, Cuzzolin et. al (2016)<sup>2</sup> and Salmaso et al. (2017)<sup>3</sup>, other than in the reference publication.
1. Sabbadin, D.; Moro, S. Supervised Molecular Dynamics (SuMD) as a Helpful Tool to Depict GPCR-Ligand Recognition Pathway in a Nanosecond Time Scale. J. Chem. Inf. Model. 2014, 54, 372–376.
2. Cuzzolin, A.; Sturlese, M.; Deganutti, G.; Salmaso, V.; Sabbadin, D.; Ciancetta, A.; Moro, S. Deciphering the Complexity of Ligand-Protein Recognition Pathways Using Supervised Molecular Dynamics (SuMD) Simulations. J. Chem. Inf. Model. 2016, 56, 687–705.
3. Salmaso, V.; Sturlese, M.; Cuzzolin, A.; Moro, S. Exploring Protein-Peptide Recognition Pathways Using a Supervised Molecular Dynamics Approach. Structure. 2017, 25,655–662.e2.

SuMD simulations can be performed starting from a pre-equilibrated system in which the ligand is placed far enough from the protein. Consider that the distance separating the protein from the ligand directly affects the system size and, therefore, the speed of the simulation. Nonetheless, take care of the PME threshold (9 Å), the long-range component of attractive forces. So the general idea is to place the ligand at a distance, at least, bigger than the PME cut-off from any protein atom. The distance should be set even depending on the hydrodynamic properties of the ligand and the complexity of the binding
event. As rule of thumb, we suggest to place the ligand in a random conformation, in a range of 30-70 Å. **Two different force field are supported to run the simulation, AMBER and CHARMM.**  

SuMD requires a **configuration file** (here named **“inputfile.dat”**) organized in three major sections containing information about (i) the system, (ii) the supervision procedure, and (iii) the simulation settings. **An explanation on each required parameter to run the simulation is provided in the inputfile_commented.dat file.**  
**N.B.**: in order to launch the simulation, **the pdb file containing the coordinates the input coordinates for the system to be simulated, a prmtop/psf file containing the corrispondent topology, and an xsc file containing the box dimension should be provided. The topology and box dimension file MUST have the same basename as the pdb file.** In the case you choose CHARMM as force field, a combined prm/par file containing all the parameters needed to describe the system must also be provided and indicated in the input file under the parameter flag.

The current version of the code only supports the **ACEMD3 engine** to run molecular dynamics simulations. All Python libraries required to successfully run the code are embedded into a YAML file ('sumd.yml') that can be used to reconstitute the right Python virtual environment through the conda package manager.  
**N.B.**: a dot file ('.suMDrc') is present in the directory. In this file you can specify the path to the acemd3 executable that you want to use. For most users, anyway, the default path should be fine.

To reconstitute the right Python virtual environment:
- **conda create -f sumd.yml**  

In case you prefer to reconstuct it manually:
1. conda create -n sumd
2. conda install -c conda-forge prody
3. conda install -c conda-forge -c acellera acemd3=3.5

To run the code:
1. open a terminal within the directory of interest
2. activate the right conda environment (**conda activate sumd**)
3. run the code (**python3 /PATH/TO/SUMD_DIRECTORY/suMD inputfile.dat**)

To test the code, an example system is provided in the **test** directory.
