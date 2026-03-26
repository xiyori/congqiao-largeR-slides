---
layout: section
---

# Part I: Foundations

## Chapter 1. Physics

---

# Standard Model

History

1. Discovery of electron by J.J. Thomson in the 19th century, marking the divisibility of the atom.
2. Discovery of the nucleus in 1911 and neutron in 1932.
3. Emergence of quantum mechanics in the 1920s to describe atomic and subatomic processes.
4. Evolution of quantum mechanics into quantum field theory (QFT) in the 1940s.
5. Establishment of quantum electrodynamics (QED) in the 1940s, describing electromagnetic interactions within a quantum framework and integrated with special relativity.
6. Introduction of Yang-Mills theory in the 1950s, incorporating QFT with non-Abelian gauge group.
7. Formulation of quantum chromodynamics (QCD) in the 1960s and 1970s, describing strong interaction.
8. Explanation of particle mass acquisition through spontaneous symmetry breaking in gauge theories with Higgs mechanisms in the 1960s.
9. Introduction of the Standard Model (SM), a comprehensive theory unifying all known elementary particles and forces except for gravity.

---
layout: two-cols
---

# Standard Model

Key components of SM

<div class="absolute-center">

* Higgs boson giving masses to other particles
* W and Z bosons as carriers of weak interaction
* Photon mediating electromagnetic force, remaining massless
* Gluon as massless boson mediating strong interaction
* Fermions as building blocks of matter, divided into quarks and leptons, constituting three generations

</div>

::right::

<div class="flex-column items-center justify-center h-full">
<img border="rounded" src="/part_I/sm.png" alt=""/>
</div>

---

# Standard Model

Lagrangian

Built to respect $\text{SU}(3) \times \text{SU}(2) \times \text{U}(1)$ gauge symmetry.

$$
\mathcal L = -\frac14 F_{\mu\nu}^a F_a^{\mu\nu} + \bar\psi (i\gamma^\mu D_\mu - m) \psi + (y_{ij}\bar\psi_i\phi\psi_j + h.c.) + |D_\mu\phi|^2 - V(\phi)
$$

- The first term corresponds to the kinetic term for gauge field, where $F_{\mu\nu}$ is the field strength tensor that covers the electroweak force and the strong force
- The second term is the coupling of fermions, such as leptons and quarks, to the gauge field
- The third term characterizes the Yukawa coupling, and it describes the interaction of the fermion fields with the Higgs field
- The fourth term is the Higgs interaction with the boson field
- The fifth term is the Higgs field potential

---
layout: two-cols
---

# Standard Model

Lagrangian expanded form

<div class="absolute-center">

We will use only relevant parts

</div>

::right::

<div class="flex-column items-center justify-center h-full">
<img border="rounded" width="330" src="/part_I/full_l.jpg" alt=""/>
</div>

---

<div class="flex-column">
<div>

# Feynman Diagram Vertices

</div>
<div class="center-container">
<img border="rounded" src="/part_I/diag.png" alt=""/>
</div>
</div>

---

# Standard Model

Higgs mechanism

Higgs field:

$$
\phi = \frac{1}{\sqrt2}\begin{pmatrix}
\phi^+\\
\phi^0
\end{pmatrix}, \quad \phi^{\bullet} \in \mathbb C
$$

Higgs potential:

$$
V(\phi) = \mu^2 \phi^\dagger \phi + \lambda (\phi^\dagger \phi)^2, \quad \mu^2 < 0, \lambda > 0
$$

Potential argmin (vaccum):

$$
\phi_{\text{vac}} = \frac{1}{\sqrt2}\begin{pmatrix}
0\\
v
\end{pmatrix}, \quad v = \sqrt{-\frac{\mu^2}{\lambda}}
$$

---

# Standard Model

Higgs mechanism

Rewrite Higgs field around $\phi_{\text{vac}}$

$$
\phi = \frac{1}{\sqrt2}\begin{pmatrix}
\phi_1^+ + i\phi_2^+\\
v + h + ia^0
\end{pmatrix}
$$

