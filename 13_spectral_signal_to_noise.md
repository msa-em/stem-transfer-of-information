---
title: Spectral Signal to Noise
numbering:
  enumerator: 13.%s
label : ssnr_page
---

So far, this article has focused on deriving analytical and numerical CTFs for various reconstruction techniques and experimental parameters, notably probe aberrations and segmented detector geometry.
The CTF is an important metric in evaluating linear imaging systems, representing the maximum usable signal.
However, it fails to capture the Poisson-limited nature of physical detectors for experiments done with finite electron fluence.

## SSNR and Detective Quantum Efficiency

To remedy this, we perform $M$ independent reconstructions on Poisson draws at finite electron fluence using simulated diffraction intensities on the _same_ white noise object, and analyze their statistics using  the spectral signal-to-noise ratio (SSNR) defined as [@https://doi.org/b8289r; @10.1051/bioconf/202412904007]:
:::{math}
:label: ssnr_eq
\begin{aligned}
\mathrm{SSNR}(\bm{q}) &= \frac{\left| \sum_i \Phi_i(\bm{q}) / M \right|}{
  \sqrt{ \sum_i \left| \Phi_i(\bm{q}) - \bar{\Phi}(\bm{q}) \right| / (M-1)}
 } \\
\Phi_i(\bm{q}) &= \mathcal{F}_{\bm{r} \rightarrow \bm{q}}\left[\phi_i^{\prime}(\bm{r}) \right],
\end{aligned}
:::
where the overbar denotes an average value.
Intuitively, @ssnr_eq represents the absolute value of the sample mean divided by the sample standard deviation of the independent reconstructions for each spatial frequency $\bm{q}$.

We note in passing that the simple SSNR metric defined in @ssnr_eq, is closely related to detective quantum efficiency &ndash; another popular metric in analyzing the efficiency of linear imaging systems &ndash; according to:

:::{math}
:label: dqe_eq
\mathrm{DQE}(\bm{q}) = \frac{\mathrm{SSNR}_{\mathrm{out}}^2(\bm{q})}{\mathrm{SSNR}_{\mathrm{in}}^2(\bm{q})},
:::
where $\mathrm{SSNR}_{\mathrm{in}}(\bm{q})$ denotes a reference or "ideal" SSNR.
This is usually taken as the HRTEM SSNR when using an ideal Zernike phase-plate [@https://doi.org/cvdgrj], which for a white-noise object is simply given by the squared root of the electron fluence.
As such, the metrics are trivially related in our case, and in what follows we use the simpler SSNR metric.

## iCOM SSNR

:::{figure} ./figures/static_icom_ssnr_placeholder.png
:label: fig_static_icom_ssnr
SSNR calculation for pixelated and segmented iCOM, highlighting that the noise is inversely linear with spatial frequency and is independent of detector geometry.
:::

:::{figure} #app:snr_segmented_icom
:label: fig_icom_ssnr
:placeholder: ./figures/widget_icom_ssnr_placeholder.png
Interactive widget demonstrating analytical iCOM SSNR for various detector geometries.
:::
