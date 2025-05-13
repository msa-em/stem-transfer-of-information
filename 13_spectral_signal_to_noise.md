---
title: Spectral Signal to Noise
numbering:
  enumerator: 13.%s
label : ssnr_page
---

So far, this article has focused on deriving analytical and numerical CTFs for various reconstruction techniques and experimental parameters, notably probe aberrations and segmented detector geometry.
The CTF is an important metric in evaluating linear imaging systems, representing the maximum usable signal.
However, it fails to capture the Poisson-limited nature of physical detectors for experiments done with finite electron fluence.

## Spectral Signal to Noise Ratio

To remedy this, we utilize a statistical framework to evaluate the transfer of information of the various reconstruction techniques and acquisition parameters.
Specifically, we perform independent reconstructions on simulated diffraction intensities with finite electron fluence by performing $M$ Poisson draws on the _same_ white noise object.
We then analyze the reconstruction fidelity using the spectral signal-to-noise ratio (SSNR) defined as [@https://doi.org/b8289r]:
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

## Detective Quantum Efficiency

We note in passing that the simple SSNR metric defined in @ssnr_eq, is closely related to detective quantum efficiency (DQE) &ndash; another popular metric in analyzing the efficiency of linear imaging systems &ndash; according to [@10.1051/bioconf/202412904007]:

:::{math}
:label: dqe_eq
\mathrm{DQE}(\bm{q}) = \frac{\mathrm{SSNR}_{\mathrm{out}}^2(\bm{q})}{\mathrm{SSNR}_{\mathrm{in}}^2(\bm{q})},
:::
where $\mathrm{SSNR}_{\mathrm{in}}(\bm{q})$ denotes the SSNR of a reference or "ideal" reconstruction.
This is usually taken as the HRTEM SSNR when using an ideal Zernike phase-plate [@https://doi.org/cvdgrj], which for a white-noise object is simply given by the squared root of the electron fluence.
As such, the metrics are trivially related in our case, and in what follows we use the simpler SSNR metric.

## iCOM SSNR

@fig_static_icom_ssnr plots the SSNR calculation for in-focus pixelated and segmented iCOM, using $M=256$ and a total electron budget of $N_e = 10^8 \, e^-/\mathrm{probe}$.
We note the following:

- The SSNR numerator, which corresponds to the maximum usable signal, is identical to the absolute value of the CTF we computed in @pixelated_icom_page and @segmented_icom_page.
- The iCOM reconstruction noise, given by the SSNR numerator, is inversely proportional to the spatial frequency, $\bm{q}$.
  - As such, the SSNR metric correctly tends to zero for both $\bm{q}\rightarrow 0$ and $\bm{q} \rightarrow 2\, q_{\mathrm{probe}}$
- In contrast to the segmented detector signal, the segmented detector noise exhibits no dependence on the detector geometry.
  - The same is true for the effect of probe aberrations.

:::{figure} ./figures/static_icom_ssnr_placeholder.png
:label: fig_static_icom_ssnr
SSNR calculation for pixelated and segmented iCOM, highlighting that the noise is inversely linear with spatial frequency and is independent of detector geometry.
:::

This last observation suggests we can use an analytical expression for the iCOM noise as $\bm{q}^{-1}$, and thus compute the iCOM SSNR faster.
@fig_icom_ssnr illustrates this interactively, allowing practitioners to quickly evaluate the iCOM SSNR for various detector geometries and acquisition parameters.

:::{figure} #app:snr_segmented_icom
:label: fig_icom_ssnr
:placeholder: ./figures/widget_icom_ssnr_placeholder.png
Interactive widget demonstrating analytical iCOM SSNR for various detector geometries.
:::

:::{note} Note:
While this article only demonstrates the SSNR for iCOM, we present similar numerical and analytical results for other phase retrieval methods in a companion article [enter cross-link once published](https://elementalmicroscopy.org).
:::
