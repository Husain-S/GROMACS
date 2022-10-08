# GROMACS-GPU Protein
    source /usr/local/gromacs/bin/GMXRC
    gmx pdb2gmx -f bap1n.pdb -o pro.gro -ignh
    gmx editconf -f pro.gro -o box.gro -bt dodecahedron -d 1.0
    gmx solvate -cp box.gro -cs spc216.gro -p topol.top -o sol.gro
    gmx grompp -f ions.mdp -c sol.gro -p topol.top -o ions.tpr -maxwarn 1
    gmx genion -s ions.tpr -o ions.gro -p topol.top -pname NA -nname CL -neutral
    gmx grompp -f em-steep.mdp -c ions.gro -p topol.top -o em-steep.tpr
    gmx mdrun -v -deffnm em-steep
    gmx grompp -f nvt.mdp -c em-steep.gro -r em-steep.gro -p topol.top -o nvt.tpr
    gmx mdrun -v -deffnm nvt
    gmx grompp -f npt-1.mdp -c nvt.gro -t nvt.cpt -r nvt.gro -p topol.top -o npt-1.tpr
    gmx mdrun -v -deffnm npt-1
    gmx grompp -f md_50.mdp -c npt-1.gro -t npt-1.cpt -p topol.top -o md_50.tpr
    gmx mdrun -v -deffnm md_50
    gmx make_ndx -f em-steep.gro -o chain_a.ndx
    gmx trjconv -f md_50.xtc -s md_50.tpr -o md_50-n.xtc -center -pbc mol -ur compact -n chain_a.ndx
# GROMACS-GPU Protein-Ligand 
    antechamber -i 755sr.pdb -o fda.mol2 -fi pdb -fo mol2 -at bcc -c bcc
    acpype -di fda.mol2 -c bcc
    source /usr/local/gromacs/bin/GMXRC
    gmx pdb2gmx -f tc10_remove-tail-LRG.pdb -o pro.gro -ignh
    gmx editconf -f fda_NEW.pdb -o fda.gro
    gmx editconf -f cpx.gro -o box.gro -bt dodecahedron -d 1.0
    gmx solvate -cp box.gro -cs spc216.gro -p topol.top -o sol.gro
    gmx grompp -f ions.mdp -c sol.gro -p topol.top -o ions.tpr -maxwarn 1
    gmx genion -s ions.tpr -o ions.gro -p topol.top -pname NA -nname CL -neutral
    gmx grompp -f em-steep.mdp -c ions.gro -p topol.top -o em-steep.tpr
    gmx mdrun -v -deffnm em-steep
    gmx make_ndx -f fda.gro -o fda.ndx
    gmx genrestr -f fda.gro -n fda.ndx -o posre_fda.itp -fc 1000 1000 1000
    gmx make_ndx -f em-steep.gro -o index.ndx
    gmx grompp -f nvt.mdp -c em-steep.gro -r em-steep.gro -p topol.top -n index.ndx -o nvt.tpr
    gmx mdrun -v -deffnm nvt
    gmx grompp -f npt-1.mdp -c nvt.gro -t nvt.cpt -r nvt.gro -p topol.top -n index.ndx -o npt-1.tpr
    gmx mdrun -v -deffnm npt-1
    gmx grompp -f md_50.mdp -c npt-1.gro -t npt-1.cpt -p topol.top -n index.ndx -o md_50.tpr
    gmx mdrun -v -deffnm md_50
    gmx make_ndx -f em-steep.gro -o chain_a.ndx
    gmx trjconv -f md_50.xtc -s md_50.tpr -o md_50-n.xtc -center -pbc mol -ur compact -n chain_a.ndx
