---
title: Direct Ptychography with a Pixelated Detector
short_title: Pixelated SSB
numbering:
  enumerator: 4.%s
label : pixelated_ssb_page
---

Direct ptychographic methods can be viewed as deconvolution techniques, which model the interference information encoded in the overlap between the first order diffracted beams and the direct beam, and use that to extract the sample phase.
Intuitively, for a specific wavevector $\bm{q}$, the convolutional effect of the probe can be modeled to estimate the expected phase modulation in the observed diffraction patterns, and any additional phase modulation may thus be attributed to the sample.

Different direct ptychographic techniques perform this deconvolution differently:

- (traditional) SSB [@10.1016/j.ultramic.2014.09.013], sums the phase information in one of the "double-overlap" regions to obtain an average estimate of the sample phase
  - This only works in the absence of probe aberrations and will be omitted in this work.
- (phase-compensated) SSB [@10.1016/j.ultramic.2016.09.002], uses @ssb_gamma_eq to perform multiplicative deconvolution, thus "flattening" the phase in the "double" and "triple" overlap regions before summing to obtain a more robust estimate of the sample phase.
- OBF [@10.1016/j.ultramic.2020.113133], uses the same multiplicative deconvolution idea, albeit using a signal-to-noise optimizing normalization weights.
  - This is traditionally used with segmented detectors and we explore it further in @segmented_ssb_page.
- WDD [@10.1016/j.ultramic.2016.09.002], uses Wiener deconvolution to isolate the sample phase, after first casting the expected phase modulation in terms of the shifted [](wiki:Wigner_distribution_function).
- tcBF [@10.1101/2024.04.22.590491], does not traditionally use deconvolution but we introduce a novel algorithm leveraging multiplicative deconvolution in @upsampled_ssb_page.

## Phase Compensated SSB CTF

In contrast to the detector response functions we have investigated so far, direct ptychography can utilize all the phase information in the complex-valued aperture-overlap function @ssb_gamma_eq.
This suggests that its CTF is instead given by summing the non-zero regions of @ssb_gamma_eq, which yields:

:::{math}
:label: ssb_ctf_eq
\mathcal{L}^{\mathrm{SSB}}(\bm{q}) = \frac{\mathrm{i}}{2} \int  \left|\Gamma(\bm{q},\bm{k}) \right| d\, \bm{k}.
:::

While the absolute value inside the integrand precludes a cleaner expression using correlation functions, which rely on linearity, @ssb_ctf_eq can be parallelized efficiently across spatial frequencies, $\bm{q}$.

For completeness, we note in passing that for the ideal case of no probe aberrations, $\chi(\bm{k})=0$, @ssb_ctf_eq reduces to the well-known geometric "double-minus-triple overlap" expression given by [@10.1016/j.ultramic.2014.10.013]:

:::{math}
:label: geometric_ssb_ctf_eq
\mathrm{Im}\left\{\mathcal{L}^{\mathrm{ideal \, SSB}}(\bm{q})\right\} = \begin{cases} [A \star A](\bm{q}) - [A \star A](2\,\bm{q}) & if \left| \bm{q} \right| \lt q_0 \\
[A \star A](\bm{q}) & \mathrm{otherwise}
\end{cases}
:::

:::{figure} #app:pixelated_ssb
:label: fig_pixelated_ssb
:placeholder: ./figures/pixelated_ssb_placeholder.png
Effect of various probe aberrations on the CTF for SSB direct ptychography with a pixelated detector.
The resulting CTF is shown on the left panel, with its radial average in the middle panel, and its effect on example weak phase objects on the right panel.
:::

[](#fig_pixelated_ssb) plots @ssb_ctf_eq for low-order isotropic aberration coefficients, namely $C_{1,0}$ and $C_{3,0}$.
We note the following:

- The CTF tends to zero for $\bm{q} \rightarrow 0$ and $\bm{q} \rightarrow 2\, q_{\mathrm{probe}}$, peaking in between.
- The CTF is purely positive, leading to no contrast reversals with aberrations (and by extension thickness).
- Similar to iCOM, the Scherzer defocus condition is suboptimal in the presence of spherical aberration, since the SSB CTF exhibits no zero-crossings.
