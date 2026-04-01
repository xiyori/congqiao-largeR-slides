---
layout: section
---

# Part IV: Search for $VH \to c\bar c$

## Chapter 7: Search for $H \to c\bar c$ at the LHC

<!-- 
Part IV presents the flagship physics application of the thesis: the search for the Higgs boson decaying to charm quark-antiquark pairs in associated production with a vector boson (VH→cc̄). Chapter 7 motivates the measurement: the charm Yukawa coupling is a key SM prediction that has never been directly measured, and this analysis exploits the full toolkit developed in Parts II and III — ParticleNet tagging, mass regression, and sfBDT calibration — to push toward the first direct sensitivity. The search uses the full CMS Run-2 dataset at √s = 13 TeV corresponding to 138 fb⁻¹.
-->

---

# Motivation for $H \to c\bar c$

<div class="absolute-center">

* SM predicts $H \to c\bar c$ branching ratio $\approx 2.9\%$ — second-generation quark Yukawa coupling
* Direct measurement of $y_c$ tests the SM mass-proportionality of Yukawa couplings
* **Challenge**: tiny signal cross section, overwhelming QCD multijet background
* **Strategy**: exploit $VH$ associated production ($V = W, Z$) with leptonic $V$ decays
  - Leptonic decay of $V$ provides triggering capability and QCD suppression
  - Boosted topology: Higgs reconstructed as a single large-$R$ jet

</div>

<!-- 
The Higgs-charm Yukawa coupling is one of the most elusive SM parameters accessible at the LHC. With a branching ratio of only ~2.9%, H→cc̄ is overwhelmed by QCD backgrounds and difficult to separate from the dominant H→bb̄ channel. The VH production mode provides the best handle: the leptonic decay of the associated W or Z boson provides a clean trigger and drastically reduces QCD multijet backgrounds. In the boosted topology where the Higgs has high pT, its decay products merge into a single large-R jet, enabling the use of the ParticleNet tagger and mass regression developed in earlier parts of the thesis.
-->

---

<div class="flex-column">
<div>

# Analysis Strategy

Three lepton channels targeting leptonic $V$ decays

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_7.1.png" alt=""/>
</div>
</div>

<!-- 
The analysis defines three channels based on the number of leptons from the vector boson decay: the 0-lepton channel targeting Z→νν̄ (with large missing transverse momentum), the 1-lepton channel targeting W→ℓν, and the 2-lepton channel targeting Z→ℓℓ. Each channel has different background compositions and sensitivities. The figure illustrates the VH event topology in each channel, showing how the Higgs boson recoils against the vector boson in the boosted regime.
-->

---

<div class="flex-column">
<div>

# Previous Results

Comparison with other $H \to c\bar c$ searches at the LHC

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_7.2.png" alt=""/>
</div>
</div>

<!-- 
This figure shows the landscape of H→cc̄ searches at the LHC before this analysis, including results from both ATLAS and CMS using different production modes (VH, VBF, ggF). The previous CMS result using the resolved-jet approach set an observed (expected) upper limit on the VH→cc̄ signal strength of 37 (48) at 95% CL. The merged-jet analysis presented in this thesis provides complementary sensitivity and, when combined with the resolved approach, significantly improves the overall constraint on the Higgs-charm Yukawa coupling.
-->

---
layout: section
---

# Part IV: Search for $VH \to c\bar c$

## Chapter 8: Analysis Method

<!-- 
Chapter 8 describes the full analysis method for the VH→cc̄ search. It covers the development of the ParticleNet tagger and mass regression model used to identify and reconstruct Higgs→cc̄ jets, the reconstruction of physics objects, the event selection in the three lepton channels, the background estimation strategy using control regions, and the systematic uncertainties. The analysis introduces several novel techniques including kinematic BDTs decorrelated from mass and cc-tagging discriminant for signal-background separation.
-->

---

# Jet Tagging and Mass Regression

ParticleNet-MD for $X \to c\bar c$ identification

* **ParticleNet-MD** trained for mass-decorrelated $X \to b\bar b$ and $X \to c\bar c$ tagging
* Uses **AK15 jets** (anti-$k_T$ $R = 1.5$) to capture wider $H$ decay products at moderate boost
* Input: PF candidates and SVs → trained on CMS simulation with flat $m_\text{SD}$ and $p_T$ spectra
* Three $X \to c\bar c$ working points: **HP** (high purity), **MP** (medium purity), **LP** (low purity)
* Calibrated via sfBDT method (Part III) — SFs $\approx 1$ with 4–8% (15–30%) uncertainty for $b\bar b$ ($c\bar c$)

<!-- 
The ParticleNet mass-decorrelated tagger used in this analysis is trained as described in Section 8.2.1, operating on AK15 jets. The larger cone size of R=1.5 compared to the standard R=0.8 helps capture the full H→cc̄ decay products at the moderate pT range of 200–300 GeV relevant for VH production. The mass-decorrelation ensures the tagger does not sculpt the background mass distribution, enabling signal extraction via a template fit in the Higgs candidate mass. Three working points provide increasing signal purity at the cost of statistical power.
-->

---
layout: two-cols
---

# ParticleNet-MD Tagger

Training on the multi-class and mass-decorrelated dataset

