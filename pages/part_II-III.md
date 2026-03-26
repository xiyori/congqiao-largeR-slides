---
layout: section
---

# Part II: Algorithms for Jet Tagging

## Chapter 3: Algorithm Overview

<!-- 
Part II of the thesis surveys the evolution of jet tagging algorithms from hand-crafted rule-based approaches through shallow machine learning to modern deep learning. Chapter 3 provides the historical overview and context, covering three generations of algorithms: rule-based methods exploiting jet substructure and heavy-flavour properties, shallow ML methods combining high-level features with BDTs or MLPs, and deep learning methods operating directly on low-level particle data. This evolution motivates why deep learning — and in particular the choice of data representation — is so important for jet tagging performance.
-->

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

<!-- 
N-subjettiness is one of the most powerful and widely-used jet substructure variables. The key insight is that if a jet has N prongs, it should be well-described by N subjet axes — so τN will be small for an N-prong jet. The ratio τNM = τN/τM provides excellent discrimination: τ21 separates 2-prong (W/Z/H) jets from single-prong QCD jets, while τ32 separates 3-prong (top) jets from 2-prong jets. Energy correlation functions (ECFs) offer an alternative approach without requiring explicit subjet axes, and their ratios like N2 have been adopted as the standard mass-decorrelated tagger in CMS for W/Z tagging. These variables form the baseline against which all more sophisticated algorithms are compared.
-->

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

<!-- 
This figure shows the distributions of jet substructure variables (such as τ21 and τ32) for different jet types — W jets, Z jets, Higgs jets, top jets, and QCD multijet background. The clear separation between signal jet classes and background in these distributions demonstrates why N-subjettiness is effective: resonance jets with a well-defined number of prongs produce characteristic substructure patterns. However, the overlap between different signal classes (e.g., W vs. H) also illustrates why these simple variables are insufficient for the multi-class discrimination needed in modern analyses, motivating the need for more powerful machine learning approaches.
-->

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

<!-- 
Heavy-flavour jet tagging exploits the fact that b and c quarks form hadrons with lifetimes long enough to travel a measurable distance before decaying. This creates displaced tracks with large impact parameter significance and reconstructed secondary vertices offset from the primary interaction point. The combination of SV mass, number of tracks, and their azimuthal alignment with the jet axis provides strong discrimination between bb/cc jets and light-quark or gluon jets. For large-R jets from H→bb or H→cc, the key challenge is that the two b or c hadrons land in separate subjets — requiring the algorithm to identify heavy-flavour signatures in both subjets simultaneously.
-->

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

<!-- 
Shallow machine learning algorithms improve on rule-based methods by combining many hand-crafted features simultaneously. The Boosted Event Shape Tagger (BEST) is a notable example: it computes jet properties in multiple Lorentz-boosted rest frames and feeds them into a BDT or MLP for multi-class classification. Computing variables in boosted frames provides additional discriminating information because the jet substructure looks different depending on the frame. However, these approaches are fundamentally limited by the expressiveness of the hand-crafted input features — no matter how cleverly designed, human-engineered variables cannot capture all the information in the full particle-level data.
-->

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

<!-- 
The first generation of deep learning jet taggers treated jets as images or sequences — natural choices given the dominance of CNNs and RNNs in early deep learning. Jet images project particle momenta onto a 2D η-φ grid for CNN processing, while sequential representations order particles by pT for 1D CNNs or RNNs. CMS deployed these approaches in ImageTop and DeepAK8. DeepDoubleX combined both CNN and GRU branches to capture different aspects of the jet structure. However, jet images are inherently sparse — most pixels are empty — and sequential representations impose an arbitrary ordering on particles that are physically unordered, both of which limit efficiency and expressiveness.
-->

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

