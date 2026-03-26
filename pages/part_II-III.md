---
layout: section
---

# Part II: Algorithms for Jet Tagging

## Chapter 3: Algorithm Overview

---

# Algorithm Overview

<div class="absolute-center">

Three generations of jet tagging algorithms

1. **Rule-based algorithms** — hand-crafted physics variables exploiting jet substructure and heavy-flavour properties
2. **Shallow machine-learning algorithms** — multivariate analyses (BDT, MLP) combining high-level features
3. **Deep learning algorithms** — DNNs operating directly on low-level particle features

</div>

<!--
Jet tagging aims to identify a jet's origin using the available properties associated with a jet.
Developing algorithms for large-R jet tagging is more challenging due to the larger complexity
of the jet constituent particles and the diversity in the structure.
In the modern deep learning era, new opportunities arise when one can dive deep into the
low-level particle features and use an advanced neural network to explore the comprehensive
relations among the input features and different particles.
-->

---
layout: two-cols
---

# Rule-based Algorithms

Jet grooming

* **Goal**: remove soft emissions from pileup or underlying events that smear the jet mass
* Four algorithms explored in CMS and ATLAS: **jet trimming**, **jet pruning**, **jet filtering**, and **soft drop**
* All techniques recluster jet constituents into subjets to identify and remove soft components
* The **soft drop algorithm** (mMDT) is most frequently used in CMS
  - Declusters the jet and removes subjets failing a soft radiation criterion
  - Can be combined with multivariate analysis or likelihood fit for signal extraction

::right::

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_3.1.png" alt=""/>
</div>
</div>

<!--
Jet grooming techniques, initiated a decade ago, particularly aid in mass reconstruction
when the large-R jet is initiated from a resonance. These techniques aim to remove
soft emissions within a jet that come from the pileup or underlying events.
-->

---

# Rule-based Algorithms

Jet substructure: $N$-subjettiness

* $N$-subjettiness $\tau_N$ measures how well a jet can be described by $N$ subjets:

$$\tau_N = \frac{1}{d_0} \sum_{i=1}^{M} p_{T,i} \min\{\Delta R_{i,\text{sj}_1}, \Delta R_{i,\text{sj}_2}, \ldots, \Delta R_{i,\text{sj}_N}\}, \quad d_0 = \sum_{i=1}^{M} p_{T,i} R_\text{jet}$$

  where $d_0$ is the normalization factor, $M$ is the number of jet constituents, and $R_\text{jet}$ is the jet radius

* The ratio $\tau_{NM} = \tau_N / \tau_M$ optimizes separation between jet classes
  - $\tau_{21}$: tags 2-prong $W/Z/H$ jets vs QCD multijet background
  - $\tau_{32}$: identifies 3-prong hadronically decayed top jets
* **Energy correlation functions (ECFs)**: probe energy distribution without subjet axes reconstruction
  - Generalized ECF ratios (e.g. $N_2$) widely used for 2-prong jet tagging in CMS
  - Can be combined in multivariate approach for better discrimination

---

<div class="flex-column">
<div>

# Rule-based Algorithms

The shape comparison for multiple resonant types of jets and QCD background jets

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_3.2.png" alt=""/>
</div>
</div>

---

# Rule-based Algorithms

Heavy-flavour jet properties

* $b$ and $c$ quarks form hadrons with **longer lifetimes** → displaced decay tracks from the primary vertex (PV)
* Key discriminating features:
  - **Displaced tracks**: track impact parameter significance
  - **Secondary vertices (SV)**: reconstructed from displaced tracks, including SV mass, number of tracks, azimuthal relation to jet
  - **Soft leptons**: nonprompt low-$p_T$ leptons from $b/c$ hadron decays
* CMS algorithms (JP, JBP) use track impact parameter to build jet $b$-probability
* These techniques extend to large-$R$ jets for tagging $H \to bb$ or $H \to cc$ signatures

---

<div class="flex-column">
<div>

# Shallow Machine-Learning Algorithms

Multivariate approaches combining high-level features

