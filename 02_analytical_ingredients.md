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
& \left.  \; A(\bm{Q}+\bm{Q}^{\prime}) \mathrm{e}^{\mathrm{i}\left[\chi(\bm{Q} + \bm{Q}^{\prime}) - \chi(\bm{Q}^{\prime}) \right]} \right\} d\bm{Q}^{\prime},
\end{aligned}
:::
where $A(\bm{Q})$ is the probe-forming aperture and $\chi(\bm{Q})$ is the aberration surface.
$A(\bm{Q})$ is a top-hat function normalized such that $\int A(\bm{Q})\, d\bm{Q} = 1$, and
:::{math}
:label:
\chi(q,\theta) = \frac{2\pi}{\lambda} \sum_{n,m} \frac{1}{n+1} C_{n,m}(q \lambda)^{n+1} \, \cos \left[m (\theta - \theta_{n,m}) \right],
:::
where $q=\left| \bm{Q}\right|$, $\theta = \arctan(\bm{Q})$, $\lambda$ is the electron wavelength, $n$ and $m$ are the radial and azimuthal orders of the aberration coefficients $C_{n,m}$, and $\theta_{n,m}$ is the aberration axis of non-isotropic coefficients.

## Aperture autocorrelation widget

:::{figure} #app:aperture_autocorrelation_widget
:label: fig_aperture_autocorrelation_widget
:placeholder: ./figures/aperture_autocorrelation_placeholder.png
Interactive figure illustrating how the aperture autocorrelation function can be interpreted as the overlap area between the aperture and an aperture shifted at a specific spatial frequency.
:::

## Aberration surface widget

:::{figure} #app:aberration_surface_widget
:label: fig_aberration_surface_widget
:placeholder: ./figures/aberrations_surface_placeholder.png
Interactive figure showing the aberration surface for common low-order aberrations.
:::