$\phi_1^+, \phi_2^+$, and $a^0$ are absorbed by the electroweak gauge fields, providing the necessary longitudinal
components for the $W^\pm$ and $Z$ bosons. This is the procedure through which they acquire masses.

$$
m_W^2 = \frac{g^2 v^2}{4}, \quad m_Z = \frac{(g^2 + g'^2) v^2}{4}
$$

$h$ is a physical Higgs boson (single scalar field degree of freedom) $m_H = v\sqrt{2\lambda}$.

---

# Standard Model

Higgs mechanism

After the electroweak symmetry
breaking, fermions gain mass through Yukawa interactions with the Higgs field:

$$
m_f = \frac{1}{\sqrt2}v y_f,
$$

where $y_f$ is the corresponding Yukawa coupling strength.

Part IV in this
dissertation focuses on the measurement of the Yukawa coupling between the Higgs boson
and the charm quark, $y_c$.

---

# LHC Higgs Boson Production

Proton-proton collisions

- **Gluon fusion (ggF)** (a). The most dominant Higgs production mode at the LHC involves the
fusion of two gluons mediated by a virtual quark loop;
- **Vector boson fusion (VBF)** (b). The VBF process produces a Higgs boson through the interaction of two vector bosons, which are emitted by quarks. The process
is characterized by the jets induced from the emitted quarks being widely separated in pseudorapidity $\eta$ and having a large invariant mass;
- **Higgs boson production associated with a vector boson $\left( V\!H \right)$** \(c\). The Higgs boson can be produced in association with a vector boson $W$ or $Z$, denoted by $V\!H$.
The emitted vector boson can provide a triggering of the Higgs boson to facilitate the experimental search. This production channel is the main research target in the physics measurement
discussed in Part IV;
- **Higgs boson production associated with a top quark-antiquark pair $\left( t\bar tH \right)$** (d). The $t\bar tH$ process involves the Higgs boson production in association with a top quark-antiquark pair. It is notable for its lower cross section owing to the substantial
mass of the resulting particles.

---

# Higgs Boson Decay

1. **Decays to Vector Bosons** (g):
	* Forbidden to decay into on-shell vector bosons due to mass constraints.
	* Decay to off-shell $WW^*$ and $ZZ^*$ pairs is considerable.
	* Important role in LHC due to a clean experimental signature in the four-lepton final state (Z boson pair).
3. **Decays to Fermions** (h):
	* Direct Yukawa coupling to fermions.
	* Proportional to fermion mass, significant for decays to first-generation fermions ($b\bar b$ and $\tau^+ \tau^-$ pairs).
	* Predominant but challenging to isolate in hadron collider environments.
4. **Loop-Induced Decay Processes** (i, j):
	* Decay into massless particles, including gluons and photons, through a loop-induced process.
	* Higgs boson to gg decay takes up considerable proportion but direct measurement is difficult.
	* Higgs boson decaying to diphoton (Higgs to $\gamma\gamma$) provides clear modelling of a peak structure on the diphoton invariant mass and is a golden channel to probe the Higgs boson at LHC.

---

<div class="flex-column">
<div>

# Feynman Diagram Vertices

Proton-proton collisions

</div>
<div class="center-container">
<img border="rounded" src="/part_I/higgs_prod.png" alt=""/>
</div>
</div>

<!--
### Production

- **Gluon fusion (ggF)** (a). The most dominant Higgs production mode at the LHC involves the
fusion of two gluons mediated by a virtual quark loop;
- **Vector boson fusion (VBF)** (b). The VBF process produces a Higgs boson through the interaction of two vector bosons, which are emitted by quarks. The process
is characterized by the jets induced from the emitted quarks being widely separated in pseudorapidity $\eta$ and having a large invariant mass;
- **Higgs boson production associated with a vector boson $\left( V\!H \right)$** \(c\). The Higgs boson can be produced in association with a vector boson $W$ or $Z$, denoted by $V\!H$.
The emitted vector boson can provide a triggering of the Higgs boson to facilitate the experimental search. This production channel is the main research target in the physics measurement
discussed in Part IV;
- **Higgs boson production associated with a top quark-antiquark pair $\left( t\bar tH \right)$** (d). The $t\bar tH$ process involves the Higgs boson production in association with a top quark-antiquark pair. It is notable for its lower cross section owing to the substantial
mass of the resulting particles.

### Decay

1. **Decays to Vector Bosons** (g):
	* Forbidden to decay into on-shell vector bosons due to mass constraints.
	* Decay to off-shell $WW^*$ and $ZZ^*$ pairs is considerable.
	* Important role in LHC due to a clean experimental signature in the four-lepton final state (Z boson pair).
3. **Decays to Fermions** (h):
	* Direct Yukawa coupling to fermions.
	* Proportional to fermion mass, significant for decays to first-generation fermions ($b\bar b$ and $\tau^+ \tau^-$ pairs).
	* Predominant but challenging to isolate in hadron collider environments.
4. **Loop-Induced Decay Processes** (i, j):
	* Decay into massless particles, including gluons and photons, through a loop-induced process.
	* Higgs boson to gg decay takes up considerable proportion but direct measurement is difficult.
	* Higgs boson decaying to diphoton (Higgs to $\gamma\gamma$) provides clear modelling of a peak structure on the diphoton invariant mass and is a golden channel to probe the Higgs boson at LHC.
-->

---

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_I/cross_sec.png" alt=""/>
</div>
<div>

The Higgs boson production cross sections in various production modes as a function of the centre-of-mass energy (left), and the branching functions as a function of the
Higgs boson mass (right).

</div>
</div>

<!--
Cross section ($\sigma$) is a measurement of the probability that an event occurs.

It's measured in “barn” – 1 b = $10^{-24} \text{cm}^2$

Branching fractions (or ratios) at the
Large Hadron Collider (LHC) define the probability of a specific particle decay channel
-->

---

<div class="flex-column">
<div>

# LHC Overview

LHC facilities

</div>
<div class="center-container">
<img border="rounded" src="/part_I/lhc.png" alt=""/>
</div>
</div>

<!--
1. The LHC is the world's largest, highest-energy particle accelerator located on the border of Switzerland and France, spanning 27 km.
2. It is designed to reach collision energies of 14 TeV, equivalent to protons traveling at 99.9999991% of light speed.
3. LHC's proton acceleration achieved through multiple stages, including Linac 2, Proton Synchrotron Booster (PSB), Proton Synchrotron (PS), Super Proton Synchrotron (SPS), and the final injection into LHC's vacuum tubes.
4. Increased probability of proton collisions by squeezing protons into small spaces, leading to proton bunch collisions every 25 nanoseconds or at a frequency of 40 MHz.
5. Proton collisions occur at four particle detectors: ATLAS, CMS, ALICE, and LHCb.
6. ALICE studies quark-gluon plasma at extreme energy densities. LHCb explores the differences between matter and antimatter through b-quark physics. ATLAS and CMS are general-purpose detectors with the same research scope and physical objectives.
-->

---

<div class="flex-column">
<div>

# LHC Overview

LHC Timeline

</div>
<div class="center-container">
<img border="rounded" src="/part_I/timeline.png" alt=""/>
</div>
</div>

<!--
1. LHC physics goals include SM studies, Higgs boson properties, and BSM signature searches such as dark matter, supersymmetry, and extra dimensions, testing particle physics theories.
2. The discovery of the Higgs boson in 2012 by ATLAS and CMS is a major success for LHC programs.
3. LHC has operated through various phases: Run 1 (2009-2013) at 7-8 TeV, Run 2 (2015-2018) at 13 TeV with an integrated luminosity of around 140 fb-1.
4. In progress is the Run 3 period (2022-2025), featuring increased luminosity and energy of 13.6 TeV, peak luminosity reaching 2 × 10^34 cm^-2s^-1.
5. High-Luminosity LHC (HL-LHC) is a planned upgrade starting in 2029 after Long Shutdown 3 (LS3), aiming to significantly increase luminosity by up to 10x and extend operational life to 2041. Figure 1.6 displays the timeline for LHC and HL-LHC programs.
-->

---

<div class="flex-column">
<div>

# CMS Overview

</div>
<div class="center-container">
<img border="rounded" src="/part_I/cms.png" alt=""/>
</div>
</div>

<!--
1. The CMS detector, located in Cessy, France, is one of two general-purpose LHC detectors focused on precision SM measurements and new physics searches.
2. The CMS detector's dimensions are 21 m long, 15 m in diameter, and weighs about 14000 tons.
3. It comprises several subdetectors: silicon pixel detector, silicon stripe detector, electromagnetic calorimeter, hadron calorimeter, and muon system.
5. Each subdetector consists of small hardware units covering the collision point region, except for the muon system and part of the hadron calorimeter.
6. Subdetectors are housed within a superconducting solenoid at 3.8 T, apart from the muon system and some of the hadron calorimeter.
7. When charged particles pass through the trackers, a strong magnetic field causes curved trajectories, enabling precise particle momentum measurements.
-->

---

<div class="flex-column">
<div>

# CMS Overview

Coordinate System

Pseudorapidity $\eta$ represents the angle of a particle relative to the beam axis:

$$
\eta \equiv -\ln\left[\tan\left(\frac{\theta}{2}\right)\right]
$$

</div>
<div class="center-container">
<img border="rounded" src="/part_I/cms_coords.png" alt=""/>
</div>
</div>

<!--
CMS coordinate system The CMS experiment uses a right-handed coordinate system. In
this system, the origin lies in the nominal interaction point. The $z$ axis runs counterclockwise along the beam direction and the $x$-$y$ plane is the transverse plane. The $x$ axis points
to the centre of the LHC ring, and the $y$ axis points upward. The $\phi$ and $r$ characterize the
azimuthal angle and the radial coordinate on the $x$-$y$ plane.
-->

---

<div class="flex-column">
<div>

# CMS Overview

Inner Tracker

</div>
<div class="center-container">
<img border="rounded" src="/part_I/inner_tracker.png" alt=""/>
</div>
</div>

<!--
1. The Inner Tracking System measures charged particle trajectories, divided into silicon pixel and strip detectors. It covers |η| < 2.4, with a material thickness of 0.4X0 to 1.0X0.
2. Silicon pixel detector: 1 m2 surface area with 66 million pixels; 0.0174 × 0.0174 size on (η, φ) space.
3. Silicon strip tracker: 200m2 with 9.6 × 106 strips; divided into inner barrel (TIB), inner disks (TID), outer barrel (TOB), and outer end-caps (TEC).
4. Pixel detector was upgraded during the LHC's year-end technical stop in 2016-2017, adding a new pixel layer in the barrel and endcap sections, increasing coverage to |η| = 3.
5. Electromagnetic Calorimeter (ECAL): Lead tungstate crystals measure electron and photon energies; relative energy resolution σ/E of 2.8%√E/GeV ⊕ 12%E/GeV ⊕ 0.3%.
6. ECAL has a preshower detector with superior granularity in front of endcaps for photon and neutral pion separation.
7. Hadron Calorimeter (HCAL): Brass absorber and plastic scintillator layers measure outgoing hadron energies; HCAL covers |η| < 1.3 (barrel) and 1.3 < |η| < 3.0 (endcaps), with coarse segmentation in the (η, φ) space.
8. ECAL and HCAL energy resolution for pions is σ/E = 110%E/GeV ⊕ 9%.
-->

---

<div class="flex-column">
<div>

# CMS Overview

Muon Chambers

</div>
<div class="center-container">
<img border="rounded" src="/part_I/muon_det.png" alt=""/>
</div>
</div>

<!--
9. Muon Chambers: CMS has the best muon identification system at LHC; dedicated muon system uses Drift Tube (DT) chambers, Cathode Strip Chambers (CSC), and Resistive Plate Chambers (RPC). DT used for precise trajectory measurements in the central barrel region, while CSC is used in endcaps.
10. Trigger and Data Acquisition: LHC collision rate of 40 MHz results in a data output of 15 PB per year; CMS trigger system reduces event rates to less than 100 kHz for final storage. The Level-1 trigger (L1T) uses custom hardware processors, and the high-level trigger (HLT) further reduces L1-accepted rate using large computing farms.
-->

---

<div class="flex-column">
<div>

# CMS Event Generation

- Monte Carlo (MC) simulations are crucial in CMS to compare collected data with Standard Model predictions.
- MC simulations numerically estimate observables by sampling pseudorandom numbers and approximating integrals.

</div>
<div class="center-container">
<img border="rounded" src="/part_I/generation_pie.png" alt=""/>
</div>
</div>

<!--
In the CMS experiment, Monte Carlo (MC) simulations are used to model phenomena expected in the detector, particularly when analytical solutions are not feasible due to complexity. MC simulations involve sampling pseudorandom numbers according to phase space and using the acceptance-rejection method to approximate integrals.
-->

---

# CMS Event Generation

- Event generators are used for exclusive collision event generation and handle both hard-scattering processes and parton showering.
- Parton showering is handled by dedicated phenomenological models, such as PYTHIA or HERWIG, which simulate non-perturbative QCD effects at low energy scales.
- The CMS software framework integrates various event generators using multithread computing utilities.
- The detector effect is delivered by an MC simulation toolkit, GEANT4, which simulates the interaction of hadronized particles with detector material.
- Pileup is simulated by generating inelastic events with PYTHIA, proceeding to GEANT4 for detector simulation, and then superimposing on the simulated hard-scattering event.

<!--
The CMS workflow for MC simulations includes event generators for exclusive collision event generation, which simulate both hard-scattering processes and parton showering. Commonly used event generators in CMS are MADGRAPH5_aMC@NLO and POWHEG. Parton showering is handled by dedicated phenomenological models such as PYTHIA or HERWIG, which simulate non-perturbative QCD effects at low energy scales and can compute simpler processes at LO accuracy. The CMS software (CMSSW) framework integrates various event generators using multithread computing utilities.

The detector effect is delivered by an MC simulation toolkit, GEANT4, which simulates the interaction of hadronized particles with detector material and integrates the effect of pileup. Pileup can be induced from the same bunch crossing (in-time pileup) or adjacent bunch crossings (out-of-time pileup) and is superimposed on the simulated hard-scattering event in the simulation.
-->

---
layout: two-cols
---

# CMS Event Reconstruction

<div class="absolute-center">

- Event reconstruction in CMS transforms raw detector data into meaningful physics objects like electrons, muons, photons, and jets for effective analysis of particle collisions.
- The Particle-flow (PF) algorithm lies at the core of CMS event reconstruction, combining information from all subdetectors to identify and reconstruct individual particles within each event, leading to PF candidates providing a global description of the event.

</div>

::right::

<div class="flex-column items-center justify-center h-full">
<img border="rounded" src="/part_I/reco.png" alt=""/>
</div>

<!--
1.5 CMS Event Reconstruction

Event reconstruction in the CMS experiment transforms raw detector data into meaningful physics objects like electrons, muons, photons, and jets for effective analysis of particle collisions. The Particle-Flow (PF) algorithm lies at the core of CMS event reconstruction, combining information from all subdetectors to identify and reconstruct individual particles within each event, resulting in PF candidates that provide a global description of the event.

1.5.1 Particle-flow candidate:

PF candidates are unified objects representing reconstructed particles, serving as fundamental building blocks for jet reconstruction and providing input features for deep learning-based jet processing. They are constructed using the PF algorithm, which integrates information from all subdetectors. Track reconstruction in the inner tracker (including electron and muon tracks) and calorimeter clusters in electromagnetic and hadronic calorimeters are essential components of this process.

An event display of a toy jet initiated by two charged particles 𝜋+ and 𝜋−, one
neutral hadron 𝐾0
𝐿, and two photons from the 𝜋0 decay, shown in the (𝑥 𝑦) coordinate[31]. The
symbols T1,2, E1,2,3,4 and H1,2 represent tracks and energy deposit in ECAL and HCAL measured
by the CMS subdetectors corresponding to these particles.
-->

---

# CMS Event Reconstruction

- Reconstruction processes for electrons, muons, secondary vertices (SVs), jets, and missing transverse momentum are carried out using the PF candidates as input features.
- GEN-jets produced from stable hadronized particles serve as truth-level references for jets in the development of jet tagging tools.
- Track reconstruction is crucial for understanding particle trajectories, their origins, and properties like momentum and direction, utilizing a Kalman Filtering (KF) based combinatorial track finder that operates in three main stages: initial seed generation, trajectory building, and final fitting.
- Calorimeter clusters reconstruction measures the energy and direction of stable neutral particles such as photons and neutral hadrons, distinguishing these neutral particles from charged particle energy deposits.
- PF elements are linked through a set of specific conditions, resulting in PF blocks including PF elements related directly or indirectly, forming the final PF candidates as a global event description.

<!--
1.5.2 Muons:

Muon candidates are selected based on global and tracker muons with additional criteria, such as isolated global muons and those inside a jet. Selection requirements include momentum determination using the inner track's pT for low-momentum muons or lowest χ2 probability among various track fits for high-momentum muons.

1.5.3 Electrons:

Electron candidates originate from a GSF track if its associated ECAL cluster is not connected to three or more tracks. The candidate includes ECAL clusters, linked tracks, and converted photon contributions. Electron identification involves isolation requirements and energy deposit evaluation. The final electron energy and direction are obtained by combining the corrected ECAL energy with the momentum of the GSF track and choosing the direction of the GSF track.

1.5.4 Secondary Vertices (SVs):

Secondary vertices can indicate commonality of displaced tracks, useful for identifying jets initiated from heavy-flavour hadrons. The Inclusive Vertex Finding (IVF) algorithm reconstructs SVs using all reconstructed tracks in an event with loose criteria as input. The algorithm identifies seed tracks, performs track clustering and fitting, conducts track arbitration, and refits and cleans the SVs.
-->

---

# Anti-kt Algorithm

1. The anti-$k_T$ jet clustering algorithm, a widely used sequential recombination jet finding approach, begins by assigning each input particle or object (constituents) as an initial "jet" with zero radius and zero transverse momentum (pT).
2. In each step of the iterative procedure, the algorithm computes the pair-wise distance between every pair of jets/particles, following a specific metric. The anti-$k_T$ algorithm employs the Cambridge/Aachen or "$k_T$" clustering metric with an additional parameter R, the distance parameter.
3. For each pair of particles $(i,j)$, the algorithm computes the anti-$k_T$ distance using the following formula:
$$
d_{ij} = \min(p_{T,i}^{-2}, p_{T,j}^{-2}) \frac{\Delta R_{ij}^2}{R^2}
$$
where $p_{T,i}, p_{T,j}$ are transverse momenta of particles $i$ and $j$, and $\Delta R$ is the distance between them in the rapidity-azimuthal angle space $\Delta R = \sqrt{\Delta y^2 + \Delta \phi^2}$.

<!--
In summary, the anti-$k_T$ algorithm merges particles with the smallest pairwise distance in each iteration until no remaining pairs fall below a specified distance threshold. This process results in well-defined and collimated jets that follow the initial parton direction closely.
-->

---

# Anti-kt Algorithm

4. In each iteration, the pair with the smallest distance $d_{ij}$ is merged using an exclusive "winner-takes-all" strategy where the four-momentum of the combined jet is updated as follows:
$$
\begin{aligned}
p_{T,\text{new jet}} &= p_{T,i} + p_{T,j}\\
\eta_{\text{new jet}} &= (p_{T,i} \cdot \eta_i + p_{T,j} \cdot \eta_j) / p_{T,\text{new jet}}\\
\psi_{\text{new jet}} &= (p_{T,i} \cdot \phi_i + p_{T,j} \cdot \phi_j) / p_{T,\text{new jet}}
\end{aligned}
$$
where $\eta$ and $\phi$ are the pseudorapidity and azimuthal angle, respectively. The combined jet then takes the place of the two initial jets/particles in subsequent iterations.

5. The algorithm continues to merge pairs of particles or jets until there are no remaining pairs below a certain distance threshold (e.g., $d_{ij} < R^2 \cdot p_{T,\min}^2$, where $p_{T,\min}$ is a user-defined parameter). At this point, the remaining objects/particles are declared as jets.
6. A smaller R value in anti-$k_T$ leads to more collimated jets, while a larger R results in broader jets that capture more of the event's radiation.

<!--
The anti-$k_T$ algorithm tends to form narrow and collimated jets that follow the original parton direction better than other jet finding algorithms like the Cambridge/Aachen (CA) or $k_T$ algorithm.
-->

---

# Jets

1. Jets are clustered from PF candidates using the anti-$k_T$ algorithm with a distance parameter R. Small-R jet collection (AK4 jets) results from R = 0.4, and large-R jet collections (AK8 or AK15 jets) use customizable parameters, such as R = 0.8 or 1.5 for specific analyses.
2. Pileup mitigation is achieved using the charged hadron subtraction algorithm for AK4 jets and the pileup per-particle identification (PUPPI) algorithm for AK8 or AK15 jets, which involve removing and correcting energy from pileup particles based on jet area and constituent probabilities.
3. The soft drop algorithm is applied to large-R jets to acquire the soft-drop mass by removing soft radiation patterns within the jet progressively using a reversed merging history of the clustering tree and splitting criteria (β = 0, zcut = 0.1, and R = 0.8 or 1.5 for AK8 and AK15 jets).
4. The soft-drop mass is designated as the invariant mass of two subjets resulting from the procedure that stops when splitting criteria are met.

<!--
The soft drop algorithm[37-39] is applied to each large-𝑅 jet to acquire the soft-drop mass
in a procedure to remove the soft radiation patterns within the jet progressively. This algorithm
first decluster a jet into its constituents and recluster them using the Cambridge/Aachen clus-
22
Chapter 1 Experimental Particle Physics
tering algorithm. This algorithm is similar to the anti-𝑘T one, except that the power index in
Eqs. (1.10, 1.11) on 𝑝T is changed from -2 to 0. This results in a clustering tree that represents
the merging history of the constituents. An iterative procedure runs on the reversed merging
history to split one constituent into two; for each splitting, the criteria
is examined, with 𝛽 = 0 and 𝑧cut = 0.1, and 𝑅 = 0.8 or 1.5 for AK8 and AK15 jets. If
the criteria are failed, it indicates that one branch is comparable soft and is discarded, and the
procedure continues with the remaining branch. The procedure stops until the requirement
is satisfied; the remaining two branches are considered two subjets of the given net, and the
soft-drop mass is designated as the invariant mass of two subjets
-->

---

# Jet Matching

- Two types of GEN-jets are clustered from PYTHIA particles with anti-$k_T$ algorithm and R=0.8 or 1.5: "no-ν" (excluding neutrinos) and "with-ν" (including neutrinos).
- The default configuration is "no-ν", serving as a reference for reconstruction accuracy.
- Soft drop algorithm is applied to both GEN-jet collections, matching the handling of reconstructed-level jets.
- A standard CMS convention is used for matching large-R jet collection to "no-ν" and "with-ν" GEN-jet collections, requiring ΔR < R0 between a jet and its matched GEN-jet.
- Some jets may not have a matched GEN-jet after the procedure.
- The soft-drop mass for each jet is determined as the mass of the matched GEN-jet from "no-ν" or "with-ν" collections.

<!--
The GEN-jets are clustered from all stable final particles generated by PYTHIA, with the
anti-𝑘T algorithm and 𝑅 = 0.8 or 1.5. Two cases are considered, one in which the neutrinos are
excluded from the particle list (denoted as “no-𝜈”), and another without the exclusion (denoted
as “with-𝜈”). The former is the default configuration, and the clustered GEN-jets provide a
reference for the reconstruction accuracy. For both cases, a soft drop algorithm with the same
settings as described above is adopted to mimic our handling of the reconstructed-level jets.
The “no-𝜈” and “with-𝜈” GEN-jet collections after soft-drop are matched to the large-
𝑅 jet collection using the standard CMS convention. To perform the matching, each jet is
matched with the GEN-jet with the smallest Δ𝑅 with the jet, also requiring Δ𝑅 < 𝑅0. This
matching process is carried out for each jet, following a sequence sorted by decreasing jet 𝑝T.
Some jets may have no matched GEN-jet after this procedure. The “no-𝜈” and “with-𝜈” GEN-
jet soft-drop mass for each jet is determined as the mass of the matched GEN-jet for the two
collections.
-->

---
layout: section
---

# Part I: Foundations

## Chapter 2. Deep Learning

---

# HEP Datasets

1. High-energy physics domain has mostly labeled public datasets
2. Datasets come from simulated events using MC event generators for hard-scattering processes
3. DELPHES used for fast simulation of detector effects and reconstruction of common analysis-level objects
4. DELPHES useful for phenomenological studies and deep learning
5. Stable particles propagated through detectors configured with the DELPHES card
6. Particles interacted with tracker, ECAL, and HCAL modules to build charged-particle tracks and calorimeter towers
7. Tracks and towers merged into E-flow object collection, considered reconstructed particles using all detector information
8. Jets clustered from E-flow objects with jet clustering algorithm
9. Jet samples constitute the jet tagging dataset.

<!--
Unlike the CV and NLP domains, where unlabelled datasets are most common and abun
dant, public datasets in the high-energy physics domain mostly come from simulated events
that are naturally labelled. These datasets are simulated with MC event generators for hard-
scattering process and DELPHES[63] for fast simulation of detector effects and reconstruction of
common analysis-level objects. DELPHES is incredibly useful for delivering phenomenological
studies in LHC physics and deep learning. In DELPHES, stable particles produced by event gen-
erators are propagated through the detectors configured with the DELPHES card and interacted
with the tracker, ECAL and HCAL modules sequentially to build charged-particle tracks and
calorimeter towers with simplified algorithms, based on predefined detector geometry, granu-
larity and resolution, etc. The processed tracks and towers are merged into the E-flow object
collection, which is considered the reconstructed particles using all the detector information, in
analogy with the PF candidates in the CMS experiment. Jets are clustered from E-flow objects
with the jet clustering algorithm, and they constitute the samples in the jet tagging dataset.
-->

---

# Jet Tagging Datasets

Top tagging dataset

* Includes 1.2M jets for training, 0.4M for validation, and 0.4M for testing
* Two sets of large-R jets initiated from top quark and QCD multijet events
* Generated by PYTHIA8 and passed to DELPHES for detector simulation
* Jets clustered with anti-kT algorithm (R = 0.8)
* Includes kinematics information of jet constituents with up to 200 highest pT constituents

---

# Jet Tagging Datasets

Quark-gluon tagging dataset

* Includes 1.6M jets for training, 0.2M for validation, and 0.2M for testing
* Two sets of small-R jets initiated from Z(→νν) + u/d/s and Z(→νν) + g events
* Generated by PYTHIA v8 and clustered with anti-kT algorithm (R = 0.4)
* Includes kinematics information of jet constituents and particle identification (PID) information
* PID varies from 8 types, including electrons, muons, photons, charged hadrons, and neutral hadrons

---

# Jet Tagging Datasets

JetClass dataset

* Large dataset comprising 100M for training, 20M for validation, and 20M for testing
* Composed of ten classes of large-R jets, including Higgs boson decay modes, top quark decays, W/Z bosons, and QCD events
* Generated by MG for resonance production and decay, then PYTHIA v8 for parton showering and DELPHES for detector simulation
* Jets clustered with R = 0.8 and input features include kinematics information, particle identification flags, and trajectory displacement features
4. Recommended metrics for JetClass dataset: binary background rejection evaluating the ability to separate two certain classes (S vs B) using a discriminant score(A) / (score(A) + score(B)).

---

<div class="flex-column">
<div>

# Jet Tagging Datasets

Detailed Comparison

</div>
<div class="center-container">
<img border="rounded" src="/part_I/datasets.png" alt=""/>
</div>
</div>