* 6 classes: $X \to b\bar b$, $X \to c\bar c$, $X \to qq$, QCD $bb$, QCD $cc$, QCD others
* Flat reweighting on $(p_T, m_\text{SD})$ 2D histogram for mass decorrelation
* Trained with WEAVER framework on NVIDIA GTX 3090

::right::

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_8.1.png" alt=""/>
</div>
</div>

<!-- 
The ParticleNet-MD tagger is trained simultaneously on six jet classes, combining signal resonant jets and QCD background jets split by heavy-flavour content. The training imposes mass decorrelation by reweighting the (pT, mSD) distribution to be flat, ensuring that the output discriminant does not depend on the jet mass. This is critical for the analysis because signal extraction relies on fitting the Higgs candidate mass distribution — any sculpting by the tagger would introduce a false signal-like bump.
-->

---

<div class="flex-column">
<div>

# Mass Regression

ParticleNet regression model for improved $H_\text{cand}$ mass resolution

* Regression model predicts GEN-level resonance mass from particle-level inputs
* **Key improvement**: better mass resolution than soft-drop mass ($\sigma/\mu$: 15.7% vs 17.3% for $H \to c\bar c$)
* Mass regression reduces the impact of out-of-cone radiation and neutrino losses

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_8.5.png" alt=""/>
</div>
</div>

<!-- 
The mass regression model, also based on the ParticleNet architecture, predicts the generator-level resonance mass from reconstructed particle-level inputs. Compared to the standard soft-drop mass, the regressed mass achieves better resolution (σ/μ = 15.7% vs 17.3% for H→cc̄ jets), providing sharper signal peaks and improved signal-background separation in the template fit. The mass regression is validated in data using a semi-leptonic tt̄ control sample, where the W→cs component of the top jet serves as a proxy for the H→cc̄ signal.
-->

---

<div class="flex-column">
<div>

# Mass Regression Validation

Data validation using the $W \to c\bar s$ component in a boosted $t\bar t$ control sample

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_8.7.png" alt=""/>
</div>
</div>

<!-- 
The mass regression performance is validated in data using a boosted semi-leptonic tt̄ control sample selected with a single muon trigger. The W→cs component of the top quark jet serves as a proxy for the H→cc̄ jet. The jet mass scale (JMS) and resolution (JMR) are extracted by fitting the W peak in the regressed mass distribution. Results show JMS compatible with 1 across all data-taking years, while an additional ~5% mass smearing is needed to match data resolution.
-->

---

# Event Selection

Three lepton channels

| Selection | 2-lepton ($Z \to \ell\ell$) | 1-lepton ($W \to \ell\nu$) | 0-lepton ($Z \to \nu\bar\nu$) |
|---|---|---|---|
| Leptons | 2 opposite-charge same-flavour | 1 tight lepton | 0 loose leptons |
| $p_T(V)$ | $> 150$ GeV | $> 150$ GeV | $p_T^\text{miss} > 200$ GeV |
| $\Delta\phi(V, H_\text{cand})$ | $> 2.5$ | $> 2.0$ | $> 1.5$ |
| Max small-$R$ jets | $< 3$ | $< 2$ | $< 2$ |
| $p_T(H_\text{cand})$ | $> 200$ GeV | $> 200$ GeV | $> 200$ GeV |

* Kinematic BDT separates VH signal from main backgrounds (decorrelated from mass and $cc$-tag)
* Events categorized into SR (BDT > 0.55) and CR (BDT < 0.55)
* Three $X \to c\bar c$ tagging categories: HP, MP, LP

<!-- 
The event selection is optimized separately for each lepton channel. All channels require at least one large-R jet with pT > 200 GeV as the Higgs candidate, and impose back-to-back topology requirements via Δφ(V, Hcand). The small-R jet multiplicity requirements suppress tt̄ backgrounds, which are more important in the 1L and 0L channels. A kinematic BDT, trained using only kinematic variables independent of the cc-tagging discriminant and Higgs mass, further separates VH signal from the dominant backgrounds while maintaining mass decorrelation for the template fit.
-->

---

<div class="flex-column">
<div>

# Kinematic BDT

Distributions showing separation between $VH$ signal and backgrounds (2L channel)

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_8.8.png" alt=""/>
</div>
</div>

<!-- 
The kinematic BDT output distributions after baseline selection in the 2L channel show good separation between the VH signal (normalized to the total background) and the dominant Z+jets background. The BDT is trained with XGBOOST using 10-fold cross-validation and inputs that include only kinematic variables (pT, η, Δφ, angular distances) but not the mass or cc-tagging discriminant. This design ensures the BDT is largely decorrelated with both the Hcand mass and the X→cc̄ discriminant, preserving the analysis strategy of performing signal extraction via a template fit in mass after BDT and cc-tag selections.
-->

---

<div class="flex-column">
<div>

# $H_\text{cand}$ Mass Distribution

Signal and background mass shapes after kinematic BDT and $X \to c\bar c$ tagging selections (2L)

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_8.12.png" alt=""/>
</div>
</div>

<!-- 
The Hcand mass distribution after high BDT and X→cc̄ tagging selections shows the characteristic signal peak structure of VH→cc̄ at the Higgs mass on top of a flat background. The signal is normalized to the total background for shape comparison. In the high-purity category (left), the signal-to-background ratio is highest, while the low-purity category (right) retains more events. The flat background mass spectrum confirms that both the kinematic BDT and the cc-tagging discriminant are decorrelated with the Higgs candidate mass, validating the analysis design.
-->

