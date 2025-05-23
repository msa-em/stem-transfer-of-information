---
title: Iterative Ptychography with a Pixelated Detector
short_title: Pixelated iterative ptycho
numbering:
  enumerator: 6.%s
label : pixelated_ptycho_page
---

The direct ptychographic methods we have introduced so far retrieve the phase information directly from the interference between the direct and scattered beams.
Still, the scattering redundancy contained in the observed diffraction intensities can be used to solve the inverse scattering problem, by iteratively obtaining self-consistent estimates for the sample and probe [@10.1007/978-3-030-00069-1_17].
This leverages our understanding of the physics of the interaction between the probe and the sample, as well as the @stem_image_formation_sec mechanism &ndash; collectively known as the "forward model".

The flexibility of the ptychographic forward model allows us to reconstruct increasingly complex scattering physics and phenomena.
@ptycho_table summarizes various scattering physics approximations and the corresponding ptychographic techniques used to reconstruct them.
In what follows, we focus on the WPOA and thus use single-slice ptychography.
Extending our analyses to mixed-state and multi-slice ptychography is left for future work.

:::{table}
:label: ptycho_table

Incomplete summary of ptychographic techniques and their usecases.

| **Applicability/Physical Phenomenon**  | **Conventional Name/Reference**                              |
| -------------------------------------- | ------------------------------------------------------------ |
| Thin or weakly-scattering objects      | Single-slice ptychography [@10.1016/j.ultramic.2009.05.012] |
| 'Thick' or multiply-scattering objects | Multi-slice ptychography [@https://www.science.org/doi/10.1126/science.abg2533] |
| Partial probe coherence                | Mixed-state ptychography [@10.1038/nature11806] |
| Tilt-series of 'thick' objects         | Joint ptychographic tomography [@https://journals.aps.org/prapplied/abstract/10.1103/PhysRevApplied.19.054062] |

:::

## Numerical White-Noise Object

The iterative nature of iterative ptychography does not lend itself well to analytical CTF expressions like the ones derived in the previous sections.
Instead, we use a numerical scheme to estimate the transfer of information using ptychographic reconstructions.

We isolate the dependence of the sample potential during phase-retrieval by reconstructing a [](wiki:White_noise) object, with scattering information across all spatial frequencies.
Specifically, we define a 2D white noise sample in diffraction space using random phases drawn from a [](wiki:Normal_distribution), and a constant unity amplitude:
:::{math}
:label: white_noise_obj_eq
\begin{aligned}
\tilde{\phi}(\bm{q}) &\sim \mathcal{N}(0,1) \quad \forall \, \bm{q}, \quad \text{such that} \quad \tilde{\phi}(\bm{q}) = \tilde{\phi}^{\ast}(-\bm{q}), \\
\phi(\bm{r}) &= \mathcal{F}^{-1}_{\bm{q}\rightarrow \bm{r}}\left[\tilde{\phi}(\bm{q})\right] \\
\end{aligned},
:::
where $\mathcal{N}(0,1)$ denotes a zero-mean normal distribution with unit standard deviation.

The white-noise object is then used to perform Nyquist-sampled STEM simulations using Equations @exit-wave-eq - @probability-density-eq.
Following phase-retrieval on the simulated datasets, the magnitude of the CTF can be directly estimated using the power spectrum of the reconstructed phase, $\phi^{\prime}(\bm{r})$:
:::{math}
:label: numerical_ctf_eq
\left|\mathcal{L}^{\mathrm{numerical}}(\bm{q}) \right| = \left| \mathcal{F}_{\bm{r} \rightarrow \bm{q}} \left[ \phi^{\prime}(\bm{r}) \right] \right|.
:::

:::{note} Note:
All the analytical expressions presented in previous sections have also been validated against numerical CTF calculations using white-noise objects defined using @white_noise_obj_eq and @numerical_ctf_eq.
:::

## Iterative Ptychography CTF

:::{figure} #app:pixelated_iterative_ptycho
:label: fig_pixelated_iterative_ptycho
:placeholder: ./figures/pixelated_iterative_ptycho_placeholder.png
Effect of various probe aberrations and iterations on the CTF for iterative ptychography with a pixelated detector.
The resulting CTF is shown on the left panel, with its radial average in the middle panel, and its effect on example weak phase objects on the right panel.
Note that the batch size refers to the number of probe positions which are simultaneously updated which impacts the convergence of the ptychographic reconstruction.
:::

While, in contrast to direct ptychographic techniques, iterative ptychography can recover both the sample and the probe through "blind deconvolution", in practice, robust estimates of the aberration coefficients significantly improve the reconstruction quality and convergence.
[](#fig_pixelated_iterative_ptycho) plots @numerical_ctf_eq for low-order isotropic aberration coefficients, namely $C_{1,0}$ and $C_{3,0}$.
We note the following:

- At early iterations (and non-zero $C_{1,0}$/$C_{3,0}$), the iterative ptychography CTF illustrates "Thon-like" oscillations [@10.1515/zna-1966-0417].
- With more iterations, the CTF approaches the ideal unity CTF, with all spatial frequencies recovered exactly.
- Lower-spatial frequencies are slower to converge.
- The super-resolution capabilities of iterative ptychography, are hinted to by the non-zero corner regions of the 2D CTF.