* Combine hand-crafted variables (jet substructure, $b$-tagging properties) via BDT or shallow MLP
* **Boosted Event Shape Tagger (BEST)**: multi-class classifier ($W/Z/H/t$ jets and QCD)
  - Inputs: jet kinematics, $m_\text{SD}$, $b$-tagging properties, subjet invariant masses, sphericity
  - Variables computed in multiple Lorentz-boosted rest frames
* These approaches offer improvements but are limited by the quality of hand-crafted features

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_3.3.png" alt=""/>
</div>
</div>

---

<div class="flex-column">
<div>

# Deep Learning Algorithms

Jet representation of images and sequences

* **Jet images** (CNN): project jet onto 2D $\eta$-$\phi$ grid or 1D sequence ordered by $p_T$
  - **ImageTop** (CMS): rasterize top-jet particles into image + subjet $b$-tag network
  - **DeepAK8** (CMS): 1D CNN on particle sequence, later combined with RNN
* **DeepDoubleX** (CMS): combined CNN and GRU architecture for $X \to b\bar b/c\bar c$ tagging
* **Limitations**:
  - Jet images are sparse — many empty pixels
  - Sequential representations require a predefined ordering, conflicting with the inherent permutation symmetry of jet particles

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_3.4.png" alt=""/>
</div>
</div>

---

<div class="flex-column">
<div>

# Deep Learning Algorithms

A schematic diagram of the DeepDoubleX algorithm (V2) for boosted heavyresonant $X \to b\bar b$ and $X \to c\bar c$ tagging

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_3.5.png" alt=""/>
</div>
</div>

---

# Deep Learning Algorithms

Jet representation of sets and graphs

* Jets as **unordered sets** (point clouds) or **graphs** — respects permutation invariance
* **Particle Flow Network (PFN)**: per-particle MLP embedding followed by global pooling
* **ParticleNet**: based on Dynamic Graph CNN (DGCNN)
  - Dynamically connects each particle to its $k$ nearest neighbours in $\eta$-$\phi$ space
  - Efficiently extracts local features through EdgeConv operations
  - Achieves major performance gains in CMS for $W/Z/H/t$ and $X \to b\bar b/c\bar c$ tagging
* ParticleNet marks a turning point: **the choice of data representation is critical** for efficient and performant DNN design

---

<div class="flex-column">

# Deep Learning Algorithms

A detailed explanation of the ParticleNet architectural design

<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_3.6.png" alt=""/>
</div>
</div>

---
layout: section
---

# Part II: Algorithms for Jet Tagging

## Chapter 4: New Advances in Deep Learning Algorithms

---

# New Advances in Deep Learning Algorithms

<div class="absolute-center">

Two key insights driving progress

1. **Incorporating Lorentz symmetry**: respecting the intrinsic symmetries of jet data as an inductive bias improves both performance and robustness
2. **Transformer architectures**: Transformers, originally developed for NLP, offer superior expressiveness and scalability for jet tagging

</div>

<!--
The community for jet tagging using DNNs has widely recognized that sets (point clouds) or
graphs are more effective for representing particle-format data. Chapter 4 highlights new
insights in deep learning algorithms developed for jet tagging, after this phase of progress.
The topic will be brought up from two aspects, the consideration of symmetry preservation
within the network design, and the advances driven by the new architecture, Transformers.
-->

---

# Algorithms Preserving Lorentz Symmetry

Symmetry preservation as inductive bias

* **Principle**: if a dataset has inherent symmetries, designing the network to respect those symmetries:
  - Improves robustness to input transformations
  - Can improve performance especially under data-constrained conditions
* For jet data, permutation symmetry → use set/graph representation (already adopted)
* Additional Lorentz symmetries on top of basic $z$-$t$ boost and $x$-$y$ rotation:

| Transformation | Description |
|---|---|
| $y$-$z$ rotation | ≈ rotation in $\eta$-$\phi$ plane |
| $x$-$t$ boost | ≈ boost along the jet axis |
| $z$-tilt | mixture of $z$-$t$ boost with $x$-$z$ rotation |
| $y$-tilt | mixture of $y$-$t$ boost with $y$-$z$ rotation |

---

<div class="flex-column">
<div>

# Algorithms Preserving Lorentz Symmetry

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_4.1.png" alt=""/>
</div>
</div>

---

<div class="flex-column">
<div>

# LorentzNet

Architecture: Lorentz Group Equivariant Block (LGEB)

