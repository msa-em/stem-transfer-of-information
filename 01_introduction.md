---
title: Introduction
numbering:
  enumerator: 1.%s
label : introduction_page
---

## Phase Retrieval Methods

When a converged electron probe passes through a thin sample, the electron wavefunction is modulated in both phase and amplitude.
Most of the sample information we are typically interested in, is encoded in the phase of the electron wavefunction.
However, this information is "lost" during intensity measurements using physical detectors &ndash; giving rise to the so-called "phase problem" [@10.1080/713819083; @10.1364/AO.21.002758].
This is further exacerbated for weakly-scattering samples, such as soft or biological materials, which exhibit negligible amplitude contrast.
To remedy this, a number of phase-retrieval techniques have been developed to computationally reconstruct this phase information from intensity measurements.

The simplest such technique is the integrated center of mass (iCOM) method [@dekkers_differential_1974; @lazic_phase_2016], which recovers the projected sample phase by integrating an estimate of the scattered probe COM.
Direct ptychographic methods, such as single side-band (SSB) [@10.1016/j.ultramic.2014.09.013; @10.1016/j.ultramic.2016.09.002], Wigner distribution deconvolution (WDD) [@rodenburg_wdd_1992; @10.1016/j.ultramic.2017.02.006], optimum bright field (OBF) [@10.1016/j.ultramic.2020.113133; @10.1093/jmicro/dfae051], and tilt-corrected bright field (tcBF) [@10.1101/2024.04.22.590491; @10.69761/XUNR2166], retrieve the phase more explicitly using the interference information in overlapping regions between unscattered and scattered beams.
The phase information can also be retrieved by solving the inverse scattering problem of how the probe and sample interact to produce the observed intensity measurements.
Solving this iteratively, in a family of techniques under the umbrella of iterative ptychography [@10.1007/978-3-030-00069-1_17], provides self-consistent estimates for both the probe and the sample.

## Article Outline

In this work, we investigate the efficacy of STEM phase retrieval methods to transfer phase information, as a function of the imaging system properties and experimental parameters, using a combination of analytical and numerical analyses and interactive widgets.

The manuscript is structured as follows:
First, we introduce the theory of image formation in STEM experiments following {cite:t}`https://doi.org/chsgqd`, highlighting the limiting components for the contrast transfer of information (CTF) &ndash; namely the probe aperture and the aberrations surface.
We then introduce analytical expressions for the CTF for each reconstruction method using pixelated detectors, before investigating how robust the CTF is to acquisitions with few-pixel, segmented detectors.
Motivated by our observations, we propose a direct ptychographic algorithm which combines tcBF and SSB, to achieve upsampled reconstructions without missing frequencies (CTF zero-crossings).
Finally, we consider the effect of Poisson-limited detectors and finite electron fluence, by introducing the spectral signal-to-noise (SSNR) formalism for statistically evaluating the transfer of information.
