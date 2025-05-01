---
title: Iterative Ptychography with a Pixelated Detector
short_title: Pixelated iterative ptycho
numbering:
  enumerator: 6.%s
label : pixelated_ptycho_page
---

:::{warning} To-Do:
Add general iterative ptychography intro.
:::

The ptychographic methods that we have introduced so far, iCOM and SSB, are both direct ptychography methods, meaning that they retrieve the phase information directly from the diffraction pattern signal.
But the redundancy of 4D dataset and overlapping regions of the CBED pattern also allow us to solve the inverse scattering problem to find the object and the probe that gave rise to the recorded diffraction patterns iteratively.
Since we know the nature of the interaction between the probe and the sample, as well as the image formation in the far-field where the CBED patterns are recorded, the redundancy in the data set should be enough to find the unknown sample provided we have a good guess for the probe.
This typically means that the aberration coefficients should be know, or estimated from the data.

## Numerical White-Noise Object

Unfortunately, the iterative nature of iterative ptychography does not lend itself well to analytical CTF expressions like the ones derived in the previous sections.
Instead, we use a numerical scheme to estimate the transfer of information using ptychographic reconstructions.

We deconvolve the dependence of the sample potential during phase-retrieval by reconstructing a white-noise object, with scattering information across all spatial frequencies.
Specifically, we define a 2D white noise object in diffraction space using random phases and a constant unity amplitude:
:::{math}
:label: white_noise_obj_eq
\begin{aligned}
\tilde{\phi}(\bm{q}) &\sim \mathcal{N}(0,1) \quad \forall \bm{q}, \quad \text{such that} \quad \tilde{\phi}(\bm{q}) = \tilde{\phi}^{\ast}(-\bm{q}), \\
\phi(\bm{r}) &= \mathcal{F}^{-1}_{\bm{q}\rightarrow \bm{r}}\left[\tilde{\phi}(\bm{q})\right] \\
\end{aligned}
:::

The white-noise object is then used to perform Nyquist-sampled STEM simulations using Equations @exit-wave-eq - @probability-density-eq.
Following phase-retrieval on the simulated datasets, the CTF can be directly estimated using the power spectrum of the reconstructed phase, $\phi^{\prime}(\bm{r})$:
:::{math}
:label: numerical_ctf_eq
\left|\mathcal{L}^{\mathrm{numerical}}(\bm{q}) \right| = \left| \mathcal{F}_{\bm{r} \rightarrow \bm{q}} \left[ \phi^{\prime}(\bm{r}) \right] \right|.
:::

:::{note} Note:
All the analytical expressions presented in this article have been tested against numerical CTF calculations using white-noise objects defined using @white_noise_obj_eq and @numerical_ctf_eq.
:::

## Iterative Ptychography CTF

:::{figure} #app:pixelated_iterative_ptycho
:label: fig_pixelated_iterative_ptycho
:placeholder: ./figures/pixelated_iterative_ptycho_placeholder.png
Effect of various probe aberrations and iterations on the CTF for iterative ptychography with a pixelated detector.
The resulting CTF is shown on the left panel, with its radial average in the middle panel, and its effect on example weak phase objects on the right panel.
:::

[](#fig_pixelated_iterative_ptycho) plots @numerical_ctf_eq for low-order isotropic aberration coefficients, namely $C_{1,0}$ and $C_{3,0}$.
We note the following:

* At early iterations (and non-zero $C_{1,0}$/$C_{3,0}$), the iterative ptychography CTF illustrates "Thon-like" oscillations.
* With more iterations, the CTF approaches the ideal unity CTF, with all spatial frequencies recovered exactly.
* Lower-spatial frequencies are slower to converge.
* Iterative ptychography has super-resolution capabilities, as can be seen by the corners of the 2D CTF.
