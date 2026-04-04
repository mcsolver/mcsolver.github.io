# Network Analysis

## Overview

Real-world networks — communication, social, infrastructure, and cybersecurity — exhibit recurring structural patterns. Detecting and comparing these patterns is central to anomaly detection, community analysis, and resilience assessment. MCIS provides an exact, symmetry-aware measure of **structural overlap** between two networks or network snapshots.

## Applications

### Motif Detection

Network motifs are small subgraphs that appear significantly more often than expected by chance. Finding the largest common motif between two networks via MCIS helps:

- Identify **functionally conserved circuits** in neural or regulatory networks
- Compare network architecture across domains (e.g., Internet AS-graph vs. power grid)
- Discover recurring attack patterns in network intrusion logs

### Anomaly and Intrusion Detection

In cybersecurity, MCIS compares a **current network state** against a known-good baseline or a threat signature:

- A high MCIS score with a known attack template triggers an alert
- Low MCIS with a baseline snapshot signals structural deviation
- Common subgraph mapping pinpoints exactly which nodes/edges match the signature

### Social Network Evolution

Tracking how a community's internal structure changes over time amounts to comparing network snapshots. MCIS quantifies:

- **Core stability** — the common subgraph is the persistent interaction core
- **Churn rate** — vertices/edges outside the MCIS are ephemeral
- **Polarisation events** — a sudden drop in MCIS size between two time windows

### Graph Edit Distance Lower Bound

Graph Edit Distance (GED) is expensive to compute exactly. Since every induced common subgraph gives an upper bound on GED, MCIS provides:

```
GED(G, H) >= |V(G)| + |V(H)| - 2 * MCIS(G, H)
```

This lower bound is tight and useful for pruning in large-scale GED computations.

### Infrastructure Resilience

Power grids, water systems, and transport networks can be compared before and after a failure event. The MCIS of the pre- and post-failure graphs identifies the **resilient subgraph** — the portion of the network that remained structurally intact.

## Symmetry in Networks

Many engineered networks (e.g., data-centre topologies, ring networks) contain high structural symmetry. SymSplit's dual symmetry breaking is particularly effective in these cases, often yielding order-of-magnitude speedups over baseline McSplit.
