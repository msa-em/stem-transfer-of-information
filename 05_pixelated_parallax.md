---
title: Tilt-Corrected Bright-Field STEM with a Pixelated Detector
short_title: Pixelated tcBF
numbering:
  enumerator: 5.%s
label : pixelated_parallax_page
---

:::{warning} To-Do:
Add general parallax intro.
:::

## Tilt-Corrected BF STEM CTF

The tilt-corrected BF STEM CTF can be understood by starting with the complex-valued aperture overlap function @ssb_gamma_eq, reproduced here for convenience:
:::{math}
:label: gamma_aperture_chi_eq
\Gamma(\bm{Q},\bm{k}) = A(\bm{k})A(\bm{q}-\bm{k})\mathrm{e}^{-\mathrm{i}\chi(\bm{Q}-\bm{k})}\mathrm{e}^{\mathrm{i}\chi(\bm{k})} - A(\bm{k})A(\bm{q}+\bm{k})\mathrm{e}^{\mathrm{i}\chi(\bm{Q}+\bm{k})}\mathrm{e}^{-\mathrm{i}\chi(\bm{k})}.
:::

To proceed, we wish to factorize @gamma_aperture_chi_eq to read:
:::{math}
:label: gamma_factorization_eq
\begin{aligned}
\Gamma(\bm{Q},\bm{k}) &\approx \Beta(\bm{Q},\bm{k}) \mathrm{e}^{\mathrm{i}\nabla\chi \cdot \bm{k}} \\
\Beta(\bm{Q},\bm{k}) &= A(\bm{k})\left(A(\bm{Q}-\bm{k})\mathrm{e}^{-\mathrm{i}\chi(\bm{Q})} - A(\bm{Q}+\bm{k})\mathrm{e}^{\mathrm{i}\chi(\bm{Q})}\right),
\end{aligned}
:::
where the term involving the gradient of the aberration surface, $\nabla \chi$, is a phase ramp corresponding to the lateral shifts observed in tcBF measurements.

The tcBF CTF is then obtained by summing $\Beta(\bm{Q},\bm{k})$ over $\bm{k}$:
:::{math}
:label: parallax_ctf_eq
\begin{aligned}
\Im\left\{\mathcal{L}^{tcBF}(\bm{Q})\right\}  &= \int \Beta(\bm{Q},\bm{k}) d\, \bm{k} \\
                                              &= -\left[A \star A\right](\bm{Q}) \sin\left[\chi(\bm{Q})\right],
\end{aligned}
:::
which we recognize as the axial CTF modulated by the aperture auto-correlation envelope.

:::{figure} #app:pixelated_parallax
:label: fig_pixelated_parallax
:placeholder: ./figures/pixelated_parallax_placeholder.png
Effect of various probe aberrations on the CTF for tcBF with a pixelated detector.
The resulting CTF is shown on the left panel, with its radial average in the middle panel, and its effect on example weak phase objects on the right panel.
:::

[](#fig_pixelated_parallax) plots @parallax_ctf_eq for low-order isotropic aberration coefficients, namely $C_{1,0}$ and $C_{3,0}$.
We note the following:

* Similar to HRTEM, the tcBF CTF features zero-crossings and thus contrast reversals.
This is often ameliorated using CTF "phase-flipping".
* Since the tcBF CTF shares the same zero-crossings as HRTEM, the Scherzer defocus is indeed the optimum configuration for a non-corrected microscope.

## Low-Order Approximation

Note that @gamma_factorization_eq is only satisfied if we approximate the shifted aberration surface $\chi(\bm{Q} \pm \bm{k})$ with its Taylor expansion:
:::{math}
:label: shifted_chi_taylor_eq
\chi(\bm{Q}\pm\bm{k}) = \chi(\bm{Q}) \pm \nabla \chi \cdot  \bm{k} + \frac{1}{2} \bm{k}^T H_{\chi} \bm{k} + \dots,
:::
where $H_{\chi}$ is the aberration surface Hessian.

While @gamma_factorization_eq is only strictly true for aberration surfaces linear in $\bm{k}$, note that for aberration coefficients with a quadratic $\bm{k}$ dependence, such as defocus and astigmatism, the Hessian error introduced is independent of $\bm{Q}$ and thus cancels out in the full $\Gamma(\bm{Q},\bm{k})$ expression.

:::{warning} To-Do:
Add Hessian computation for defocus, stig, and coma?
:::