---

# Background Estimation Strategy

Control regions constrain major backgrounds

* **Signal Region (SR)**: high kinematic BDT + $X \to c\bar c$ tag → mass template fit
* **Low-BDT CR**: low kinematic BDT score → constrains $V$+jets and $t\bar t$ normalizations
* **High-$N_j$ CR**: additional small-$R$ jets → constrains $t\bar t$ components
  - $t\bar t$ split into **Top-merged**, **$W$-merged**, and **Other** components
  - Similar shapes between high/low $N_j$ for Top- and $W$-matched; normalization SFs transferred
* Background normalization SFs shared across lepton channels where validated:
  - $Z$+jets: 0L + 2L; $W$+jets: 0L + 1L; $t\bar t$: 0L + 1L

<!-- 
The background estimation strategy uses control regions to constrain the normalizations of major background processes. The low-BDT control region provides a sideband enriched in the main backgrounds (V+jets, tt̄) while remaining orthogonal to the signal region. The high-Nj control region is specific to the 0L and 1L channels where tt̄ is significant, exploiting the fact that tt̄ events tend to have additional small-R jets. The tt̄ background is split into three components based on the matching of quarks to the large-R jet, which is necessary because the composition changes with jet multiplicity requirements.
-->

---

<div class="flex-column">
<div>

# $t\bar t$ Background Decomposition

Shape comparison between low- and high-$N_j$ regions for three $t\bar t$ components (0L)

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_8.20.png" alt=""/>
</div>
</div>

<!-- 
This figure validates the tt̄ background estimation strategy by comparing the Hcand mass shapes between the low-Nj (signal-like) and high-Nj (control) regions for the three tt̄ components. The top-matched and W-matched components show very similar shapes between the two regions, confirming that normalization scale factors from the high-Nj CR can be safely transferred to the SR. The "Other" component shows larger differences, so separate normalization scale factors are used for the high-Nj CR in this case.
-->

---

# Systematic Uncertainties

Key sources of uncertainty

**Theoretical:**
* PDF and scale ($\mu_R$, $\mu_F$) variations for signal and backgrounds
* $VH$ production cross section and $p_T$ spectrum corrections (NLO EWK + NNLO QCD)
* Single top (15%) and diboson (5%) cross section uncertainties

**Experimental:**
* Jet energy scale/resolution (correlated between small-$R$ and large-$R$ jets)
* $X \to c\bar c$ tagging efficiency and mistag rate (from sfBDT calibration)
* Lepton efficiency, MET trigger, pileup reweighting
* JMS and JMR from $t\bar t$ validation (Section 8.2.2)

<!-- 
The systematic uncertainties are categorized into theoretical and experimental sources. The dominant experimental uncertainties are the cc-tagging efficiency and mistag rate uncertainties, derived from the sfBDT calibration method presented in Part III. The JMS and JMR uncertainties from the mass regression validation are also important since they directly affect the signal mass shape. On the theoretical side, the V+jets and tt̄ normalizations are left floating in the fit, constrained by the control regions, so their cross section uncertainties do not directly enter.
-->

---
layout: section
---

# Part IV: Search for $VH \to c\bar c$

## Chapter 9: Analysis Results

<!-- 
Chapter 9 presents the analysis results in three stages: first, validation of the full procedure via the VZ→cc̄ measurement; second, the VH→cc̄ signal extraction; and third, the combination with the resolved-jet analysis for the final result. The VZ→cc̄ validation is a landmark result in itself — representing a first observation of Z→cc̄ in a hadron collider — and confirms that the full analysis chain works correctly before applying it to the much rarer Higgs signal.
-->

---

# $VZ \to c\bar c$ Validation

First observation of $Z \to c\bar c$ at a hadron collider

* Full analysis procedure validated by measuring $VZ$ production with $Z \to c\bar c$
* Same event selection and signal extraction, but treating $VZ \to c\bar c$ as signal
* Results:

| Metric | Full Run 2 Combined |
|---|---|
| Expected significance | 5.7$\sigma$ |
| Observed significance | 4.9$\sigma$ |
| Best-fit $\mu_{VZ \to c\bar c}$ | $0.87^{+0.25}_{-0.21}$ |

* Consistent with SM expectation — **validates the full analysis chain**
* Combined with resolved-jet analysis: observed significance **5.7$\sigma$** → first observation

<!-- 
The VZ→cc̄ validation is a critical milestone. By using the identical analysis procedure but treating VZ→cc̄ as the signal process, the observed significance of 4.9σ (expected 5.7σ) with μ = 0.87 demonstrates that the full chain of ParticleNet tagging, mass regression, kinematic BDT, and template fitting works correctly. The consistency with the SM prediction (μ ≈ 1) gives confidence in the analysis methodology. When combined with the resolved-jet approach, the significance reaches 5.7σ — constituting the first observation of Z→cc̄ at a hadron collider, a remarkable result in its own right.
-->

---

# $VH \to c\bar c$ Results

Signal extraction from full Run 2 data

