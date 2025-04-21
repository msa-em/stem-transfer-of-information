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
\mathcal{L}_j(\bm{Q}) = \frac{i}{2} \int A(\bm{Q}^{\prime}) D_j(\bm{Q}^{\prime}) & \left\{ A(\bm{Q}-\bm{Q}^{\prime}) \mathrm{e}^{-\mathrm{i}\left[\chi(\bm{Q} - \bm{Q}^{\prime}) - \chi(\bm{Q}^{\prime}) \right]} - \right. \\
& \left.  \; \; A(\bm{Q}+\bm{Q}^{\prime}) \mathrm{e}^{\mathrm{i}\left[\chi(\bm{Q} + \bm{Q}^{\prime}) - \chi(\bm{Q}^{\prime}) \right]} \right\} d\bm{Q}^{\prime},
\end{aligned}
:::
where $A(\bm{Q})$ is the probe-forming aperture and $\chi(\bm{Q})$ is the aberration surface.
$A(\bm{Q})$ is a top-hat function normalized such that $\int A(\bm{Q})\, d\bm{Q} = 1$, and
:::{math}
:label: chi_eq
\chi(q,\theta) = \frac{2\pi}{\lambda} \sum_{n,m} \frac{1}{n+1} C_{n,m}(q \lambda)^{n+1} \, \cos \left[m (\theta - \theta_{n,m}) \right],
:::
where $q=\left| \bm{Q}\right|$, $\theta = \arctan(\bm{Q})$, $\lambda$ is the electron wavelength, $n$ and $m$ are the radial and azimuthal orders of the aberration coefficients $C_{n,m}$, and $\theta_{n,m}$ is the aberration axis of non-isotropic coefficients.

## Aperture autocorrelation widget

It is instructive to explore [](#complex_ctf_eq) for the ideal case of no aberrations, $\chi(\bm{Q})=0$, a pixelated detector sampled at Nyquist, $D_j(\bm{Q}) = \delta(\bm{Q})$, and a circular probe-forming aperture with convergence semiangle $q_0$ defined by:
:::{math}
:label: probe_forming_aperture_eq
A(\bm{Q}) = \begin{cases}
1 & \mathrm{if} \quad \left|\bm{Q}\right| \lt q_0 \\
0 & \mathrm{otherwise}
\end{cases}
:::

In this case, [](#complex_ctf_eq) reduces to the aperture auto-correlation function, which can be expressed compactly using Fourier transforms:
:::{math}
:label: aperture_autocorrelation_eq
\left[A \star A\right](\bm{Q})  =  \Re\left\{
  \mathcal{F}_{\bm{r} \rightarrow \bm{Q}}^{-1} \left[ \left| \mathcal{F}_{\bm{Q} \rightarrow \bm{r}} \left[ A(\bm{Q}) \right] \right|^2 \right]
  \right\},
:::
where $ \star $ denotes cross-correlation and $\Re\left\{\cdot\right\}$ denotes the real-part of a complex-valued expression.

Intuitively, [](#aperture_autocorrelation_eq) can be interperted as the "double overlap" area between the aperture and a shifted aperture centered at $\bm{Q}$.
[](#fig_aperture_autocorrelation_widget) illustrates this interactively, as well as plot the radially-averaged aperture autocorrelation function.

:::{figure} #app:aperture_autocorrelation_widget
:label: fig_aperture_autocorrelation_widget
:placeholder: ./figures/aperture_autocorrelation_placeholder.png
Interactive figure illustrating how the aperture autocorrelation function can be interpreted as the overlap area between the aperture and an aperture shifted at a specific spatial frequency.
:::

Notice [](#aperture_autocorrelation_eq) has support up to $2 q_{\mathrm{probe}}$ and is zero beyond that.
With the exception of iterative ptychography, which we explore in-depth in [](pixelated_ptycho_page), all STEM phase-retrieval methods are limited by the aperture autocorrelation function.

## Aberration surface widget

Similarly, for axial illumination, $\bm{Q}^{\prime} = 0$, [](#complex_ctf_eq) reduces to the HRTEM CTF:
:::{math}
:label: hrtem_ctf_eq
\mathcal{L}_{\mathrm{HRTEM}}(\bm{Q}) = -\sin\left[\chi(\bm{Q})\right].
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
