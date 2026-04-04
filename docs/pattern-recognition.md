# Pattern Recognition

## Overview

Many pattern recognition problems involve comparing **structural descriptions** rather than raw pixel arrays. Graphs provide an expressive, transformation-invariant representation for shapes, scenes, and 3-D models. MCIS measures the largest shared structural fragment between two such graph descriptions.

## Applications

### Image Retrieval via Scene Graphs

A scene graph encodes objects as vertices and spatial/semantic relations (left-of, supports, part-of) as edges. MCIS between two scene graphs:

- Retrieves images containing a common structural pattern (e.g., "person sitting on chair next to table")
- Powers **compositional similarity search** in image databases
- Supports visual question answering by matching query subgraphs to scene descriptions

### Shape and Contour Matching

2-D shapes can be encoded as **shock graphs** or **Reeb graphs** capturing the skeletal structure. MCIS on these representations:

- Provides a **part-based similarity score** invariant to non-rigid deformation
- Enables shape retrieval in medical imaging (e.g., organ boundary comparison)
- Supports logo and trademark similarity detection

### 3-D Model Comparison

CAD models and point-cloud reconstructions are often represented as adjacency graphs of surface patches or mesh faces. MCIS identifies the largest shared sub-assembly, enabling:

- **Re-use detection** across CAD libraries
- **Partial matching** for object recognition in cluttered scenes
- Cross-modality alignment (CAD model vs. scanned point cloud)

### Document Layout Analysis

Page layouts can be encoded as graphs of text blocks, images, and spatial relationships. MCIS across layout graphs supports:

- Template-based document classification
- Cross-document structural diff for version control
- Style transfer by identifying common layout skeletons

## Why Graph Representations?

Unlike appearance-based features, graph representations are:

- **Invariant to low-level variation** (lighting, texture, colour)
- **Compositional** — parts and relations are explicit
- **Interpretable** — the MCIS result directly identifies the shared structural elements

SymSplit's exact MCIS output provides both the size of the common substructure and the explicit vertex correspondence, making it actionable for downstream alignment tasks.
