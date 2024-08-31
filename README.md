# QDDataBase

Colloidal Quantum Dots (QDs) combine inorganic materials scaffolds with surface organic ligands. A key role played by the ligands in all these systems is the stabilization of the inorganic region in organic solvents to prevent its dissolution. The suitability of a certain ligand depends on several factors such as magnitude of the QD/ligand binding strength, ligand/ligand packing, and ligand/solvent interactions.  In practice, each QD type has its best ligand; finding such ligand is however a tedious work, if one considers the labor and material costs involved in the experiments. In this context, computational screening provides an attractive alternative to browse the largely unexplored space of potentially interesting ligands.

We therefore introduce a public database of organic molecules, derived by an advanced filtering of the PUBCHEM database, with the aim of building a subset of surface ligands candidates that are potentially suitable to passivate the surface of any colloidal QD.
For each ligand in the database, we additionally provide relevant chemical and physical properties, from the boiling and melting points to more specific properties that account for the interactions with the solvent and amongst ligands themselves at the QD surface. 


## Pre-Filtering
We first mined the Compound database of PubChem [1], an open repository of ~110 million available chemical substances, to select the molecules that could effectively behave as ligands. This filter was mostly based on the presence of a single functional group in the molecule, chosen amongst the well-known ligands’ anchoring groups (carboxylic acid, sulfonic acid, phosphonic acid, thiol, amines) and reduced the dataset to ~37 million of candidates.

This “smiles to filter” scanning process, excluding (or including) a set of molecules based on structural characteristics like their functional groups was performed using the Python-based library [Flamingo](https://github.com/nlesc-nano/flamingo).

## QD/Ligand Interactions

We performed a sensitivity analysis by computing the QD/ligand binding strength at the DFT level for two QD models (CdSe and CsPbBr3) and for a representative subset of ligands spanning types of backbones and substituents and evidenced that the QD/ligand interactions are mostly determined by the type of anchoring group. We concluded that the selection of a given functional group already provides, in first approximation, a good measure of the QD/ligand binding strength.

## Ligand/Solvent Interactions

For our reference dataset (divided by anchoring group), we then estimated the values of various pure component physical properties that are either of interest by themselves (e.g. boiling point, melting point) or can be used for the solvation property calculations (e.g. logP, solvation energy and activity coefficients in various organic solvents).

The estimation of COSMO-RS (COnductor-like Screening MOdel for Realistic Solvents) [2] properties was carried out by the Fast Sigma program implemented in AMS (Amsterdam Modelling Suite) [3]. The calculations were automatized and managed via the Compound Attachment Tools ([CAT](https://github.com/nlesc-nano/CAT)) [4] and sister packages [nano-CAT](https://github.com/nlesc-nano/nano-CAT) and [data-CAT](https://github.com/nlesc-nano/data-CAT).

## Ligand/Ligand Interactions

Inspired by the organometallic chemistry, we then introduced the ligand cone angle as an approximate measure of the steric interactions amongst neighboring ligands at the QD surface. As preliminary linearization and geometry optimization were found to be required to obtain realistic molecular conformations and the cone angle. The calculations are therefore more time-consuming than initially expected and are currently being run. The results will be progressively added to the dataset as they become available.

The calculation of the cone angle is performed via the [nano-CAT](https://github.com/nlesc-nano/nano-CAT) code and preceded by a biased conformational search implemented in [CAT](https://github.com/nlesc-nano/CAT) and by a geometry optimization at the DFTB level of theory with the GFN1-xTB parameter set [5] using AMS.


[1] Kim S et al., Nucleic Acids Res., 49(D1):D1388–D1395, 2021.

[2] Klamt A. et al., J. Phys. Chem., 99(7) : 2224–2235, 1995.

[3] te Velde G. et al., J. Comput. Chem., 22(9): 931–967, 2001.

[4] van Beek B. et al., J. Chem. Inf. Model. 2022, 62, 22, 5525–5535.

[5] Grimme S. et al., J. Chem. Theory Comput., 13(5):1989–2009, 2017.