<!-- 
This figure shows the architecture of the DeepDoubleX algorithm (V2), which was developed specifically for boosted X→bb̄ and X→cc̄ tagging in CMS. The network combines two branches: a CNN processing ordered particle sequences, and a GRU processing track and secondary vertex features. The two branches are concatenated and passed through a fully-connected network for final classification. DeepDoubleX was the state-of-the-art CMS tagger before ParticleNet and represents the transition from simple 1D CNNs to more complex multi-branch architectures. Its two-branch design reflects the challenge of combining both global jet structure information and local heavy-flavour signatures.
-->

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

<!-- 
Treating jets as unordered sets or graphs — rather than images or sequences — is now recognized as the most natural and effective representation for particle-format data. The Particle Flow Network (PFN) demonstrated that per-particle embeddings followed by a permutation-invariant global pooling operation can achieve competitive performance. ParticleNet went further by using Dynamic Graph CNN, connecting each particle to its k nearest neighbors in η-φ space and applying EdgeConv operations to extract local geometric features. ParticleNet delivered major performance gains over all previous CMS taggers and became the new standard for large-R jet tagging, deployed in the analyses that form the backbone of Part III and Part IV of this thesis.
-->

---

<div class="flex-column">

# Deep Learning Algorithms

A detailed explanation of the ParticleNet architectural design

<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_3.6.png" alt=""/>
</div>
</div>

<!-- 
This figure provides a detailed view of the ParticleNet architecture. The core component is the EdgeConv block: for each particle, k nearest neighbors in η-φ space are found, edge features are computed between the central particle and each neighbor, and these are aggregated to update the particle representation. Stacking multiple EdgeConv blocks allows the network to build up increasingly global representations. A channel-wise global average pooling layer combines all particle representations into a single jet-level feature vector, which is passed through a classification network. The dynamic graph construction — recalculated at each layer in the learned feature space — allows the network to capture both local geometric and global semantic relationships between particles.
-->

---
layout: section
---

# Part II: Algorithms for Jet Tagging

## Chapter 4: New Advances in Deep Learning Algorithms

<!-- 
Chapter 4 focuses on the two most significant advances in jet tagging deep learning algorithms developed as part of this thesis work: incorporating Lorentz symmetry as an inductive bias (leading to LorentzNet), and applying Transformer architectures to jet data (leading to Particle Transformer, ParT). These two advances address complementary aspects of the problem: Lorentz symmetry provides a physics-motivated prior that improves robustness and data efficiency, while Transformers provide superior expressiveness and scalability. Together they represent the current state of the art in jet tagging and form the algorithmic core of this PhD thesis.
-->

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

<!-- 
The principle of symmetry preservation as an inductive bias is well-established in machine learning: if the data has a known symmetry, building networks that respect it reduces the effective parameter space, improves generalization, and can dramatically improve performance under limited data. For jet data, we already exploit permutation symmetry via set/graph representations. The additional Lorentz symmetries beyond the basic z-t boost and x-y rotation include four types of transformations that a jet system should be invariant under. Designing networks that respect these additional symmetries — especially the fully Lorentz-invariant combination — is the motivation for LorentzNet.
-->

---

<div class="flex-column">
<div>

# Algorithms Preserving Lorentz Symmetry

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_4.1.png" alt=""/>
</div>
</div>

<!-- 
Figure 4.1 illustrates the four additional Lorentz transformation types beyond basic boosts and rotations that are relevant for jet physics. Each transformation has a distinct physical interpretation and acts differently on the particle four-momenta in the jet rest frame. The y-z rotation is approximately a rotation in the η-φ plane; the x-t boost is approximately a boost along the jet axis; the z-tilt and y-tilt are mixed transformations. LorentzNet is designed to be equivariant under all of these transformations by using Minkowski inner products as the fundamental building block of its edge and node feature computations.
-->

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

<!-- 
LorentzNet's architecture is built around the Lorentz Group Equivariant Block (LGEB), which simultaneously maintains two types of node features: Lorentz-invariant scalar features h (regular real-valued vectors) and Lorentz-equivariant vector features x (four-momenta that transform covariantly). The key innovation is using Minkowski inner products — both the squared norm (x_i - x_j)² and the dot product x_i · x_j — as edge features in the message-passing scheme. These products are by construction Lorentz-invariant, so the network's learned representations respect Lorentz symmetry automatically. The fully-connected graph structure (every particle communicates with every other) ensures no pairwise relationship is missed, at the cost of O(N²) computational complexity.
-->

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

