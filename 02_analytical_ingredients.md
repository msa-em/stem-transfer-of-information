---
title: Analytical Framework for Contrast Transfer Functions in STEM Measurements
short_title: Analytical CTF Framework
numbering:
  enumerator: 2.%s
label : analytical_framework_page
---

## Contrast Transfer Function Ingredients

For STEM measurements, the complex-valued CTF function, introduced in the [](stem_image_formation) and [](stem_ctf) sections, takes the form [@https://doi.org/chsgqd ; @https://doi.org/phzz]:

:::{math}
:label: complex_ctf_eq
\begin{aligned}
\mathcal{L}_j(\bm{Q}) = \frac{i}{2} \int A(\bm{k}) D_j(\bm{k}) & \left\{ A(\bm{Q}-\bm{k}) \mathrm{e}^{-\mathrm{i}\left[\chi(\bm{Q} - \bm{k}) - \chi(\bm{k}) \right]} - \right. \\
& \left.  \; \; A(\bm{Q}+\bm{k}) \mathrm{e}^{\mathrm{i}\left[\chi(\bm{Q} + \bm{k}) - \chi(\bm{k}) \right]} \right\} d\bm{k},
\end{aligned}
:::
where $A(\bm{k})$ is the probe-forming aperture and $\chi(\bm{k})$ is the aberration surface.
$A(\bm{k})$ is a top-hat function normalized such that $\int A(\bm{k})\, d\bm{k} = 1$, and
:::{math}
:label: chi_eq
\chi(k,\theta) = \frac{2\pi}{\lambda} \sum_{n,m} \frac{1}{n+1} C_{n,m}(k \lambda)^{n+1} \, \cos \left[m (\theta - \theta_{n,m}) \right],
:::
where $k=\left| \bm{k}\right|$, $\theta = \arctan(\bm{k})$, $\lambda$ is the electron wavelength, $n$ and $m$ are the radial and azimuthal orders of the aberration coefficients $C_{n,m}$, and $\theta_{n,m}$ is the aberration axis of non-isotropic coefficients.

Equation [](#complex_ctf_eq) can be expressed more compactly using symmetric and asymmetric weighted cross-correlations of the complex-valued wavefunction $\psi(\bm{k}) = A(\bm{k})\mathrm{e}^{-\mathrm{i} \chi(\bm{k})}$ with the detector function:

:::{math}
:label: symmetric_asymmetric_correlations_eq
\begin{aligned}
\Re\left\{\mathcal{L}_j(\bm{Q})\right\} & = \frac{1}{2} \Bigl\{ \left[\psi \star \psi \, D_j \right](\bm{Q}) + \left[\psi \, D_j \star \psi \right](\bm{Q}) \Bigr\} \\
\Im\left\{\mathcal{L}_j(\bm{Q})\right\} & = \frac{1}{2} \Bigl\{ \left[\psi \star \psi \, D_j \right](\bm{Q}) - \left[\psi \, D_j \star \psi \right](\bm{Q}) \Bigr\},
\end{aligned}
:::
where $ \star $ denotes cross-correlation and $\Re\left\{\cdot\right\}$, $\Im\left\{\cdot\right\}$ denote the real and imaginary parts of complex-valued expressions respectively.

## Aperture Autocorrelation

It is instructive to explore @complex_ctf_eq and @symmetric_asymmetric_correlations_eq for the ideal case of no aberrations, $\chi(\bm{k})=0$, a pixelated detector sampled at Nyquist, $D_j(\bm{k}) = \delta(\bm{k})$, and a circular probe-forming aperture with convergence semiangle $k_0$ defined by:
:::{math}
:label: probe_forming_aperture_eq
A(\bm{k}) = \begin{cases}
1 & \mathrm{if} \quad \left|\bm{k}\right| \lt k_0 \\
0 & \mathrm{otherwise}
\end{cases}
:::

In this case @symmetric_asymmetric_correlations_eq reduces to the aperture auto-correlation function:
:::{math}
:label: aperture_autocorrelation_eq
\Im\left\{\mathcal{L}^{\mathrm{ideal}}(\bm{Q})\right\} = \left[A \star A\right](\bm{k})  =  \Re\left\{
  \mathcal{F}_{\bm{r} \rightarrow \bm{k}}^{-1} \left[ \left| \mathcal{F}_{\bm{k} \rightarrow \bm{r}} \left[ A(\bm{k}) \right] \right|^2 \right]
  \right\}.
:::

Intuitively, [](#aperture_autocorrelation_eq) can be interperted as the "double overlap" area between the aperture and a shifted aperture centered at $\bm{k}$.
[](#fig_aperture_autocorrelation_widget) illustrates this interactively, as well as plot the radially-averaged aperture autocorrelation function.

:::{figure} #app:aperture_autocorrelation_widget
:label: fig_aperture_autocorrelation_widget
:placeholder: ./figures/aperture_autocorrelation_placeholder.png
Interactive figure illustrating how the aperture autocorrelation function can be interpreted as the overlap area between the aperture and an aperture shifted at a specific spatial frequency.
:::

Notice [](#aperture_autocorrelation_eq) has support up to $2 q_{\mathrm{probe}}$ and is zero beyond that.
With the exception of iterative ptychography, which we explore in-depth in [](pixelated_ptycho_page), all STEM phase-retrieval methods are limited by the aperture autocorrelation function.

## Aberration Surface

Similarly, for axial illumination, $\bm{k} = 0$, [](#complex_ctf_eq) reduces to the HRTEM CTF:
:::{math}
:label: hrtem_ctf_eq
\Im\left\{\mathcal{L}^{\mathrm{axial}}(\bm{Q})\right\} = -\sin\left[\chi(\bm{Q})\right].
:::

:::{figure} #app:aberration_surface_widget
:label: fig_aberration_surface_widget
:placeholder: ./figures/aberrations_surface_placeholder.png
Interactive figure showing the aberration surface for common low-order aberrations.
:::

[](#fig_aberration_surface_widget) plots [](#hrtem_ctf_eq) for common low-order coefficients, as well as provide the functionality to balance spherical aberration using the Scherzer defocus:
:::{math}
:label: scherzer_defocus_eq
C_{1,0}^{\mathrm{sch.}} = \mathrm{sgn}\left\{C_{3,0}\right\} \sqrt{\frac{3}{2} \left| C_{3,0}\right| \lambda },
:::
where $\mathrm{sgn}\left\{\cdot\right\}$ denotes the sign of a real number.