* Binned maximum likelihood fit on $H_\text{cand}$ mass in all SRs and CRs simultaneously
* No significant excess observed beyond SM backgrounds
* Best-fit signal strength: $\mu_{VH \to c\bar c} = 7.2^{+4.4}_{-4.2}$
* Observed (expected) upper limit at 95% CL: $\mu_{VH \to c\bar c} < 15$ (8.5)

<!-- 
The VH→cc̄ signal extraction uses a simultaneous binned maximum likelihood fit across all signal and control regions for all three data-taking years. No significant excess is observed. The best-fit signal strength of 7.2 is compatible with both the SM expectation (μ=1) and zero within uncertainties. The observed upper limit of 15 at 95% CL constrains the VH→cc̄ production rate to less than 15 times the SM prediction.
-->

---

<div class="flex-column">
<div>

# $VH \to c\bar c$ Results

Post-fit nuisance parameters and their impacts on the signal strength

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_9.9.png" alt=""/>
</div>
</div>

<!-- 
This impact plot shows the 30 nuisance parameters with the largest impact on the VH→cc̄ signal strength. The dominant sources are statistical uncertainties (Poisson-constrained bin-by-bin parameters), followed by the cc-tagging efficiencies and mistag rates, the V+jets normalization scale factors, and the tt̄ normalization factors. The pull values (θ - θ₀)/Δθ are generally within ±1, indicating no significant tension with the pre-fit constraints. The overall uncertainty on the signal strength is dominated by statistical limitations rather than systematics.
-->

---

# Combined $VH \to c\bar c$ Results

Combination with resolved-jet analysis

* Merged-jet and resolved-jet analyses made orthogonal via $p_T$ threshold of 300 GeV on large-$R$ jet
* **Combined results**:

| Result | Value |
|---|---|
| Best-fit $\mu_{VH \to c\bar c}$ | $7.7^{+3.8}_{-3.5}$ |
| Observed (expected) 95% CL upper limit | 14 (7.6) |
| $\kappa_c$ constraint (observed 95% CL) | $1.1 < \|\kappa_c\| < 5.5$ |
| $\kappa_c$ constraint (expected) | $\|\kappa_c\| < 3.4$ |

* **Strongest direct constraint** on the Higgs-charm Yukawa coupling at the time
* $VZ \to c\bar c$ combined: $\mu = 1.01^{+0.23}_{-0.21}$, significance = **5.7$\sigma$** → first observation of $Z \to c\bar c$

<!-- 
The combination of the merged-jet and resolved-jet analyses provides the strongest constraint on the Higgs-charm Yukawa coupling. The observed 95% CL interval of 1.1 < |κc| < 5.5 represents a significant step toward probing second-generation quark Yukawa couplings. The expected constraint of |κc| < 3.4 demonstrates that the analysis is approaching the sensitivity needed to test the SM prediction of κc = 1. The combined VZ→cc̄ observation at 5.7σ provides a remarkable demonstration of the experimental reach achievable with the techniques developed in this thesis.
-->

---

<div class="flex-column">
<div>

# Outlook: HL-LHC Projection

Projected sensitivity with 3000 fb$^{-1}$

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_9.10.png" alt=""/>
</div>
</div>

<!-- 
This figure shows the profile likelihood scan on the signal strengths μ_VH→bb̄ and μ_VH→cc̄ projected to the HL-LHC with 3000 fb⁻¹ of data. The projection is based on the merged-jet analysis workflow with proper estimation of the statistical uncertainties. The contour shows that at the HL-LHC, the VH→cc̄ signal strength can be constrained to approximately ±0.2 around the SM value, enabling a meaningful measurement of the Higgs-charm Yukawa coupling and a test of the mass-proportionality of fermion Yukawa couplings at the second-generation level.
-->

---
layout: section
---

# Part V: Application Paradigm for Pre-training and Fine-tuning

## Chapter 10: Perspectives on Future Jet Models

<!-- 
Part V extends beyond specific CMS applications to explore how the "pre-training and fine-tuning" paradigm — the driving force behind the AI revolution in NLP and computer vision — can be applied to jet physics at the LHC. Chapter 10 provides the theoretical foundation and design philosophy for future jet models, discussing three key aspects: expressiveness (Transformer architectures), large capacity (scaling model parameters), and comprehensiveness (pre-training on diverse jet categories for transfer learning). This sets the stage for the GloParT model (Chapter 11), its fine-tuning applications (Chapter 12), and the Sophon model with JETCLASS-II dataset (Chapter 13).
-->

---

# Jet Tagging Problem Revisited

Statistical interpretation of DNN classification

<div class="absolute-center">

* Each jet class corresponds to a **probability density function** (PDF) $\rho_c(x)$ in an abstract latent space
* Optimal classifier estimates the **normalized PDF ratio**: $\hat{y}_c(x) = \frac{\rho_c(x)}{\sum_{c'} \rho_{c'}(x)}$
* This connects to physics: the PDF ratio corresponds to the ratio of **fully differential cross sections**
* **Implication**: with enough data and model capacity, DNNs can approach optimal signal-background separation for any analysis
* Larger models + larger datasets → closer to the theoretical optimum

</div>

<!-- 
This slide presents the key theoretical insight motivating Part V. From a statistical perspective, each jet class corresponds to a probability density function in an abstract high-dimensional space. The Neyman-Pearson lemma tells us the optimal discriminant is the PDF ratio, and cross-entropy training of a neural network is precisely learning to estimate this ratio. This means that DNN jet classification has a deep connection to the underlying physics — the PDFs correspond to fully differential cross sections. The implication is that with a large enough model and dataset, we can approach optimal discrimination for any signal-background pair, motivating the development of large, comprehensive pre-trained models.
-->