<!-- 
This systematic study directly addresses the question: does incorporating Lorentz-invariant features into a network actually improve performance? The answer is nuanced and data-size dependent. By ablating different pairwise features in a controlled graph network, we find that features invariant under more Lorentz symmetry types consistently perform better, with the fully invariant pairwise invariant mass m²_ij providing the greatest benefit. Crucially, the effect is strongest when training data is scarce — with 6k training jets, symmetry-preserving features provide a large advantage; with 100M jets, the gap narrows as the network can learn symmetries from data alone. This confirms that Lorentz symmetry acts as an effective data augmentation, reducing the sample complexity needed to learn good representations.
-->

---

<div class="flex-column">
<div>

# Systematic Study: Preserving Lorentz Symmetry

</div>
<div class="center-container">
<img border="rounded" src="/part_II-III/Figure_4.4.png" alt=""/>
</div>
</div>

<!-- 
Figure 4.4 shows the systematic comparison of different pairwise interaction features across varying training sizes and datasets. The x-axis shows training data size (from 6k to 100M) and the y-axis shows classification performance (AUC). Each line represents a different type of pairwise feature, ordered by their degree of Lorentz invariance. The clear ordering — fully Lorentz-invariant features (m²_ij) consistently on top, symmetry-violating features (E_ij) consistently at the bottom — demonstrates that the choice of feature is the primary driver of performance, especially in the low-data regime where the gap between designs is largest.
-->

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

<!-- 
Table 4.3 compares the performance of PFN, ParticleNet, and several LorentzNet variants that incorporate different combinations of node-wise features on the Top and QG datasets. This ablation study isolates the contribution of different input features to the overall performance gain of LorentzNet. The results demonstrate that both the Lorentz-equivariant vector features and the Lorentz-invariant scalar features contribute to performance, and that the combination with Minkowski-product-based edge features provides the best overall results. This validates the design principle of LorentzNet as a genuinely Lorentz-equivariant architecture.
-->

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

<!-- 
The Transformer architecture, originally developed for natural language processing, turns out to be exceptionally well-suited for jet data. Self-attention naturally handles permutation-invariant particle sets — it computes all-pairs interactions without requiring a predefined ordering, effectively treating each particle as a "token." The key difference from standard sequence Transformers is the absence of positional encodings. The table on this slide demonstrates the most striking property of Transformers: their performance scales dramatically with training data size. At 2M training samples, ParT slightly outperforms ParticleNet; at 100M samples, ParT achieves a dramatically higher background rejection at 50% signal efficiency (10638 vs 7634), illustrating the data-hungry but high-capacity nature of Transformer architectures.
-->

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

<!-- 
This table presents a detailed breakdown of the performance scaling of ParticleNet and ParT across all ten JetClass classes as training data grows from 2M to 100M jets. The pattern is consistent: both models improve with more data, but ParT improves much more steeply. This data-scaling advantage is a hallmark of the Transformer architecture — its large parameter count and expressive attention mechanism allow it to continue learning from additional data even at 100M samples, while simpler models plateau earlier. This finding directly motivates the pre-training work in Part V of the thesis, where the goal is to leverage even larger training sets and transfer learning to push performance further.
-->

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

<!-- 
The Particle Transformer (ParT) architecture makes two key design choices beyond a standard Transformer. First, it incorporates pairwise interaction features — ΔR_ij, k_{T,ij}, z_ij, and the Lorentz-invariant m²_ij — as additive biases in the attention logits. This allows the network to directly attend to physically meaningful particle-particle relationships rather than learning them implicitly from individual particle features alone. Second, it uses Class Attention Blocks (after the Particle Attention Blocks) where a special "class token" attends to all particles to produce the final classification representation. The use of m²_ij as one of the four pairwise features directly incorporates the Lorentz symmetry insight from the LorentzNet study.
-->

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