<small>

* Fully connected GNN with **Lorentz-invariant** scalar edge and **Lorentz-equivariant** vector node features
* Each LGEB performs three sequential updates using Minkowski inner products:
  1. **Edge feature update**: $m^l_{ij} = \phi_e(h^l_i, h^l_j, \psi((x^l_i - x^l_j)^2), \psi(x^l_i \cdot x^l_j))$
  2. **Vector node update**: $x^{l+1}_i = x^l_i + c \sum_{j \in \mathcal{N}(i)} \phi_x(m^l_{ij}) \cdot x^l_j$
  3. **Scalar node update**: $h^{l+1}_i = h^l_i + \phi_h(h^l_i, \sum_{j \in \mathcal{N}(i)} w_{ij} m^l_{ij})$
* 6 stacked LGEBs, followed by average pooling and MLP decoder

</small>

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_4.2.png" alt=""/>
</div>
</div>

---

<div class="flex-column">
<div>

# LorentzNet

Performance and robustness

* Benchmarked on Top, QG, and JetClass datasets
* **Surpasses ParticleNet** by a large margin on Top and QG datasets
* Demonstrates **robustness** to Lorentz boosts: accuracy remains constant when input jets undergo $x$-$t$ boost with parameter $\beta = v/c$, while other models (ParticleNet, PFN) show performance drops
* On JetClass LorentzNet accuracy = 0.855, outperforming ParticleNet (0.844) and ParT-plain (0.849)

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_4.3.png" alt=""/>
</div>
</div>

<!--
The performance of LorentzNet is benchmarked on the Top and QG datasets. It achieves
superior performance, surpassing ParticleNet by a large margin. In addition, as LorentzNet
is built with full Lorentz symmetry preservation, studies show the performance remains
constant when jets undergo a Lorentz boost, while other algorithms manifest a performance drop.
-->

---

# Systematic Study: Preserving Lorentz Symmetry

Quantifying the effect of different pairwise features

| Variable | Lorentz-invariant? | Additional symmetries |
|---|---|---|
| $m^2_{ij} = (p_i + p_j)^2$ | ✓ (full Lorentz) | all 4 extra |
| $\Delta R_{ij}$ | ✓ ($z$-$t$, $x$-$y$) | $y$-$z$ rotation |
| $\Delta R_{ij}(p_{T,i}+p_{T,j})$ | ✓ ($z$-$t$, $x$-$y$, $y$-$z$) | $x$-$t$ boost |
| $E_{ij} = E_i + E_j$ | ✗ (violates basic symmetries) | — |

* **Key finding**: incorporating variables invariant under more symmetry types consistently improves performance
* Effect is **strongest with limited training data** — symmetry acts as effective data augmentation
* Confirmed on both Top and JetClass datasets across training sizes from 6k to 100M

---

<div class="flex-column">
<div>

# Systematic Study: Preserving Lorentz Symmetry

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_4.4.png" alt=""/>
</div>
</div>

---

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_4.5.png" alt=""/>
</div>
</div>

<!--
Comparison of network performance on Top dataset in terms of AUC among different training data size, selected among 6 k, 20 k and 60 k, for the baseline network as ParticleNet (left) and LorentzNetbase (right)
-->

---

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_4.6.png" alt=""/>
</div>
</div>

<!--
Comparison of network performance in terms of AUC evaluated under various types of Lorentz transformation applied to the test dataset
-->

---

<div class="flex-column">
<div>

# LorentzNet

Comparison of network performance of the PFN, ParticleNet and LorentzNetbase variants incorporating different nodewise features

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Table_4.3.png" alt=""/>
</div>
</div>

---

# The Transformer Algorithm

* **Self-attention** naturally fits particle-format data:
  - Captures long-range dependencies between all pairs of particles (fully connected graph)
  - No predefined token ordering needed — particles are inherently permutation invariant
* **Scaling advantage**: Transformers improve more with larger datasets
  - At 2M samples: ParT ≈ ParticleNet performance
  - At 100M samples (JetClass): ParT dramatically outperforms ParticleNet

