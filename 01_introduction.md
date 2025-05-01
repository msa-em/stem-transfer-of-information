---
title: Introduction
numbering:
  enumerator: 1.%s
label : introduction_page
---

## Phase Retrieval Methods

When the STEM electron beam traverses the sample the wavefunction of the electrons may be modulated in both phase and amplitude.
The electron wavefunction contains all the information about the sample and the probe, including the aberration surface.
However, since the electron wavefunction is complex, and the phase information is contained in its imaginary part, all of the phase information is lost upon detection by real detectors.
This is because real detectors are only able to detect intensity variations, the absolute square of the electron wavefunction, and can not record complex information.
Because a lot of the information we are typically interested in when imaging a sample is encoded in the phase of the electron wavefunction, this phase problem is a hindrance and numerous methods for retrieving the phase information have been developed.


The simplest method is the center of mass (COM) method, which estimates the phase of the beam through its relation to the deflection of the COM of the CBED pattern.
Specifically, this COM is proportional to the gradient of the phase, which means that the phase may be retrieved through integration of the COM signal, typically termed integrated center of mass (iCOM).
Other methods retrieve the phase more explicitly from the redundant information in overlapping regions between the unscattered and scattered beams.
Single side-band ptychography (SSB) is one such method, which retrieves the phase modulation applied to the beam by the sample by extracting any additional phase modulation than the expected from the double overlap regions of zeroth and first order diffraction disks. 
Applying signal-to-noise optimising weights to the SSB phase reconstruction yields the optimum bright field (OBF) method. 
These are direct phase retrieval methods, but it is also possible to retrieve the phase information iteratively by solving the inverse scattering problem of how the probe and object interact to produce the CBED patterns. 
This is done by comparing a guess for the STEM probe to the recorded CBED patterns, which informs how the object must have modulated the probe and thus updates the object reconstruction and the probe guess.
Performing this procedure iteratively, a solution for both the probe and the object may be found, and the only prior information used is that of how the probe and the object interact.


(stem_image_formation)=
## STEM Image Formation

The electron wavefunction of a converged electron probe exiting a thin sample is given by [@https://doi.org/chsgqd]:
:::{math}
:label: exit-wave-eq
\psi^{\mathrm{obj}}_{\bm{r}^{\prime}}(\bm{r}) = T(\bm{r}) \times \psi(\bm{r}^{\prime}-\bm{r}),
:::
where $\psi$ is the converged electron probe at the object plane, centered at position $\bm{r}^{\prime}$ and defined across arbirtary positions $\bm{r}$ in the object plane, $T(\bm{r}) = \exp\left[\mathrm{i}\,\phi(\bm{r}) \right]$ is the complex-valued transmission function of the sample phase, $\phi(\bm{r} )$.

The transmitted electron wavefunction is then propagated to the far-field detector plane given by:
:::{math}
:label: detector-exit-wave-eq
\psi^{\mathrm{det}}_{\bm{r}^{\prime}}(\bm{k}) = \mathcal{F}_{\bm{r} \rightarrow \bm{k}} \left[ \psi^{\mathrm{obj}}_{\bm{r}^{\prime}}(\bm{r}) \right],
:::
where $\mathcal{F}_{\bm{r} \rightarrow \bm{k}}$ is the Fourier operator which transforms positions in the object plane, $\bm{r}$, to positions in the detector plane, $\bm{k}$.

While the electron wavefunction at the detector plane is complex-valued, physical detectors can only record its probability density, given by:
:::{math}
:label: probability-density-eq
J^{\mathrm{det}}_{\bm{r}^{\prime}}(\bm{k}) = \left| \psi^{\mathrm{det}}_{\bm{r}^{\prime}}(\bm{k}) \right|^2,
:::
where we have omitted the incoherent integrals resulting from the temporal and spatial partial coherence of the electron source [@https://doi.org/chsgqd].

Finally, the intensity recorded on a specific detector segment or pixel is given by:
:::{math}
:label: detector-intensity-eq
I_{j,\bm{r}^{\prime}} = \int J^{\mathrm{det}}_{\bm{r}^{\prime}}(\bm{k}) D_j(\bm{k})\, d\bm{k},
:::
where $D_j(\bm{k})$ is the detector response function for the j<sup>th</sup> segment or pixel.

(stem_ctf)=
## Contrast Transfer Functions

In general, the relationship between [](#probability-density-eq) and the sample phase is non-linear.
For weak-phase objects which only scatter the incoming illumination weakly, and can thus be well approximated using the leading terms of the Taylor expansion:
:::{math}
:label: weak-phase-taylor-exp-eq
T(\bm{r}) = \exp\left[\mathrm{i}\,\phi(\bm{r})\right] \approx 1 + \mathrm{i}\, \phi(\bm{r}),
:::
then the image formation theory described above becomes linear, and the image contrast is proportional to the sample phase.
This is most commonly expressed in terms of the intensity Fourier transform, $\tilde{I}_{j,\bm{q}^{\prime}} = \mathcal{F}_{\bm{r}^{\prime} \rightarrow \bm{q}^{\prime}}\left[ I_{j,\bm{r}^{\prime}} \right]$, as a function of spatial frequency,$\bm{q}^{\prime}$:

:::{math}
:label: ctf-eq
\tilde{I}_{j,\bm{q}^{\prime}} = 2\, \tilde{\phi}(\bm{q}^{\prime}) \times \mathcal{L}_j(\bm{q}^{\prime}),
:::
where $\mathcal{L}_j(\bm{q}^{\prime})$ is the complex-valued contrast transfer of information (CTF), which is sample-independent and depends on the properties of the imaging system, such as the incoming illumination aperture and aberrations, the detector geometry, and the reconstruction method.

## Article Outline

In this work, we investigage the CTF as a function of the imaging system properties and provide quantitative comparisons between the efficiency of different phase retrieval methods.

The manuscript is structured as follows:
First, we introduce the components of the incoming illumination limiting the transfer of information for STEM measurements, namely the probe aperture and the aberrations surface.
We then investigate the effect of the reconstruction method in extracting this information for pixelated detectors, introducing analytical expressions for each method.
Next, we consider how robust the CTF is to acquisitions with few-pixel, segmented detectors.
Motivated by our observations, we propose a direct ptychographic algorithm which combines tcBF and SSB, to achieve upsampled reconstructions without missing frequencies (CTF zero-crossings).
Finally, we consider the effect of Poisson-limited detectors and finite electron fluence, by introducing the spectral signal-to-noise (SSNR) method for statistically evaluating the transfer of information.