---

# Design Philosophy for Future Models

<div class="absolute-center">

Three aspects driving the design

1. **Expressiveness**: Transformers scale well with parameters and data, respecting particle data symmetries
2. **Large capacity**: GloParT reaches 10M parameters (20× ParticleNet); future models will grow further
3. **Comprehensiveness**: pre-train on hundreds of jet classes → learn a universal jet representation
   - Multiclass classifier stacks binary classifiers → output scores construct optimal discriminants for any pair of classes
   - Enables **transfer learning** to downstream analysis tasks

</div>

<!-- 
The design philosophy combines three complementary aspects. Expressiveness comes from the Transformer architecture, which handles particle-format data naturally and scales well. Large capacity — growing from ParticleNet's ~500K parameters to GloParT's 10M — allows the model to learn finer distinctions in the jet phase space. Comprehensiveness is achieved by pre-training on hundreds of diverse jet categories, covering all major resonance decay topologies. A key theoretical result is that a multiclass classifier trained with cross-entropy loss estimates the normalized PDF ratios for all classes simultaneously, so any binary discrimination can be constructed from the multiclass outputs — no retraining needed.
-->

---

<div class="flex-column">
<div>

# Pre-training and Fine-tuning Paradigm

Connecting conventional analysis-level training to transfer learning

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_10.2.png" alt=""/>
</div>
</div>

<!-- 
This figure illustrates how the pre-training and fine-tuning paradigm connects to existing CMS analysis practices. In conventional analyses, jet tagger output scores are used as inputs to event-level BDTs or neural networks. The transfer learning extension replaces these tagger scores with hidden-layer neuron values from a comprehensive pre-trained model, providing a richer jet representation. The pre-trained model's hidden layers encode a comprehensive understanding of jet phase space learned from hundreds of jet classes, and this knowledge transfers to downstream tasks — even those not seen during pre-training. This is analogous to using ImageNet-pretrained features for novel image classification tasks in computer vision.
-->

---
layout: section
---

# Part V: Pre-training and Fine-tuning

## Chapter 11: GloParT — Model Pre-training

<!-- 
Chapter 11 introduces the Global Particle Transformer (GloParT) — a comprehensive pre-trained jet model developed within the CMS experiment. GloParT is trained simultaneously as a 314-class classifier and a dual-target mass regressor, covering all major jet topologies including two-prong resonances, multi-prong WW*/ZZ*/top decays, and QCD jets. The model uses the ParT-L architecture with 10M parameters and represents the most comprehensive jet tagging model developed for CMS to date.
-->

---

<div class="flex-column">
<div>

# GloParT: 314 Jet Categories

Large-scale classification spanning all major jet topologies

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_11.1.png" alt=""/>
</div>
</div>

<!-- 
The 314 jet categories used for GloParT training cover the full diversity of jet topologies relevant for LHC physics. Two-prong categories include H→bb̄, cc̄, ss̄, qq̄, gg, ℓℓ, ττ and charged scalar decays (bc, cs, bs). Multi-prong categories cover H→WW* and H→ZZ* with all possible W/Z decay modes (fully hadronic, semi-leptonic) as well as top→bW topologies. QCD jets are split into 5 classes by heavy-flavour content. This comprehensive training set ensures GloParT learns a universal jet representation that can generalize to a wide range of downstream physics tasks.
-->

---
layout: two-cols
---

# GloParT Training

Samples and mass-decorrelated reweighting

* **Two-prong resonant jets**: produced via $\tilde G \to HH$ (resonant) and non-resonance di-$H$ production
  - Flat $p_T$ and $m_\text{SD}$ spectra for mass decorrelation
  - $m_H$: 15–250 GeV; $m_{\tilde G}$: 600–6000 GeV
* **Multi-prong jets**: $H \to W^{(*)}W^{(*)}$, $H \to Z^{(*)}Z^{(*)}$, $t \to bW$
  - Three $m_W/m_H$ configurations targeting SM-like and BSM topologies
* **QCD jets**: $p_T$-binned QCD multijet events from PYTHIA

::right::

<div class="flex-column">
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_11.2.png" alt=""/>
</div>
</div>

<!-- 
The training samples are carefully designed to ensure comprehensive phase space coverage and mass decorrelation. Two-prong jets are produced with variable resonance masses (15–250 GeV) and wide pT spans, ensuring flat kinematic distributions. For multi-prong jets, three configurations of mW/mH are used: one targeting SM-like H→WW*, one targeting on-shell WW, and one targeting off-shell WW — this ensures good tagging performance across different BSM mass hypotheses. The figure shows the generator-level mH and mW configurations for the H→W(*)W(*) samples.
-->

---

# GloParT Training Objective

Hybrid classification and regression loss

$$L_\text{tot} = L_\text{cls} + \lambda (L_\text{reg1} + L_\text{reg2})$$

* **Classification**: multiclass cross-entropy over 314 classes
  - Optimal solution: $\hat{y}_c(x) = \frac{\rho_c(x)}{\sum_{c'} \rho_{c'}(x)}$ — normalized PDF ratio
