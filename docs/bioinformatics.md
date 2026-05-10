# Bioinformatics

## Overview

Biological systems are inherently graph-structured. Proteins interact through physical binding (protein–protein interaction networks), metabolites connect via enzymatic reactions (metabolic networks), and genes regulate each other (gene regulatory networks). MCIS enables **comparative analysis** of these networks across conditions, time points, and species.

## Applications

### Protein–Protein Interaction (PPI) Networks

PPI networks encode the interactome of a cell. Conserved subnetworks across species often correspond to evolutionarily important functional modules (e.g., the spliceosome, ribosome assembly). MCIS:

- Detects **conserved interaction modules** between human and model organisms
- Supports **ortholog group identification** beyond pairwise sequence alignment
- Reveals rewiring events associated with disease states

### Metabolic Pathway Alignment

Metabolic pathways can be modelled as directed or undirected graphs with enzyme nodes and metabolite edges. MCIS across two organisms' metabolic graphs identifies:

- **Shared biosynthetic routes** useful for engineering synthetic pathways
- **Divergent branches** that explain phenotypic differences
- Candidate horizontal gene transfer events

### Structural Bioinformatics

Protein 3-D structures can be abstracted into **contact graphs** (residues as vertices, spatial proximity as edges) or **secondary-structure graphs**. MCIS between contact graphs detects:

- Structurally conserved domains across low-sequence-identity proteins
- Binding site similarity for function annotation
- Allosteric communication paths shared across homologues

### RNA Secondary Structure Comparison

RNA secondary structures are modelled as planar graphs of base-pairing interactions. MCIS identifies the largest shared stem-loop or pseudoknot motif between two RNA molecules.

## Example Graph Pair

**Protein complex (K₄) vs K₄ + species-specific interactor** — the four-protein clique is the conserved functional module.

Graph G (K₄ — four proteins, all pairs interact):

```
c Conserved protein complex - 4 proteins fully connected
p edge 4 6
e 1 2
e 1 3
e 1 4
e 2 3
e 2 4
e 3 4
```

Graph H (same complex plus one additional interactor, protein 5, found only in one species):

```
c K4 complex + species-specific interactor (protein 5)
p edge 5 7
e 1 2
e 1 3
e 1 4
e 2 3
e 2 4
e 3 4
e 1 5
```

Expected MCIS size: **4** (the conserved clique; protein 5 is species-specific).

---

## Why MCIS over Sequence Alignment?

Sequence alignment captures linear similarity and fails when insertions, circular permutations, or convergent evolution produce structurally similar but sequentially dissimilar proteins. MCIS operates directly on the **topology**, making it complementary to sequence-based methods.

## Scale Considerations

Biological networks can be large (thousands of nodes). Exact MCIS becomes intractable at that scale; SymSplit is best suited for subnetwork-level comparisons (< 200 nodes) or as a subroutine within heuristic decomposition pipelines.
