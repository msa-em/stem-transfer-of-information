---
title: Analytical Framework for Contrast Transfer Functions in STEM Measurements
short_title: Analytical CTF Framework
numbering:
  enumerator: 2.%s
label : analytical_framework_page
---

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

In general, the relationship between [](#probability-density-eq) and the sample phase is non-linear.
Weak-phase objects only scatter the incoming illumination weakly, and can thus be well approximated using the leading terms of the Taylor expansion,
:::{math}
:label: weak-phase-taylor-exp-eq
T(\bm{r}) = \exp\left[\mathrm{i}\,\phi(\bm{r})\right] \approx 1 + \mathrm{i}\, \phi(\bm{r}).
:::

In this case, the image formation theory described above becomes linear, and the image contrast is proportional to the sample phase.
This is most commonly expressed in terms of the intensity Fourier transform, $\tilde{I}_{j,\bm{q}^{\prime}} = \mathcal{F}_{\bm{r}^{\prime} \rightarrow \bm{q}^{\prime}}\left[ I_{j,\bm{r}^{\prime}} \right]$, as a function of spatial frequency, $\bm{q}^{\prime}$:

:::{math}
:label: ctf-eq
\tilde{I}_{j,\bm{q}^{\prime}} = 2\, \tilde{\phi}(\bm{q}^{\prime}) \times \mathcal{L}_j(\bm{q}^{\prime}),
:::
where $\mathcal{L}_j(\bm{q}^{\prime})$ is the complex-valued contrast transfer function (CTF), which is sample-independent and depends on the properties of the imaging system, such as the incoming illumination aperture and aberrations, the detector geometry, and the reconstruction method.

## Contrast Transfer Functions

For STEM measurements, the complex-valued CTF function takes the form [@https://doi.org/chsgqd]:

:::{math}
:label: complex_ctf_eq
\begin{aligned}
\mathcal{L}_j(\bm{q}) = \frac{i}{2} \int A(\bm{k}) D_j(\bm{k}) & \left\{ A(\bm{q}-\bm{k}) \mathrm{e}^{-\mathrm{i}\left[\chi(\bm{q} - \bm{k}) - \chi(\bm{k}) \right]} - \right. \\
& \left.  \; \; A(\bm{q}+\bm{k}) \mathrm{e}^{\mathrm{i}\left[\chi(\bm{q} + \bm{k}) - \chi(\bm{k}) \right]} \right\} d\bm{k},
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
\mathrm{Re}\left\{\mathcal{L}_j(\bm{q})\right\} & = \frac{1}{2} \Bigl\{ \left[\psi \star \psi \, D_j \right](\bm{q}) + \left[\psi \, D_j \star \psi \right](\bm{q}) \Bigr\} \\
\mathrm{Im}\left\{\mathcal{L}_j(\bm{q})\right\} & = \frac{1}{2} \Bigl\{ \left[\psi \star \psi \, D_j \right](\bm{q}) - \left[\psi \, D_j \star \psi \right](\bm{q}) \Bigr\},
\end{aligned}
:::
where $ \star $ denotes cross-correlation and $\mathrm{Re}\left\{\cdot\right\}$, $\mathrm{Im}\left\{\cdot\right\}$ denote the real and imaginary parts of complex-valued expressions respectively.

For a pixelated detector sampled at Nyquist, $D_j(\bm{k}) = \delta(\bm{k})$, the integrand of @complex_ctf_eq reduces to:
:::{math}
:label: ssb_gamma_eq
\Gamma_{\psi}(\bm{q},\bm{k}) =  \psi^{\ast}(\bm{k}) \psi(\bm{q}-\bm{k}) - \psi(\bm{k}) \psi^{\ast}(\bm{q}+\bm{k}),
:::
which is known as the spatial-frequency dependent aperture-overlap function and encodes the phase interference between the first order diffracted beams and the direct beam [@10.1016/j.ultramic.2016.09.002].

### Aperture Autocorrelation

It is instructive to explore @complex_ctf_eq - @ssb_gamma_eq for the ideal case of no aberrations, $\chi(\bm{k})=0$, and a circular probe-forming aperture with convergence semiangle $k_0$ defined by:
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
\mathrm{Im}\left\{\mathcal{L}^{\mathrm{ideal}}(\bm{q})\right\} = \left[A \star A\right](\bm{k})  =  \mathrm{Re}\left\{
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
With the exception of iterative ptychography, which we explore in-depth in [](#pixelated_ptycho_page), all STEM phase-retrieval methods are limited by the aperture autocorrelation function.

### Aberration Surface

Similarly, for axial illumination, $\bm{k} = 0$, [](#complex_ctf_eq) reduces to the HRTEM CTF:
:::{math}
:label: hrtem_ctf_eq
\mathrm{Im}\left\{\mathcal{L}^{\mathrm{axial}}(\bm{q})\right\} = -\sin\left[\chi(\bm{q})\right].
:::

[](#fig_aberration_surface_widget) plots [](#hrtem_ctf_eq) for common low-order coefficients, as well as provide the functionality to balance spherical aberration using the Scherzer defocus:
:::{math}
:label: scherzer_defocus_eq
C_{1,0}^{\mathrm{sch.}} = \mathrm{sgn}\left\{C_{3,0}\right\} \sqrt{\frac{3}{2} \left| C_{3,0}\right| \lambda },
:::
where $\mathrm{sgn}\left\{\cdot\right\}$ denotes the sign of a real number.

:::{figure} #app:aberration_surface_widget
:label: fig_aberration_surface_widget
:placeholder: ./figures/aberrations_surface_placeholder.png
Interactive figure showing the aberration surface for common low-order aberrations.
:::