* **Regression**: log-cosh loss for two mass targets:
  - GEN-level resonance mass (resonant jets) / GEN-jet $m_\text{SD}$ including $\nu$ (QCD)
  - GEN-level visible-particle mass (resonant jets) / GEN-jet $m_\text{SD}$ excluding $\nu$ (QCD)
* $\lambda = 5$ to balance classification and regression

<!-- 
The hybrid loss function trains both classification and regression simultaneously. The classification part uses standard multiclass cross-entropy, whose theoretical minimum corresponds to estimating the normalized PDF ratios — meaning the 314 output scores have a well-defined statistical interpretation. The regression part uses log-cosh loss for two mass targets: the resonance mass and the visible-particle mass, which differ for jets with neutrinos in the final state. The visible-particle mass regression performs slightly better because it avoids the ambiguity of neutrino-related mass differences between jet classes.
-->

---

<div class="flex-column">
<div>

# GloParT Architecture

ParT-L: 10M parameters with separate embedding for three input groups

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_11.6.png" alt=""/>
</div>
</div>

<!-- 
The GloParT model uses the ParT-L (large) architecture with 10M parameters — approximately 20× the size of ParticleNet. A key architectural feature is the separate embedding for three input groups: charged PF candidates, neutral PF candidates, and secondary vertices. This split accommodates the significant differences in feature spaces between these groups (e.g., neutral candidates lack track-related features). After separate embedding, the tokens are concatenated and processed through 8 particle attention blocks and class attention blocks. The model outputs 314 classification nodes and 2 regression nodes.
-->

---

<div class="flex-column">
<div>

# GloParT: Statistical Interpretation

The multiclass classifier estimates normalized PDF ratios for all jet classes

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_11.5.png" alt=""/>
</div>
</div>

<!-- 
This figure illustrates the key statistical insight: each jet class corresponds to a PDF in an abstract jet phase space, and the optimal multiclass classifier outputs the normalized PDF ratio at each point. For any two classes A and B, the optimal discriminant is simply p(A)/(p(A)+p(B)), regardless of how many other classes are in the training set. This means GloParT's 314 output scores can construct optimal discriminants for any pair of classes without retraining — a powerful property that enables its use across hundreds of physics analyses.
-->

---

# GloParT: Classification Performance

<div class="absolute-center">

* **$H \to b\bar b$ vs QCD**: GloParT surpasses ParticleNet-MD (AUC: 0.9949 vs 0.9905 at 400–600 GeV)
* **$H \to c\bar c$ vs QCD**: similar improvement (AUC: 0.9935 vs 0.9883)
* **$H \to c\bar c$ vs $H \to b\bar b$**: significant gain in separating similar signals (AUC: 0.9949 vs 0.9905)
* Mass decorrelation: GloParT maintains good decorrelation with $m_\text{SD}$
* **Novel capabilities**: $b\bar c$, $b\bar s$, $c\bar s$ tagging; $H \to WW^*$ and top tagging in mass-decorrelated manner
* Model scaling: performance improves from ParT-lite → ParT-B → ParT-L

</div>

<!-- 
GloParT achieves superior classification performance compared to ParticleNet-MD across all benchmarked tasks. The improvements are particularly significant for distinguishing similar signal classes (e.g., H→cc̄ vs H→bb̄), where the larger model capacity and comprehensive training provide a clear advantage. GloParT also brings entirely new tagging capabilities not available in previous CMS taggers, including mass-decorrelated cs, bc, and bs tagging for BSM searches, and H→WW* tagging for boosted Higgs identification.
-->

---

<div class="flex-column">
<div>

# GloParT: Mass Regression Performance

Comparison of reconstructed mass resolution for $H \to b\bar b$ jets

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_11.17.png" alt=""/>
</div>
</div>

<!-- 
The mass regression performance of GloParT is compared with the soft-drop mass and the CMS ParticleNet regression algorithm. Using the GEN-level visible-particle mass as the regression target, GloParT achieves comparable or slightly better mass resolution than ParticleNet. The visible-particle mass target avoids the issue of shifted peaks caused by neutrino losses in multi-prong categories, which affects the resonance-mass target. This demonstrates that GloParT's comprehensive training does not sacrifice regression quality.
-->

---

<div class="flex-column">
<div>

# GloParT: Mass Decorrelation

$X \to c\bar c$ tagging discriminant mass decorrelation comparison

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_11.15.png" alt=""/>
</div>
</div>

<!-- 
The mass decorrelation performance shows that GloParT maintains good decorrelation with the soft-drop mass for QCD jets across different working points, comparable to the ParticleNet-MD tagger. This is critical for physics analyses that rely on fitting the jet mass spectrum to extract signal — any sculpting by the tagger would bias the result. The flat mass distributions at each working point confirm that GloParT's 314-class training does not introduce mass-dependent biases.
-->

---
layout: section
---

# Part V: Pre-training and Fine-tuning

## Chapter 12: GloParT — Model Fine-tuning

<!-- 
Chapter 12 demonstrates the practical value of the pre-trained GloParT model through two fine-tuning scenarios. The first shows that GloParT can tag novel jet categories not seen during pre-training, achieving near-optimal performance via lightweight transfer learning. The second shows that GloParT can be fine-tuned to derive mass-correlated jet models (like the CMS top tagger) by incorporating jet mass and pT as auxiliary inputs. Both scenarios demonstrate that comprehensive pre-training creates a powerful, reusable foundation for diverse downstream tasks.
-->

