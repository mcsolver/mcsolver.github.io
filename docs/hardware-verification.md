# Hardware Verification

## Overview

Digital hardware designs are described as **netlists** — directed graphs where vertices represent logic gates, flip-flops, or ports, and edges represent signal wires. Comparing netlists structurally is a core task in formal verification, design re-use, and IP protection. MCIS identifies the **largest equivalent functional block** shared between two netlists.

## Applications

### Equivalence Checking

Formal equivalence checking verifies that two implementations (e.g., RTL and gate-level netlist after synthesis) compute the same function. MCIS-based structural matching provides:

- A **structural alignment kernel** that seeds Boolean equivalence checking tools
- Faster convergence for incremental verification after small ECO (Engineering Change Order) patches
- Identification of which sub-circuits changed between two design revisions

### Cross-Design Re-Use Detection

Large SoC designs contain many IP blocks that are reused or slightly modified across product generations. MCIS:

- Detects **unintentional duplication** that inflates area
- Identifies **partially reused IP** that should be unified into a parameterised module
- Supports licence compliance auditing by matching against known IP fingerprints

### Hardware Trojan Detection

A hardware Trojan is a malicious modification inserted into a design. Comparing a reference netlist against a manufactured-chip reverse-engineered netlist via MCIS:

- The **MCIS identifies the intact portion** of the design
- Vertices/edges outside the MCIS are candidate Trojan insertion points
- The vertex mapping directly localises the suspicious circuit region

### Synthesis Quality Assessment

Different synthesis tools or constraint settings produce structurally different netlists for the same RTL. MCIS quantifies how much of the logical structure is preserved, helping engineers:

- Benchmark synthesis tools on structural preservation
- Identify over-optimised paths where logic sharing reduces debuggability
- Validate that timing-driven optimisation did not alter functional intent

## Graph Encoding

A typical netlist graph encoding for MCIS:

| Network element | Graph element |
|---|---|
| Logic gate (AND, OR, XOR…) | Vertex with type label |
| Flip-flop / register | Vertex with label `FF` |
| Signal wire | Directed edge |
| Primary input / output | Boundary vertex |

For unlabelled MCIS (as in SymSplit), labels are dropped and structural isomorphism alone is matched. Label-aware variants pre-filter vertex compatibility.

## Example Graph Pair

**Linear 4-gate pipeline vs pipeline with bypass wire** — three shared gates form the MCIS; the bypass is the design difference.

Graph G (straight pipeline — gates 1→2→3→4):

```
c Linear 4-gate pipeline
p edge 4 3
e 1 2
e 2 3
e 3 4
```

Graph H (same pipeline plus a bypass wire from gate 1 directly to gate 3):

```
c Pipeline with bypass wire (gate 1 to gate 3)
p edge 4 4
e 1 2
e 2 3
e 3 4
e 1 3
```

Expected MCIS size: **3** (gates 2, 3, 4 — the segment unaffected by the bypass).

---

## Scale and Practicality

Industrial netlists can contain millions of gates. Exact MCIS is applied at the **block level** (hundreds to low thousands of gates) after partitioning. SymSplit's symmetry-breaking is highly effective on regular structures such as arithmetic units, memory arrays, and symmetric bus fabrics.