| Model | Training size | Accuracy | $H \to bb$ Rej50% |
|---|---|---|---|
| ParticleNet | 2M | 0.828 | 5540 |
| ParticleNet | 100M | 0.844 | 7634 |
| ParT | 2M | 0.836 | 5587 |
| ParT | 100M | **0.861** | **10638** |

---

<div class="flex-column">
<div>

# The Transformer Algorithm

Performance of ParticleNet and ParT trained with different data sizes of JETCLASS

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Table_4.4.png" alt=""/>
</div>
</div>

---

# Particle Transformer (ParT)

Architecture overview

* **Backbone**: $L = 8$ Particle Attention Blocks + 2 Class Attention Blocks
* **Key innovation**: incorporates **pairwise features** as attentive bias in attention mechanism
* Pairwise features for particle pair $(i, j)$:
  - $\Delta R_{ij}$ — angular separation
  - $k_{T,ij} = \min(p_{T,i}, p_{T,j}) \Delta R_{ij}$ — $k_T$-type variable
  - $z_{ij} = \min(p_{T,i}, p_{T,j}) / (p_{T,i} + p_{T,j})$ — momentum fraction
  - $m^2_{ij} = (p_i + p_j)^2$ — pairwise invariant mass (fully Lorentz-invariant)
* Modified attention: $\text{P-MHA}(Q, K, V, U) = \text{softmax}\left(\frac{QK^T}{\sqrt{d}} + U\right) V$
  - $U$ is the embedded pairwise feature matrix — provides Lorentz-symmetry inductive bias

---

<div class="flex-column">
<div>

# Particle Transformer (ParT)

A schematic diagram of the Particle Transformer architecture (a), the Particle Attention Block (b) and Class Attention Block \(c\)

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_4.8.png" alt=""/>
</div>
</div>

---

<div class="flex-column">
<div>

# Particle Transformer (ParT)

A schematic diagram of the universal network-modifying recipe for all baseline networks to incorporate additional nodewise features

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_4.7.png" alt=""/>
</div>
</div>

---

# Particle Transformer (ParT)

Performance comparison

| Model | Accuracy | AUC | Rej50% (top) | FLOPs |
|---|---|---|---|---|
| PFN | 0.772 | 0.9714 | 2924 | 4.62 M |
| ParticleNet | 0.844 | 0.9849 | 7634 | 540 M |
| LorentzNet | 0.855 | 0.9869 | 9217 | 2.01 G |
| ParT (plain) | 0.849 | 0.9859 | 9569 | 260 M |
| **ParT** | **0.861** | **0.9877** | **10638** | 340 M |

* ParT achieves **highest performance** with **moderate computational cost**
* ParT has 6× more parameters than ParticleNet but **similar FLOPs** — efficient Transformer design
* LorentzNet achieves high accuracy but with ~6× higher FLOPs than ParT due to fully-connected GNN

---

<div class="flex-column">
<div>

# Particle Transformer (ParT)

Comparison of jet tagging performance on the top tagging dataset with multiple algorithms

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Table_4.5.png" alt=""/>
</div>
</div>

---

<div class="flex-column">
<div>

# Particle Transformer (ParT)

Comparison of jet tagging performance on the quark–gluon tagging dataset with multiple algorithms

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Table_4.6.png" alt=""/>
</div>
</div>

---

# Discussion: Future Directions in DNN Algorithms

Three potential directions for Transformer-based models