---

<div class="flex-column">
<div>

# Fine-tuning for Novel Jet Tagging

Tagging leptoquark $\text{LQ} \to b\tau$ jets — a class not in pre-training

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_12.1.png" alt=""/>
</div>
</div>

<!-- 
The first fine-tuning experiment demonstrates GloParT's generalization to a completely novel jet category: leptoquark LQ→bτ jets. The GloParT architecture is frozen, and only a lightweight 2-layer MLP is trained on the 256-dimensional hidden-layer features. The MLP has 38 output classes including the 3 new LQ→bτ modes and selected existing categories. The training uses only 256k jets per epoch (vs 7.68M in original training) and converges in just 15 epochs — the entire fine-tuning process is extremely lightweight compared to training from scratch.
-->

---

<div class="flex-column">
<div>

# Fine-tuning Performance

LQ $\to b\tau_h$ tagging: fine-tuned vs from-scratch comparison

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_12.3.png" alt=""/>
</div>
</div>

<!-- 
The fine-tuning results for LQ→bτh tagging show that GloParT achieves competitive performance compared to training from scratch with the new classes included. Against QCD, H→bb̄, and H→τhτh backgrounds, the fine-tuned model performs comparably or only slightly below the from-scratch baseline. The most challenging task — separating LQ→bτh from t→bW→bτhν — shows a larger gap (AUC 0.70 vs 0.78), as these topologies are very similar. Overall, the results demonstrate that GloParT's pre-trained latent representation contains sufficient information to generalize to unseen jet classes with minimal additional training.
-->

---

<div class="flex-column">
<div>

# Fine-tuning for New Models

Deriving a mass-correlated top tagger from GloParT

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_12.4.png" alt=""/>
</div>
</div>

<!-- 
The second fine-tuning scenario derives a mass-correlated top tagger from the mass-decorrelated GloParT model by incorporating jet mSD and pT as auxiliary inputs. An auxiliary 3-layer MLP takes the latent features together with mSD and pT, producing residual corrections to the original logits. This design is theoretically motivated: the mass-decorrelated and mass-correlated optimal classifiers are related by a function of mSD, so the auxiliary network learns this mass dependency. This approach has been integrated into the CMS software as part of the GloParT stage-3 model deployment.
-->

---

<div class="flex-column">
<div>

# Fine-tuning Results

Top vs QCD tagging: fine-tuned GloParT vs ParticleNet tagger

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_12.5.png" alt=""/>
</div>
</div>

<!-- 
The fine-tuned GloParT model for top tagging achieves performance comparable to or exceeding the dedicated ParticleNet top tagger used in CMS, despite being derived from a mass-decorrelated base model. This demonstrates that the comprehensive jet representation learned during pre-training, combined with the auxiliary mass-dependent network, can recover mass-correlated discrimination power. The result validates the paradigm of using a single comprehensive base model from which specialized taggers can be derived through lightweight fine-tuning.
-->

---
layout: section
---

# Part V: Pre-training and Fine-tuning

## Chapter 13: The Sophon Model and JetClass-II

<!-- 
Chapter 13 extends the pre-training philosophy beyond CMS-specific simulation by introducing the JETCLASS-II dataset and the Sophon model — a public implementation that enables reproducible research. JETCLASS-II contains 139M labelled jets across 188 categories with DELPHES fast simulation matching CMS Run-2 conditions. The Sophon model demonstrates three key applications: superior direct tagging performance, strong generalization via transfer learning to novel tasks, and powerful implications for LHC resonance search programmes including both targeted searches and anomaly detection.
-->

---

# JetClass-II Dataset

<div class="absolute-center">

* **139M labelled jets** across **188 categories** (vs 100M / 10 classes in original JetClass)
* Fast simulation via DELPHES with CMS Run-2-like conditions + PUPPI pileup removal
* Three major types:
  - **2-prong resonant jets** (15 classes): $b\bar b$, $c\bar c$, $s\bar s$, $q\bar q$, $bc$, $cs$, $gg$, $\ell\ell$, $\tau\tau$, ...
  - **3/4-prong resonant jets** (146 classes): all $Y^{(*)}Y^{(*)} \to$ quarks/leptons combinations
  - **QCD jets** (27 classes): categorized by $b$, $c$, $s$ quark content
* Variable resonance masses and flat $(p_T, m_\text{SD})$ spectra for mass decorrelation
* Public dataset for community use and reproducible research

</div>

<!-- 
JETCLASS-II is a major extension of the original JetClass dataset. With 188 categories spanning the full diversity of jet topologies at the LHC, it provides the most comprehensive training set for jet tagging studies to date. The DELPHES simulation includes realistic CMS-like detector effects including pileup and PUPPI mitigation, creating conditions closely resembling actual CMS data. The 27 QCD classes are particularly novel — splitting QCD jets by their complete heavy-flavour composition (number of b, c, and s quarks) enables fine-grained background modeling.
-->

---

<div class="flex-column">
<div>

# Sophon Model

Pre-training and application scheme

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_13.1.png" alt=""/>
</div>
</div>

