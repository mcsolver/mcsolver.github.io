# Cheminformatics

## Overview

In cheminformatics, molecules are represented as **molecular graphs** — atoms are vertices and covalent bonds are edges. Finding structural similarity between two molecules is fundamental to drug discovery, toxicology prediction, and chemical database search.

The **Maximum Common Induced Subgraph (MCIS)** of two molecular graphs is the largest fragment shared by both molecules in terms of atom count, while preserving all bonds within that fragment. This is commonly called the **Maximum Common Substructure (MCS)**.

## Applications

### Drug Discovery & Virtual Screening

Lead optimisation relies on identifying a common scaffold between a known active compound and a candidate. MCIS quantifies how much of the pharmacophore is conserved across series, enabling:

- **Scaffold-based clustering** of compound libraries
- **Activity cliff detection** — pairs with high MCIS score but divergent bioactivity
- **Bioisostere replacement** guided by the common core

### Similarity Search in Chemical Databases

Chemical databases such as PubChem, ChEMBL, and ZINC contain hundreds of millions of compounds. MCIS-based similarity provides a theoretically grounded alternative to fingerprint-based Tanimoto scores, especially for:

- Retrieving structurally novel analogues
- Fragment-based screening
- Reaction pathway comparison

### Toxicology & ADMET Prediction

Regulatory agencies use structural alerts based on recurring toxic fragments. MCIS can identify whether a candidate shares a known toxic substructure with a reference compound, supporting ADMET (Absorption, Distribution, Metabolism, Excretion, Toxicity) modelling.

## Graph Representation

Atoms carry **vertex labels** (element, charge, hybridisation) and bonds carry **edge labels** (single, double, aromatic). For labelled MCIS, vertex/edge compatibility constraints are added to the subgraph search.

SymSplit handles unlabelled graphs; label-constrained variants can be encoded by pre-filtering the compatibility relation before running the solver.

## Complexity Note

MCS in molecular graphs is NP-hard in general but tractable in practice for drug-sized molecules (< 100 heavy atoms) with branch-and-bound solvers. SymSplit's symmetry-breaking pruning is particularly effective when ring systems introduce structural symmetry — a common occurrence in medicinal chemistry scaffolds.
