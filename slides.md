---
theme: seriph

title: "Modern deep learning for large-R jet tagging"
info: |
  ## Modern deep learning for large-R jet tagging &mdash; algorithms, calibration methods, and applications in the CMS experiment
  Best Dissertations Course

# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable Comark Syntax: https://comark.dev/syntax/markdown
comark: true
# duration of the presentation
duration: 1 hour 20 min

layout: intro
---

<div class="text-center">

### Modern deep learning for large-$R$ jet tagging --- algorithms, calibration methods, and applications in the CMS experiment

- Author: Congqiao Li
- Supervisor: Prof. Qiang Li
- Award: CMS Ph.D. Thesis Award 2024

HSE CS PhD School $\bullet$ Best Dissertations Course

19.03.2026

</div>

<!-- 
This presentation covers the PhD thesis of Congqiao Li from Peking University, which was awarded the CMS Ph.D. Thesis Award 2024. The thesis addresses a central challenge in LHC physics: reliably identifying the origins of large-radius jets produced in boosted decays of heavy resonances like the Higgs boson, W/Z bosons, and top quarks. The work spans three interconnected topics — developing novel deep learning algorithms (LorentzNet and Particle Transformer), designing the sfBDT calibration method to derive data-to-simulation scale factors for advanced jet taggers, and applying these tools in landmark physics measurements including the first observation of Z→cc at a hadron collider. Together these contributions represent a comprehensive advancement of modern jet physics at the LHC.
-->

---

<div class="flex-column">
<div>

# CMS Ph.D. Thesis Award

- Recognizes and rewards excellence in Ph.D. thesis research yearly since year 2000
- Targets students who submitted their Ph.Ds the previous year between August 1 and July 31
- The theses are judged on their content, originality, clarity of writing, and impact within CMS and the high energy physics in general and can be written on any CMS-related work

<br>

</div>
<div class="center-container">
<img border="rounded" src="/intro/winners.png" alt=""/>
</div>
</div>

<!-- 
The CMS Ph.D. Thesis Award has been recognizing outstanding doctoral research within the CMS collaboration since the year 2000. Theses are judged annually on their content, originality, clarity of writing, and impact within CMS and high energy physics broadly. The 2024 award to Congqiao Li recognized the combined impact of his work on novel deep learning architectures for jet tagging, the innovative sfBDT calibration method that is now deployed in official CMS publications, and the application of these tools in precision Higgs boson measurements — a rare combination of algorithmic, experimental, and physics contributions in a single thesis.
-->

---

# Authors

<div class="grid-container">
  <div class="grid-item">

**Li, Congqiao**

PhD from Peking University, China

  </div>
  <div class="grid-item">

<img border="rounded" width="200" src="/intro/author.png" alt=""/>

</div>
  <div class="grid-item">

**Li, Qiang**

Professor, State Key Laboratory of Nuclear Physics and Technology,
Peking University, China

</div>
  <div class="grid-item">

<img border="rounded" width="200" src="/intro/superv.png" alt=""/>

</div>
</div>

<style>
.grid-container {
  display: grid;
  /* Defines two columns, each taking up an equal fraction of the available space */
  grid-template-columns: 1fr 1fr;
  /* Defines two rows, each taking up an equal fraction of the available space */
  grid-template-rows: 1fr 1fr;
  /* Optional: Adds space between the grid items */
  gap: 20px;
  /* Optional: Set a specific height for the container, or it will just be as tall as its content */
}

/*.grid-item {

}*/
</style>

<!-- 
Congqiao Li completed his PhD at Peking University under the supervision of Professor Qiang Li, who leads an active CMS group at the State Key Laboratory of Nuclear Physics and Technology. The thesis work was performed within the CMS collaboration at CERN, drawing on both the experimental infrastructure of CMS and the theoretical tools of particle physics phenomenology. Professor Qiang Li's group has made long-standing contributions to CMS jet physics and boosted object identification, and this thesis represents a culmination of that research program.
-->

---

# Publications

Experimental publications with significant contributions

- CMS Collaboration, “Search for Higgs boson decay to a charm quark-antiquark pair in proton-proton collisions at $\sqrt s$ = 13 TeV”, Phys. Rev. Lett. 131, 061801 (2023), arXiv: 2205.05550 [hep-ex].
- MS Collaboration, “Performance of heavy-flavour jet identification in boosted topologies in proton-proton collisions at $\sqrt s$ = 13 TeV”, CMS Physics Analysis Summary CMS-PAS-BTV-22-001, 2022.

<!-- 
The experimental publications reflect the two main experimental pillars of the thesis. The first is the CMS search for H→cc in the VH production channel — one of the most challenging Higgs decay modes due to the small branching fraction and large QCD background — representing the first CMS result directly targeting the Higgs-charm Yukawa coupling. The second is a CMS Physics Analysis Summary documenting the performance and calibration of heavy-flavour jet taggers in boosted topologies across the full Run-2 dataset, the primary experimental deliverable that validated the sfBDT method and enabled its use across many CMS analyses.
-->

---

# Publications

Phenomenological research

- C. Li, et al., “Accelerating resonance searches via signature-oriented pre-training”, arXiv:
2405.12972 [hep-ph].
- C. Li, et al., “Does Lorentz-symmetric design boost network performance in jet physics?”,
Phys. Rev. D 109, 056003 (2024), arXiv: 2208.07814 [hep-ph].
- H. Qu, C. Li, and S. Qian, “Particle Transformer for Jet Tagging”, in International Con-
ference on Machine Learning, pp. 18281-18292. PMLR, 2022, arXiv: 2202.03772
[hep-ph].
- S. Gong, et al., “An efficient Lorentz equivariant graph neural network for jet tagging”, JHEP 07, 030 (2022), arXiv: 2201.08187 [hep-ph].
- C. Li, et al., “Loop-induced $ZZ$ production at the LHC: An improved description by
matrix-element matching”, Phys. Rev. D 102, 116003 (2020), arXiv: 2006.12860 [hep-ph].

<!-- 
The phenomenological publications span several years and research directions. The two most central to this thesis are the Particle Transformer paper — which introduced a Transformer backbone with pairwise attentive bias and set a new state-of-the-art on the JetClass benchmark — and the systematic study of Lorentz-symmetric design, which quantified exactly how and when symmetry preservation improves performance. The pre-training paper on GloParT explores the emerging paradigm of foundation models for jet physics, which is Part V of the thesis. The LorentzNet paper and the loop-induced ZZ production study reflect the breadth of the research program.
-->

---
src: ./pages/part_I.md
---

Contents here are ignored

---
src: ./pages/part_II-III.md
---

Contents here are ignored

---
src: ./pages/part_IV-V.md
---

Contents here are ignored

---
layout: end
---

<div class="text-center">

# Thank you!

<PoweredBySlidev mt-10 />

</div>

<!-- 
Thank you for your attention. To summarize the key contributions of this thesis: algorithmically, LorentzNet demonstrated the value of Lorentz-equivariant GNNs and Particle Transformer set a new state-of-the-art by combining a Transformer backbone with pairwise attentive bias; experimentally, the sfBDT calibration method delivered robust scale factors for seven CMS boosted-jet taggers now used across the collaboration; and in physics, the VHcc analysis achieved the first observation of Z→cc and the best direct measurement of the Higgs-charm Yukawa coupling. I am happy to take questions on any aspect of the work.
-->