<!-- 
The Sophon model uses the Particle Transformer architecture with 2.3M parameters, trained as a 188-class classifier on JETCLASS-II. The figure shows two application modes: (a) direct usage, where discriminants are constructed from ratios of output scores for specific signal and background classes; and (b) transfer learning, where the 128-dimensional hidden-layer features are used as inputs to a lightweight MLP for novel tagging tasks. The transfer learning approach requires only 1/320 of the training data and 1/1,000,000 of the computational cost compared to the original Sophon training.
-->

---

<div class="flex-column">
<div>

# Sophon: Direct Tagging

$X \to b\bar b$ tagging surpasses dedicated ParT and ParticleNet trainings

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_13.2.png" alt=""/>
</div>
</div>

<!-- 
The Sophon model's direct X→bb̄ tagging performance (top panel) surpasses dedicated binary ParT and ParticleNet classifiers trained specifically for this task with expanded training datasets. The Sophon* variant (trained on only 42 classes) performs worse, demonstrating that the large-scale comprehensive training is essential for achieving the best performance — even when the additional 146 classes are not directly related to the bb̄ task. The bottom panel shows the mass spectrum after applying the Sophon discriminant at εB = 10⁻⁴, revealing a clean signal peak for the X→bb̄ resonance at 200 GeV.
-->

---

<div class="flex-column">
<div>

# Sophon: Transfer Learning

$X \to b\bar s$ tagging — a novel class not in pre-training

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_13.3.png" alt=""/>
</div>
</div>

<!-- 
The transfer learning capability of Sophon is demonstrated on the X→bs̄ tagging task, which was not included in the 188 pre-training classes. After fine-tuning a lightweight MLP on Sophon's latent features, the model surpasses dedicated ParT and ParticleNet binary classifiers trained specifically for X→bs̄ vs QCD — even though those dedicated models use 16M signal jets while the transfer learning uses only a fraction of the data. This demonstrates that the knowledge embedded in Sophon's latent space transfers effectively to unseen jet topologies, confirming the value of comprehensive pre-training.
-->

---

<div class="flex-column">
<div>

# Implications for LHC Resonance Searches

Sophon enables three novel search strategies

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_13.4.png" alt=""/>
</div>
</div>

<!-- 
By applying various Sophon discriminants at progressively tighter thresholds, the SM hadronic peak structures of the W boson (via W→cs), Z boson (via Z→bb̄), and top quark (via t→bqq') emerge clearly from the QCD background. This demonstrates a universal approach for resonance searches: even without knowing the target resonance properties, one can construct hundreds of discriminants from the 188 output scores and scan the mass spectrum for potential peaks. This paradigm shift enables comprehensive, model-independent searches with minimal effort.
-->

---

<div class="flex-column">
<div>

# Sophon for Anomaly Detection

Significance improvement with IAD method using Sophon transfer learning

</div>
<div class="center-container">
<img border="rounded" src="/part_IV-V/Figure_13.8.png" alt=""/>
</div>
</div>

<!-- 
The Sophon model's knowledge also boosts anomaly detection through weakly-supervised classifiers. Using the Idealized Anomaly Detector (IAD) method with Sophon's latent features as inputs, the maximum significance improvement is substantially better than using conventional high-level jet variables, and the sensitivity threshold drops to approximately 0.6–1.0σ initial significance. The signal-targeted Sophon discriminant achieves even faster discovery, requiring ~3.5× fewer signal events than the IAD approach. This demonstrates that comprehensive pre-training enhances both targeted searches and model-agnostic anomaly detection.
-->

---
layout: section
---

# Chapter 14: Outlook

<!-- 
Chapter 14 provides the outlook for the field, connecting the thesis contributions to the broader trajectory of collider physics and AI. The rapid development of deep learning is driving what many consider the next industrial revolution, and particle physics is uniquely positioned to benefit from these advances. The four aspects covered in this thesis — algorithms, calibration, physics applications, and the pre-training paradigm — each have promising future directions that will shape how LHC data is analyzed in the coming decade.
-->

---

# Outlook

<div class="absolute-center">

**Algorithms**: Transformer efficiency improvements needed for high-luminosity LHC; Lorentz symmetry preservation may become standard; future models may process raw detector data

**Calibration**: push toward full phase-space calibration using DNN-based reweighting; essential as taggers are applied to more diverse signatures

**Physics applications**: GloParT enables broader boosted-topology searches; hundreds of discriminants → comprehensive bump hunting across all final states without calibration; combined with calibration methods → precision measurements

**Pre-training paradigm**: GloParT stage-3 integrated into CMS software for Run 3 analyses; expected to enhance Higgs property measurements ($H \to b\bar b$, $c\bar c$, $WW^*$, $\tau\tau$), di-Higgs searches, and anomaly detection programmes

</div>

<!-- 
The outlook connects all four pillars of the thesis to future developments. On algorithms, the key challenge is efficiency — Transformers' quadratic complexity becomes a bottleneck as particle multiplicities grow at the HL-LHC. For calibration, DNN-based full phase-space reweighting could replace proxy-based methods. For physics, the GloParT model opens hundreds of new analysis channels by providing discriminants for all major jet topologies. The pre-training paradigm is now moving from proof-of-concept to production deployment: the GloParT stage-3 model was integrated into CMS software in November 2024 and is expected to enhance numerous upcoming CMS analyses using Run 3 data.
-->
