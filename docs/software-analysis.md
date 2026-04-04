# Software & Malware Analysis

## Overview

Compiled software can be represented as graphs capturing its **control flow**, **call structure**, or **data dependencies**. MCIS over these graphs enables structural comparison of programs without relying on source code or symbol information — making it applicable to obfuscated binaries, stripped executables, and cross-compiler variants.

## Graph Representations

| Representation | Vertices | Edges | Use case |
|---|---|---|---|
| Control-Flow Graph (CFG) | Basic blocks | Conditional / unconditional jumps | Function-level similarity |
| Call Graph | Functions | Call sites | Module-level architecture |
| Program Dependence Graph (PDG) | Statements | Data / control dependencies | Semantic clone detection |
| System-call Graph | Syscall nodes | Execution order | Malware behaviour matching |

## Applications

### Malware Variant Detection

Malware families are often mutated to evade signature-based detectors: dead code insertion, block reordering, register renaming, and function splitting. These transformations change the binary but leave the **structural skeleton** of the CFG largely intact. MCIS:

- Measures the largest shared CFG fragment between a known malware sample and a candidate binary
- Is robust to compiler differences and obfuscation passes that do not restructure control flow
- Provides an **interpretable mapping** identifying which blocks correspond between samples

### Code Clone Detection

Software projects accumulate copy-pasted or lightly modified code. MCIS on CFGs detects:

- **Type-3 clones** (structurally similar with minor modifications) missed by text-diffing tools
- Cross-language clones when both are compiled to a common IR (e.g., LLVM bitcode)
- Plagiarism in student submissions or open-source licence violations

### Patch Analysis and Vulnerability Propagation

When a CVE patch is applied to a library, downstream projects may ship the vulnerable version. MCIS between the patched and unpatched function CFG:

- Identifies exactly which basic blocks changed (vertices outside the MCIS)
- Enables **binary-level patch presence testing** without recompilation
- Quantifies the structural distance introduced by the fix

### Firmware Similarity

Embedded firmware for IoT devices is often derived from a common SDK with vendor-specific customisation. MCIS across firmware call graphs:

- Identifies the common SDK core
- Detects whether a security-critical function (e.g., TLS handshake) was modified
- Supports firmware provenance attribution

## Robustness to Obfuscation

| Obfuscation technique | Effect on CFG | MCIS impact |
|---|---|---|
| Dead code insertion | New disconnected vertices | MCIS excludes dead code — no impact |
| Block splitting | One vertex → two vertices | Slight MCIS reduction |
| Opaque predicates | Extra conditional edges | Small structural noise |
| Control-flow flattening | Dispatcher pattern | Significant restructuring — reduced MCIS |

SymSplit gives exact MCIS, so even small structural differences are faithfully captured rather than approximated.