1. **Scaling**: investigate effect of scaling up model size on 100M+ datasets; explore whether larger data continues to improve performance → motivates work in Part V
2. **Multi-task capability**: leverage Transformers' large capacity to handle complex, multi-class, or multi-modal tasks → explored in GloParT (Part V)
3. **Efficiency improvement**:
   - Adopt efficient Transformer variants (linear attention, etc.)
   - Address quadratic complexity of pairwise feature computation (≈ 20% of ParT's compute)
   - Find alternative methods to incorporate Lorentz symmetry without full pairwise computation

---
layout: section
---

# Part III: Calibration of Jet Taggers

## Chapter 5: Introduction to Boosted-jet Flavour Tagger Calibration

---

# Why Calibration is Needed

The simulation-to-data discrepancy problem

* When a jet tagger is deployed in an LHC physics analysis, a **calibration** step is required
* DNN-based taggers are trained on simulated jets → may capture simulation-specific patterns not present in real data
* **Scale Factor (SF)**: ratio of tagging efficiency in data vs. simulation

$$\text{SF} = \frac{\epsilon_{\text{data}}}{\epsilon_{\text{MC}}}$$

* Deeper and more complex networks tend to **amplify** the data-simulation discrepancy
* SFs depend on the tagger working point, jet $p_T$, and data-taking conditions
* Focus of Part III: calibrating **boosted-jet flavour taggers** ($X \to b\bar b$ and $X \to cc$ algorithms)

---

# Overview of Boosted-jet Flavour Taggers

Target: identify large-$R$ jets from $X \to b\bar b$ or $X \to cc$ decays

* Applications: Higgs boson searches ($H \to bb/cc$), BSM resonance searches
* Key characteristic: **two-prong structure** with displaced tracks or SVs in each prong
* All taggers must be **mass-decorrelated** to avoid sculpting the background mass distribution

Four $X \to b\bar b/c\bar c$ taggers in CMS:

| Tagger | Architecture | Mass decorrelation |
|---|---|---|
| double-b | BDT (SV + track features) | variable selection |
| DeepAK8-MD | 1D CNN (ResNet) | adversarial training |
| DeepDoubleX | CNN + GRU | mass spectrum reweighting |
| **ParticleNet-MD** | Graph CNN | mass spectrum reweighting |

---

<div class="flex-column">
<div>

# Overview of Boosted-jet Flavour Taggers

ParticleNet-MD shows **largely enhanced** separating power versus QCD background

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_5.1.png" alt=""/>
</div>
</div>

<!--
Illustration on large-𝑅 jet topologies with different origins. The first two cases fall under the category of boosted-jet flavour tagging
-->

---

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_5.2.png" alt=""/>
</div>
</div>

<!--
The normalized distributions of the $X \to b\bar b$ and $X \to c\bar c$ discriminants on the simulated signal 𝐻 → 𝑏𝑏 and 𝐻 → 𝑐𝑐 jets, the bb and cc components of QCD multijet background jets, and inclusive QCD jets
-->

---

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.1.png" alt=""/>
</div>
</div>

<!--
Performance comparison of the $X \to b\bar b$ (top) and $X \to c\bar c$ (bottom) identification algorithms in terms of ROC curves for 𝐻 →𝑏𝑏 or 𝐻 →𝑐𝑐 signal jets versus the inclusive QCD jets as background
-->

---

# Calibration Challenge

Why $H \to bb/cc$ calibration is hard

* For top/$W$ jet taggers: pure calibration samples available in data (e.g. $t\bar{t}$ events)
* For $H \to bb/cc$: **impossible** to obtain pure $H \to bb/cc$ sample in data
* Solution: use **proxy jets** with characteristics similar to signal jets

Two proxy approaches:
1. **Gluon-splitting jets** ($g \to bb/cc$): abundant in QCD multijet events; require special selection to improve similarity to $H \to bb/cc$
   - Previous method: SV-based reweighting (works for double-b, fails for advanced ParticleNet-MD)
2. **$Z \to bb$ jets**: more direct proxy, but fewer statistics and larger SF uncertainties due to non-resonant hadronic background

→ **Challenge**: a more performant tagger better discriminates $g \to bb$ from $H \to bb$, making gluon-splitting proxies less suitable

---

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.2.png" alt=""/>
</div>
</div>

<!--
The mass decorrelation performance on the QCD multijet background for various $X \to b\bar b$ and $X \to c\bar c$ discriminants
-->

---
layout: section
---

# Part III: Calibration of Jet Taggers

## Chapter 6: A Novel Calibration Method — sfBDT

---

# The sfBDT Method

Key idea: multivariate selection of signal-like gluon-splitting jets

* **sfBDT** = BDT for Scale Factor derivation
* Strategy: train a BDT to distinguish two subsets of $g \to bb/cc$ QCD jets:
  - **Signal-like jets**: low gluon contamination, closer to $H \to bb/cc$
  - **Gluon-contaminated jets**: contain additional ISR/FSR radiation, less signal-like
* Apply sfBDT selection to retain only signal-like proxy jets
* **Two generations** of sfBDT design:
  1. Based on **generator-level partons** (gluon contamination fraction $\kappa_g$)
  2. Based on **generator-level hadrons** (N-subjettiness $\tau_{31}^h$ of first-generation hadrons)

---

# The sfBDT Method

Data and simulated samples

* **Data**: proton-proton collisions at 13 TeV, Run 2 (2016–2018), 138 fb$^{-1}$
* **Trigger**: logical OR of multiple $H_T$ triggers (125–900 GeV) — expands jet statistics in low $p_T$ region
* **MC samples**: QCD multijet (dominant), $V(\to qq)$+jets, $t\bar{t}$, single top
* **Key**: use same PYTHIA parton shower generator for both $H \to bb/cc$ signal and $g \to bb/cc$ proxy jets — DNN performance is sensitive to parton shower patterns
* **MC-to-data reweighting**: 3D grid on (event $H_T$, jet $p_T$, jet index) to compensate for trigger prescaling effects

---

<div class="flex-column">
<div>

# The sfBDT Method

The number of data events passing the jet 𝐻T triggers with different thresholds and passing the logical OR of all triggers, for the 2016 post-VFP (left) and 2018 (right) detector conditions as an example

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.3.png" alt=""/>
</div>
</div>

---

<div class="flex-column">
<div>

# The sfBDT Method

Summary of the MC and data yields (upper panel for each plot) and the MC-todata reweighting factors (lower panel) for the 2018 data on the 3D variables (event 𝐻T, jet 𝑝T, jet index)

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.4.png" alt=""/>
</div>
</div>

---

# The sfBDT Method

Jet selection and flavour categorization

- $p_T > 200$ GeV, $|\eta| < 2.4$, $50 < m_\text{SD} < 200$ GeV
- At least one SV matched to **each** of the two soft-drop subjets

| Category | Definition |
|---|---|
| "bb" | Both subjets matched to ≥1 $b$-hadron |
| "b" | Jet (not both subjets) matched to ≥1 $b$-hadron |
| "cc" | Both subjets matched to ≥1 $c$-hadron |
| "c" | Jet (not both subjets) matched to ≥1 $c$-hadron |
| "light" | Otherwise |

* **Proxy jets**: flvB (flvC) component after SV requirement + sfBDT selection, for $X \to b\bar b$ ($X \to c\bar c$)

---
layout: two-cols
---

# sfBDT Design

Generation 1: parton-level gluon contamination

* **Observation**: $g \to cc$ jets contain more extra gluons from ISR/FSR compared to $H \to cc$ jets
* Define gluon contamination rate:

$$\kappa_g = \frac{\sum_{i \in \{g\}} p_{T,i}}{\sum_{i \in \{g,q\}} p_{T,i}}$$

* **BDT training**: signal-like ($\kappa_g < 0.15$) vs gluon-contaminated ($\kappa_g > 0.85$) QCD jets
* **6 input features**: $\tau_{21}$, $M_{\text{sj1}}$, $M_{\text{sj2}}$, $N_\text{tracks from SV1,2}$, $p_{T,\text{SV1}}$, $p_{T,\text{SV2}}$
* **10-fold cross-validation** to avoid overfitting
* Tighter sfBDT selection → proxy jets more signal-like

::right::

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.5.png" alt=""/>
</div>
</div>

<!--
The 𝜅𝑔 distributions of large-𝑅 jets for the signal 𝐻 → 𝑐𝑐 jets and the 𝑔 → 𝑐𝑐 jets selected from QCD multijet events
-->

---

<div class="flex-column">
<div>

# sfBDT Design

A 2D histogram on the tagging discriminant (ParticleNet-MD $X \to b\bar b$𝑐𝑐 developed for AK15 jets) versus the sfBDT score, for the 𝐻 →𝑐𝑐 (left) and the 𝑔 →𝑐𝑐 (right) jets

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.6.png" alt=""/>
</div>
</div>

---

<div class="flex-column">
<div>

# sfBDT Design

The distributions of the tagging discriminant (ParticleNet-MD $X \to b\bar b$𝑐𝑐 developed for AK15 jets)

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.7.png" alt=""/>
</div>
</div>

---

# sfBDT Design

Generation 2: hadron-level N-subjettiness

* **Motivation for upgrade**: gluon fraction misses additional quark radiation; parton patterns are generator-dependent
* New metric: **$\tau_{31}^h$** — N-subjettiness computed on first-generation hadrons

$$\tau_{31}^h = \frac{\sum_{i \in \text{had.}} p_{T,i} \min[\Delta R_{i,\hat{n}_{3,1}}, \Delta R_{i,\hat{n}_{3,2}}, \Delta R_{i,\hat{n}_{3,3}}]}{\sum_{i \in \text{had.}} p_{T,i} \Delta R_{i,\hat{n}_{1,1}}}$$

  where $\hat{n}_{1,1}$ is the direction of the vector sum of all hadron momenta, and $\hat{n}_{3,j}$ ($j=1,2,3$) are the three subjet axes from exclusive $k_T$ clustering of first-generation hadrons

* Signal-like: $\tau_{31}^h < 0.1$; background-like: $\tau_{31}^h > 0.1$
* **Advantages**: uses hadron-level physics (more generator-independent), captures both gluon and quark extra radiation
* Implemented in Run-2 published calibration results

---
layout: two-cols
---

# sfBDT Coastlines

Automatic determination of sfBDT selection

<small>

* A **tagger transformation** $\tilde{x} = T(x)$ maps the signal tagger shape to uniform distribution on $(0, 1)$
* **sfBDT coastlines**: contours of the cumulative 2D PDF on the tagger–sfBDT plane

$$F_y(x, y) = \int_y^1 f(x, y') \,dy'$$

  where $f(x, y')$ is the joint 2D probability density function

* 9 coastlines selected, corresponding to contours at $F_y = \frac{k}{N} F_y(0.6, 0)$ for $k = 3, \ldots, 11$, $N = 12$
* **Key property**: for each coastline, the selected proxy jet collection has the **same tagger discriminant shape** as the signal jets (uniform distribution)
* 9 coastlines × 9 "coast number" options = **81 SF measurements** per working point

</small>

::right::

<div class="flex-column items-center justify-center h-full">
<img border="rounded" src="/part_II-III/Figure_6.8.png" alt=""/>
<small>

The cartoon of a $g \to b\bar b (c\bar c)$ jet with an additional parton emission in the format of Feynman diagrams

</small>
</div>

---

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.9.png" alt=""/>
</div>
</div>

<!--
The example plots for the tagger transformation map, the original tagger shape and the transformed tagger shape for the ParticleNet-MD (top) and DeepDoubleX (bottom)
-->

---

<div class="flex-column">
<div>

# sfBDT Coastlines

The 2D histogram of the tagger–sfBDT variable (the coloured pixels), and illustration of the “sfBDT coastlines” (left), the distribution of the tagging discriminant of proxy jets with (center) and without (right) normalized to unity

</div>
<div class="flex justify-center">
<img border="rounded" src="/part_II-III/Figure_6.10.png" alt=""/>
<img border="rounded" src="/part_II-III/Figure_6.13.png" alt=""/>
</div>
</div>

<style>
img {
  display: block;
  max-height: 270px;
  width: auto;
  height: auto;
}
</style>

---

<div class="flex-column">
<div>

# sfBDT Coastlines

The sfBDT coastlines derived in the context of calibrating the ParticleNet-MD $X \to b\bar b$ discriminants in three exclusive $p_T$ bins

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.11.png" alt=""/>
</div>
</div>

---

# Scale Factor Derivation

Template maximum likelihood fit

* **Fit variable**: $\log(M_{\text{SV1, max}(\sigma_{d_{xy}})}/\text{GeV})$ — mass of the SV with maximum $d_{xy}$ significance
* **Three flavour components**: flvB, flvC, flvL — each with a free-floating yield scale factor in the tagger-selected region
* The **flvB (flvC) scale factor = SF** for $X \to b\bar b$ ($X \to c\bar c$) calibration
* SFs derived for:
  - 4 data-taking eras (2016 pre/post-VFP, 2017, 2018)
  - 3 working points (HP, MP, LP)
  - 3 $p_T$ bins: (450, 500), (500, 600), (600, ∞) GeV
* **Systematic uncertainties**: jet energy scale/resolution, $b/c$ tagging, pileup, plus dedicated **sfBDT coastline variation** uncertainty

---

<div class="flex items-center justify-center">
<img class="img1" border="rounded" src="/part_II-III/Figure_6.14.png" alt=""/>
<img class="img2" border="rounded" src="/part_II-III/Figure_6.15.png" alt=""/>
</div>

<style>
img {
  display: block;
  width: auto;
  height: auto;
}
.img1 {
  max-height: 480px;
}
.img2 {
  max-height: 270px;
}
</style>

<!--
Left: Comparison of the signal and proxy jets on a collection of jet observables. The observables are related to high-level properties of the jet, subjets, tracks, and SVs

Right: Illustration on the choices of “sfBDT coastline” selections applied for an individual fit
-->

---

<div class="flex-column">
<div>

# sfBDT Results

The separation power of signal and proxy jets illustrated in terms of the ROC curve, where the proxy jet collection is defined by a selection on the sfBDT coastline (left), data and MC comparison on the transformed ParticleNet-MD $X \to b\bar b$ (center) and $X \to c\bar c$ (right) tagging discriminants in 2018 data-taking condition, before the sfBDT selection is applied

</div>
<div class="flex justify-center">
<img border="rounded" src="/part_II-III/Figure_6.16.png" alt=""/>
<img border="rounded" src="/part_II-III/Figure_6.18.png" alt=""/>
</div>
</div>

<style>
img {
  display: block;
  max-height: 270px;
  width: auto;
  height: auto;
}
</style>

---

<div class="flex-column">
<div>

# sfBDT Results

Data and MC comparison on the transformed ParticleNet-MD $X \to b\bar b$ tagging discriminants in 2018 data-taking condition, after the sfBDT coastline selection applied

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.19.png" alt=""/>
</div>
</div>

---

# Calibration Results

Scale factors for ParticleNet-MD $X \to b\bar b$ and $X \to cc$

* **81 SF measurements** per (WP, $p_T$ bin, era) are combined via envelope method
* Results for ParticleNet-MD $X \to b\bar b$ discriminant SFs (2016–2018, HP WP, $p_T > 450$ GeV):

| Era | $p_T$ range | SF |
|---|---|---|
| 2018 | 450–500 GeV | $\approx 1.0 \pm 0.1$ |
| 2018 | 500–600 GeV | $\approx 1.0 \pm 0.1$ |
| 2018 | 600+ GeV | $\approx 1.0 \pm 0.1$ |

* **Derived SFs are around unity** — confirms simulation-to-data consistency for ParticleNet-MD
* Results are part of **published CMS results** (CMS-PAS-BTV-22-001)
* sfBDT SFs applied in **numerous CMS analyses** including the VHcc measurement (Part IV)

---

<div class="flex-column">
<div>

# Calibration Results

Data and MC comparison on the fit variable for the inclusive “pass”+“fail” region, passing the middle sfBDT coastline selection

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.21.png" alt=""/>
</div>
</div>

---

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.22.png" alt=""/>
</div>
</div>

<!--
Pre-fit and post-fit distributions on the fit variable for the “pass” (left) and “fail” (right) region in the context of calibrating the ParticleNet-MD $X \to b\bar b$
-->

---

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_6.24.png" alt=""/>
</div>
</div>

<!--
Summary of the ParticleNet-MD $X \to b\bar b$ tagging discriminant SFs in the plot format, separately shown for four data-taking conditions
-->

---

# Summary: Part II and Part III

Key takeaways

**Part II — Algorithms**:
- Historical evolution: rule-based → shallow ML → deep learning
- **Lorentz symmetry preservation** as inductive bias: pairwise invariant masses ($m_{ij}^2$) give best performance gains, especially with limited data
- **LorentzNet**: first fully Lorentz-equivariant GNN, demonstrates robustness and superior performance
- **Particle Transformer (ParT)**: Transformer with pairwise attentive bias, achieves state-of-the-art performance with efficient computation; scales well with data size

**Part III — Calibration**:
- Advanced DNN taggers (ParticleNet-MD) require new calibration approaches
- **sfBDT method**: trains a BDT to select signal-like $g \to bb/cc$ proxy jets; introduces two designs (parton-level and hadron-level)
- Delivers robust scale factors for 7 taggers in CMS, applied in many physics analyses