<!-- 
Figure 4.8 shows the full ParT architecture schematic. Panel (a) shows the overall structure: particle inputs go through an embedding layer, then L=8 Particle Attention Blocks, then 2 Class Attention Blocks, and finally a classification head. Panel (b) details the Particle Attention Block: pairwise features are embedded to form the matrix U, which is added to the standard QK^T/√d attention logits before softmax, allowing the pairwise physics features to directly modulate attention scores. Panel (c) shows the Class Attention Block: a learnable class token attends over all particle representations and accumulates a global jet summary. This architecture achieves an excellent balance between expressiveness and computational efficiency.
-->

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

<!-- 
Figure 4.7 shows the universal recipe for incorporating additional node-wise features into any baseline network architecture — a generalizable methodology not specific to ParT. The recipe works by embedding the additional features (such as particle type, charge, or displacement) into the same dimensionality as the main feature vector, then adding this embedding at each layer of the network. This modular approach allows systematic ablation studies comparing the contribution of different input feature types, and was used to investigate the effect of Lorentz-invariant pairwise features across multiple baseline architectures beyond just ParT.
-->

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

<!-- 
This performance comparison table is the central quantitative result of Chapter 4. ParT achieves the highest accuracy (0.861) and background rejection at 50% signal efficiency (10638) on the JetClass dataset, surpassing LorentzNet (0.855, 9217) and ParticleNet (0.844, 7634). Crucially, ParT achieves this with only 340M FLOPs — similar to ParticleNet and approximately 6× fewer than LorentzNet. This demonstrates that the Transformer architecture achieves a superior performance-to-compute tradeoff: the pairwise attentive bias provides Lorentz-symmetry benefits at minimal computational cost, while the attention mechanism allows efficient long-range particle interactions without the O(N²) cost of a fully-connected GNN.
-->

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

<!-- 
Table 4.5 shows the comprehensive benchmarking of ParT and all comparison algorithms on the Top tagging dataset. The table lists accuracy, AUC, and background rejection at 50% and 30% signal efficiency for all models. ParT consistently leads across all metrics, with the AUC of 0.9877 compared to 0.9869 for LorentzNet and 0.9849 for ParticleNet. The top tagging task is particularly sensitive to the network's ability to capture the three-prong substructure of hadronic top decays, and the pairwise attentive bias in ParT allows it to model these three-body correlations more effectively than methods that operate on single-particle features.
-->

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

<!-- 
Table 4.6 presents the quark-gluon tagging benchmark results. The QG task is structurally different from the Top task: it involves small-R jets and a binary discrimination between quark-initiated and gluon-initiated jets based on subtle differences in multiplicity, particle composition, and radiation patterns. ParT again leads the field, confirming that its advantages are not specific to complex multi-prong topologies but generalize to simpler jet classification tasks as well. The particle identification features (distinguishing electron, muon, photon, charged hadron, neutral hadron types) are particularly important for the QG task, and ParT effectively leverages these through its multi-head attention mechanism.
-->

---

# Discussion: Future Directions in DNN Algorithms

Three potential directions for Transformer-based models

