# Dynamic 3DGS-SLAM Paper Comparison

This document organizes representative works on dynamic-scene 3D Gaussian SLAM and related Gaussian mapping methods.

The purpose is not only to summarize individual papers, but also to compare how different methods handle dynamic observations, Gaussian growth, map compactness, and camera tracking.

## 1. Comparison Dimensions

I mainly compare the following aspects:

- Dynamic-scene assumption
- Dynamic-object detection or suppression strategy
- Geometric / semantic / residual cues
- Gaussian initialization and densification
- Clone / split control
- Map compactness
- Camera tracking strategy
- Rendering quality
- Computational overhead
- Dataset and evaluation protocol
- Open-source availability
- Main limitation

---

## 2. Method Comparison

| Method | Dynamic Handling | Main Cue | Gaussian Growth Control | Tracking | Map Compactness | Main Limitation |
|---|---|---|---|---|---|---|
| DG-SLAM | TBD | TBD | TBD | TBD | TBD | TBD |
| DGS-SLAM | TBD | TBD | TBD | TBD | TBD | TBD |
| SDG-SLAM | TBD | TBD | TBD | TBD | TBD | TBD |
| Gassidy | TBD | TBD | TBD | TBD | TBD | TBD |
| WildGS-SLAM | TBD | TBD | TBD | TBD | TBD | TBD |
| ResGS | TBD | TBD | TBD | TBD | TBD | TBD |
| EDC | TBD | TBD | TBD | TBD | TBD | TBD |
| GDAGS | TBD | TBD | TBD | TBD | TBD | TBD |

> `TBD` indicates that the corresponding item will be filled after checking the original paper and supplementary material.

---

## 3. Questions for Each Paper

When reading each work, I try to answer the following questions:

### Problem Definition

1. What type of dynamic scene does the paper target?
2. What failure mode of conventional Gaussian SLAM is emphasized?
3. Is the main problem tracking, mapping, rendering, or map redundancy?

### Dynamic Modeling

1. How are dynamic regions detected?
2. Does the method rely on semantics?
3. Does it use optical flow, depth inconsistency, photometric residuals, geometric residuals, or motion segmentation?
4. Is dynamic information estimated online or obtained from a pretrained model?

### Gaussian Lifecycle

1. How are new Gaussians initialized?
2. How are clone and split operations triggered?
3. Are dynamic Gaussians directly removed?
4. Does the method control Gaussian growth before densification or prune Gaussians afterwards?
5. Does it explicitly model the history or lineage of Gaussian growth?

### Tracking and Mapping

1. Does the method modify the tracking loss?
2. Does the method modify the mapping loss?
3. Are tracking and mapping affected by the same dynamic mask?
4. Is there a separate reliability or confidence model?

### Experiments

1. Which datasets are used?
2. Which dynamic sequences are evaluated?
3. What metrics are reported?
4. Is the final number of Gaussians reported?
5. Is runtime or memory consumption reported?
6. Are ablation studies sufficient to support the proposed mechanism?

---

## 4. Taxonomy

Current dynamic 3DGS-SLAM methods can be investigated from several perspectives:

### A. Observation-level suppression

Dynamic observations are detected and excluded or down-weighted before they influence tracking or mapping.

Typical cues may include:

- semantic masks
- motion segmentation
- optical flow
- depth inconsistency
- photometric residuals
- geometric residuals

### B. Gaussian-level control

Individual Gaussians are evaluated according to their current state and may be suppressed, removed, or assigned lower confidence.

### C. Growth-level control

Instead of only processing already-created Gaussians, the method intervenes during Gaussian densification and controls whether clone/split operations should occur.

### D. Lifecycle / lineage-level modeling

Gaussian growth is analyzed over time by linking newly generated Gaussians to their source or parent Gaussians.

This perspective is particularly relevant to my current research.

---

## 5. Relation to My Research

My current research investigates a different question from simply detecting dynamic pixels:

> Can persistent map redundancy in dynamic scenes be understood as a Gaussian lifecycle growth problem?

The working hypothesis is that unstable Gaussians can repeatedly participate in clone/split operations and generate descendants, causing local Gaussian populations to expand even when the original dynamic observations are transient.

To study this problem, I focus on:

- Gaussian UID tracking
- source-parent UID tracking
- parent-lineage construction
- visibility-conditioned residual statistics
- lineage-level risk estimation
- pre-densification growth gating
- map-size and localization analysis

The objective is to move from **observation-level dynamic suppression** toward **lifecycle-aware Gaussian growth control**.

---

## 6. Reading Status

| Paper | Read | Detailed Notes | Code Checked | Experiments Checked |
|---|---:|---:|---:|---:|
| DG-SLAM | ⬜ | ⬜ | ⬜ | ⬜ |
| DGS-SLAM | ⬜ | ⬜ | ⬜ | ⬜ |
| SDG-SLAM | ⬜ | ⬜ | ⬜ | ⬜ |
| Gassidy | ⬜ | ⬜ | ⬜ | ⬜ |
| WildGS-SLAM | ⬜ | ⬜ | ⬜ | ⬜ |
| ResGS | ⬜ | ⬜ | ⬜ | ⬜ |
| EDC | ⬜ | ⬜ | ⬜ | ⬜ |
| GDAGS | ⬜ | ⬜ | ⬜ | ⬜ |

---

## 7. Notes

This file will be continuously updated as I review the original papers, supplementary materials, and available implementations.

Only information verified from the original sources will be added to the comparison table.