1. **Scaling**: investigate effect of scaling up model size on 100M+ datasets; explore whether larger data continues to improve performance → motivates work in Part V
2. **Multi-task capability**: leverage Transformers' large capacity to handle complex, multi-class, or multi-modal tasks → explored in GloParT (Part V)
3. **Efficiency improvement**:
   - Adopt efficient Transformer variants (linear attention, etc.)
   - Address quadratic complexity of pairwise feature computation (≈ 20% of ParT's compute)
   - Find alternative methods to incorporate Lorentz symmetry without full pairwise computation

<!-- 
The success of ParT opens several important research directions for the community. On scaling, the question is whether the performance plateau typical of ParticleNet-like models has been overcome — does ParT continue to improve with even larger datasets beyond 100M jets? This motivated the GloParT pre-training work in Part V. On multi-task capability, can Transformers handle the full diversity of LHC jet classification tasks within a single model, learning shared representations that transfer across jet types? This is the foundation of the Sophon model. On efficiency, the O(N²) cost of pairwise feature computation grows quadratically with jet constituent count, which is manageable for jets with ~100 particles but could become a bottleneck for future high-luminosity LHC conditions.
-->

---
layout: section
---

# Part III: Calibration of Jet Taggers

## Chapter 5: Introduction to Boosted-jet Flavour Tagger Calibration

<!-- 
Part III shifts from algorithm development to the critical experimental challenge of deploying DNN jet taggers in real CMS analyses. Chapter 5 introduces the calibration problem: DNNs trained on simulation may not perform identically on real data due to simulation-to-data discrepancies, requiring scale factors derived from control samples. For boosted-jet flavour taggers like ParticleNet-MD targeting H→bb̄ and H→cc̄, this calibration is particularly challenging because no pure signal sample exists in data — we must rely on proxy jets whose properties approximate those of signal. This chapter sets up the motivation for the novel sfBDT calibration method introduced in Chapter 6.
-->

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

<!-- 
Calibration is a mandatory step before any DNN tagger can be used in an official CMS physics analysis. The scale factor (SF = ε_data/ε_MC) corrects for the fact that DNN taggers trained on simulation may have different efficiencies when applied to real collision data. More complex and powerful DNNs — like ParticleNet-MD — tend to amplify data-simulation discrepancies because they extract more information from the data, including subtle patterns that simulations may not accurately model. Scale factors must be measured as a function of jet pT, working point, and data-taking year, and their uncertainties directly impact the final physics result. This is why a reliable calibration method for advanced taggers is a critical prerequisite for using them in precision analyses.
-->

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

<!-- 
This slide summarizes the four main CMS boosted-jet flavour taggers targeting X→bb̄ and X→cc̄ signatures. All four must be mass-decorrelated — meaning their discriminant scores must not sculpt the jet mass distribution of background jets — to avoid creating artificial peaks in signal-sensitive mass regions. The oldest tagger (double-b) uses a BDT with secondary vertex features, while the newer DNNs (DeepAK8-MD, DeepDoubleX, ParticleNet-MD) operate on particle-level inputs. ParticleNet-MD is the most powerful and is the primary focus of the calibration work in Part III. Crucially, a more powerful tagger better separates gluon-splitting proxy jets from true H→bb̄/cc̄ signal, making calibration harder — this is the central challenge that the sfBDT method must address.
-->

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

<!-- 
The calibration challenge for H→bb̄/cc̄ taggers is fundamentally different from other CMS calibrations. For top and W taggers, abundant pure calibration samples exist in data (tt̄ events, W+jets events), but for Higgs boson decays this is impossible. The natural proxy choice — gluon-splitting g→bb̄/cc̄ jets from QCD multijet events — is abundant but impure: these jets contain extra ISR/FSR radiation from the initial and final state gluons that makes them structurally different from H→bb̄/cc̄. The previous approach of SV-based reweighting worked for the older double-b tagger but fails completely for ParticleNet-MD, which is powerful enough to distinguish gluon-splitting from Higgs even after reweighting. This motivates the sfBDT method as a fundamentally new approach.
-->

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

<!-- 
Chapter 6 introduces the sfBDT method — the central experimental contribution of this thesis. The name stands for "BDT for Scale Factor derivation." The core idea is to train a BDT that selects a subset of g→bb̄/cc̄ jets that are more signal-like, improving the quality of the proxy sample used for calibration. This chapter covers two generations of the sfBDT design, the concept of "sfBDT coastlines" for automated working point selection, the template maximum likelihood fit procedure for SF extraction, and the final published results for seven CMS taggers. The method has been formally approved as an official CMS calibration procedure and the results appear in CMS-PAS-BTV-22-001.
-->

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

<!-- 
The sfBDT method's key insight is to reformulate the proxy selection problem as a supervised learning task. Rather than trying to reweight the entire g→bb̄/cc̄ population to look like H→bb̄/cc̄, we train a BDT to identify and retain only the most signal-like subset. The BDT is trained to distinguish two extreme subsets: jets with very low gluon contamination (κg < 0.15, more similar to Higgs) versus jets with high gluon contamination (κg > 0.85). By applying a selection cut on the sfBDT score, we retain only the signal-like fraction of g→bb̄/cc̄ jets for use as calibration proxy. The two generations address different approximations: Gen 1 uses parton-level information to define contamination, while Gen 2 uses hadron-level N-subjettiness for better generator independence.
-->

---

# The sfBDT Method

Data and simulated samples

* **Data**: proton-proton collisions at 13 TeV, Run 2 (2016–2018), 138 fb$^{-1}$
* **Trigger**: logical OR of multiple $H_T$ triggers (125–900 GeV) — expands jet statistics in low $p_T$ region
* **MC samples**: QCD multijet (dominant), $V(\to qq)$+jets, $t\bar{t}$, single top
* **Key**: use same PYTHIA parton shower generator for both $H \to bb/cc$ signal and $g \to bb/cc$ proxy jets — DNN performance is sensitive to parton shower patterns
* **MC-to-data reweighting**: 3D grid on (event $H_T$, jet $p_T$, jet index) to compensate for trigger prescaling effects

<!-- 
The calibration uses the full CMS Run-2 dataset of 138 fb⁻¹ of proton-proton collisions at 13 TeV. QCD multijet events are selected using a logical OR of multiple HT triggers, covering thresholds from 125 to 900 GeV — this combination is essential for obtaining sufficient jet statistics across the full pT range from 200 GeV to well above 600 GeV. A critical systematic: different HT triggers are prescaled by different amounts, so the triggered dataset has a complex composition that requires a 3D reweighting on (HT, jet pT, jet index) to ensure the MC correctly models the data composition. Using the same PYTHIA parton shower for both signal simulation and the proxy jet MC is essential because DNN taggers are sensitive to subtle differences in shower patterns.
-->

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

<!-- 
This figure shows the number of data events passing each HT trigger threshold (125, 200, 300, 450, 600, and 900 GeV) as a function of jet pT, for two representative data-taking conditions (2016 post-VFP and 2018). The logical OR of all triggers (shown in black) provides a smooth and large event count across the full pT range. The trigger plateau regions — where a given trigger is 100% efficient — are visible as the flat portions of each curve. Using the logical OR rather than a single trigger is crucial for maximizing statistics in the low-pT region (pT ≈ 200-450 GeV) where boosted-jet flavour tagger calibration is most challenging due to lower jet boost.
-->

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

<!-- 
Figure 6.4 shows the MC-to-data reweighting procedure applied on the 3D grid of (HT, jet pT, jet index) variables. The upper panel shows the raw comparison of data and MC yields before reweighting — the MC does not match data due to the complex combination of differently-prescaled triggers. The lower panel shows the derived reweighting factors, which vary significantly across the 3D space. After applying these weights, the MC accurately models the data composition and kinematics. This reweighting is a critical step because any residual MC-data mismodeling in the kinematic variables would propagate into the sfBDT training and bias the derived scale factors.
-->

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

<!-- 
The jet selection and flavour categorization define the sample composition for the scale factor fit. Jets are selected with pT > 200 GeV, |η| < 2.4, and a soft-drop mass window of 50–200 GeV to match the signal region of H→bb̄/cc̄ analyses. The requirement that each soft-drop subjet has at least one matched secondary vertex strongly enriches the heavy-flavour content and is the key selection that makes g→bb̄/cc̄ jets dominate the proxy sample. The flavour categories (bb, b, cc, c, light) are defined by matching to hadrons in simulation, allowing the template fit to separately constrain each component. The flvB component (both subjets matched to b-hadrons) is the proxy for X→bb̄ calibration.
-->

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

<!-- 
Figure 6.6 shows a 2D histogram of the ParticleNet-MD X→cc̄ tagging discriminant versus the sfBDT score, separately for H→cc (signal, left) and g→cc (proxy before sfBDT selection, right). The key observation is that these two distributions are quite different — the g→cc jets have a broad, low sfBDT score distribution, while H→cc jets have high sfBDT scores. By applying a sfBDT selection cut (keeping only high sfBDT score jets), the g→cc distribution is made to more closely resemble the H→cc distribution in the tagging discriminant space. This validates the core hypothesis of the sfBDT method: the sfBDT score can indeed select proxy jets that are genuinely more similar to signal.
-->

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

<!-- 
Figure 6.7 shows the 1D distributions of the ParticleNet-MD X→cc̄ tagging discriminant for H→cc signal jets and g→cc proxy jets, comparing the effect of different sfBDT selection thresholds. Without any sfBDT selection, the proxy and signal discriminant distributions differ significantly — the proxy has too many low-score jets. As the sfBDT selection is progressively tightened, the proxy distribution converges toward the signal distribution. This convergence is the empirical validation that sfBDT selection successfully improves the proxy quality, and it motivates the quantitative framework of sfBDT coastlines introduced in the next section.
-->

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

<!-- 
Generation 2 of the sfBDT improves upon Gen 1 by replacing the parton-level gluon contamination fraction κg with a hadron-level N-subjettiness τ³¹h computed from first-generation hadrons. This change addresses two limitations of Gen 1: first, parton-level information is generator-dependent and may differ between the Higgs and QCD MC samples; second, κg only captures gluon radiation but misses the extra quark radiation that also makes g→cc jets differ from H→cc. The N-subjettiness τ³¹h — the ratio of 3-subjet to 1-subjet N-subjettiness computed on first-generation hadrons — is sensitive to both gluon and quark extra radiation, and being defined at the hadron level makes it more robust. Gen 2 sfBDT is the version used in the published CMS Run-2 results.
-->

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

<!-- 
The sfBDT coastlines concept provides an elegant solution to the problem of choosing the sfBDT selection threshold. Rather than selecting a single cut value (which would introduce an arbitrary choice), the coastline formalism maps the 2D tagger-sfBDT space into a set of contour lines where each coastline guarantees that the selected proxy jets have the same tagger discriminant shape as the signal jets (specifically, a uniform distribution after the tagger transformation). This is achieved by defining a tagger transformation T(x) that maps signal jets to a uniform distribution, then defining coastlines as level curves of the cumulative 2D probability density. The 9 coastlines define 9 different sfBDT selection tightnesses, yielding 81 independent SF measurements that are combined via an envelope method to assess systematic uncertainty.
-->

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

<!-- 
Figure 6.10 (left) shows the 2D tagger-sfBDT plane with the coastline contours overlaid, visualizing how the nine coastlines partition the proxy jet population from tightest (top-left) to loosest (bottom-right) selection. Figure 6.13 (right) shows the tagging discriminant distributions of proxy jets selected by each coastline, both normalized and unnormalized. The normalized distributions confirm the key property: regardless of which coastline is chosen, the proxy distribution matches the signal distribution. The unnormalized distributions show the trade-off — tighter coastlines have better proxy quality but fewer events, increasing statistical uncertainty on the SF.
-->

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

<!-- 
Figure 6.11 shows the sfBDT coastlines derived separately in three pT bins for the ParticleNet-MD X→bb̄ calibration. The coastlines are computed independently in each pT bin because the tagger-sfBDT correlation changes with jet pT — higher-pT jets have different substructure properties. The variation of coastline shapes across pT bins reflects the changing kinematics of g→bb̄ jets: at higher pT the jets are more boosted and the substructure is more collimated, making them somewhat more signal-like even without sfBDT selection. The coastlines are derived in simulation and then applied identically to data, with the sfBDT coastline variation among the nine options providing an important source of systematic uncertainty in the final SF measurement.
-->

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

<!-- 
The scale factors are extracted via a template maximum likelihood fit in the SV mass distribution — specifically, the mass of the secondary vertex with the largest transverse impact parameter significance. This variable provides strong discrimination between the three jet flavour components (flvB, flvC, flvL) because b-hadrons produce heavier SVs than c-hadrons, which in turn produce heavier SVs than light-quark or gluon jets. The fit is performed separately for the tagger "pass" and "fail" regions, allowing independent constraints on signal-like and background-like events. Each fit yields three scale factors — one per flavour component — and the flvB (or flvC) SF is the calibration result. Fits are run for 81 coastline combinations, and the envelope of all results defines the final SF with its total uncertainty.
-->

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

<!-- 
This slide shows two key validation plots for the sfBDT method. Figure 6.16 (left) shows the ROC curve comparing the separation between signal (H→cc) and proxy (g→cc) jets for different sfBDT coastline selections — tighter coastlines result in better proxy quality (lower separation between signal and proxy), confirming that the sfBDT selection successfully reduces the difference between proxy and signal. Figure 6.18 (right) shows the data vs. MC comparison of the transformed tagging discriminant before any sfBDT selection is applied, revealing significant data-MC discrepancy in the raw sample — precisely the problem that motivates the calibration. The combination of these plots motivates the complete sfBDT workflow.
-->

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

<!-- 
Figure 6.19 shows the data vs. MC comparison of the transformed ParticleNet-MD X→bb̄ tagging discriminant after applying the sfBDT coastline selection. Comparing with the before-selection plot in the previous slide, the data-MC agreement is dramatically improved — the distributions now show good consistency across the full discriminant range. This improvement is the direct demonstration that the sfBDT method successfully selects proxy jets that match the signal distribution. The residual difference that remains after sfBDT selection — quantified by the variation across the nine coastlines — is included as a dedicated systematic uncertainty in the final scale factor derivation.
-->

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

<!-- 
The final calibration results confirm the central hypothesis of the thesis: despite the large difference in the simulated discriminant distributions between ParticleNet-MD and the older double-b tagger, the derived scale factors are consistent with unity across all pT bins, working points, and data-taking eras. Scale factors of approximately 1.0 ± 0.1 confirm that the CMS simulation correctly models the behavior of ParticleNet-MD within about 10% uncertainty. This is a highly non-trivial result — it validates that the entire chain of CMS simulation (PYTHIA + GEANT4 + reconstruction) adequately captures the complex physics that ParticleNet-MD has learned to exploit. These SFs are now an official CMS result used in all analyses employing these taggers.
-->

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

<!-- 
Figure 6.21 shows the data vs. MC comparison on the SV mass fit variable — log(M_SV max(σ_dxy)/GeV) — for jets in the inclusive pass+fail region passing the middle sfBDT coastline selection. The three MC components (flvB in red, flvC in blue, flvL in green) sum to give the total prediction, which is compared to data (black points). The good agreement in this pre-fit comparison demonstrates that the sfBDT selection has produced a proxy sample well-described by simulation, validating the fit setup. The SV mass variable provides excellent flavour discrimination: flvB jets peak at high SV mass (~5 GeV for b-hadrons), while flvC and flvL peak at progressively lower masses.
-->

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
<!-- 
This summary slide closes Parts II and III with the key messages. In Part II, we traced the evolution of jet tagging algorithms through three generations, culminating in two specific algorithmic contributions: LorentzNet, which demonstrated that Lorentz equivariance provides measurable performance gains especially in the data-limited regime; and Particle Transformer (ParT), which combined a Transformer backbone with pairwise attentive features to achieve state-of-the-art performance on the JetClass benchmark. In Part III, we addressed the practical challenge of deploying ParticleNet-MD in CMS: the sfBDT method provides a principled solution to the calibration problem by training a BDT to select high-quality proxy jets, delivering scale factors close to unity for seven taggers. Together, these contributions form a coherent story from algorithm design to experimental validation.
-->
