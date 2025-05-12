---
title: Direct Ptychography with a Segmented Detector
short_title: Segmented SSB
numbering:
  enumerator: 8.%s
label : segmented_ssb_page
---

While traditionally, direct ptychography techniques have utilized pixelated detectors, the methods generalize well to segmented detectors [@10.1016/j.ultramic.2014.10.013].
This allows us to leverage the benefits outlined in the previous section, including faster dwell times for increased temporal resolution [@bekkevold_ultra-fast_2024].

## Analytical Segmented SSB CTF

The segmented SSB CTF can be derived analytically by binning the aperture-overlap function using the detector geometry, prior to taking its absolute value:

:::{math}
:label: segmented_ssb_ctf_eq
\mathcal{L}^{\mathrm{S-SSB}}(\bm{q}) = \frac{\mathrm{i}}{2} \sum_j \int \left| D_j (\bm{k}) \Gamma(\bm{q},\bm{k}) \right|d\, \bm{k} .
:::

@fig_segmented_ssb plots the SSB CTF for various detector geometries, highlighting how the symmetry of the detector is reflected in the symmetry of the two-dimensional CTF.

:::{figure} #app:segmented_ssb
:label: fig_segmented_ssb
:placeholder: ./figures/segmented_ssb_placeholder.png
Effect of detector geometries on the CTF for SSB direct ptychography.
The double-triple overlap regions are colloquially referred to as "trotters", due to their visual similarity with a [](wiki:Pig's_trotter).
:::

We note the following:

- As the number of radial and annular segments is increased, the aperture-overlap function or "trotters" are better sampled, yielding a more accurate CTF.
  - This is particularly important when the probe includes aberrations, as the aperture-overlap function is no longer uniform in phase.
- The detector geometry results in a highly anisotropic 2D CTF, with the CTF approaching zero near the edges of each segment.
  - Note this effect is obfuscated in the radially averaged 1D CTF.

## Noise Optimizing OBF Weights

Optimum Bright Field (OBF) STEM bears many similarities with phase-compensated SSB, and was in-fact developed specifically to optimize the signal-to-noise ratio in reconstructions using segmented detectors [@10.1016/j.ultramic.2020.113133; @10.1093/jmicro/dfae051].

This is done by using a different normalization than SSB in phase-compensating the measured aperture-overlap function, given by:

:::{math}
:label: segmented_obf_eq

\begin{aligned}
\mathcal{L}^{\mathrm{S-OBF}}(\bm{q}) &= \frac{\mathrm{i}}{2} \sum_j \int D_j (\bm{k}) A(\bm{k}) K(\bm{q})  d\, \bm{k}  \\

K(\bm{q}) &= \left( \int \frac{\left| D_j (\bm{k}^{\prime}) \Gamma(\bm{q},\bm{k}^{\prime}) \right|^2} {D_j (\bm{k}^{\prime}) A(\bm{k}^{\prime})} d\, \bm{k}^{\prime} \right)^{-1/2},
\end{aligned}
:::
where $A(\bm{k})$ is the normalized probe aperture.

Note that using the OBF weights in @fig_segmented_ssb above, results in broadening the SSB CTF, and minimizing the anisotropic influence of detector segmentation on the 2D CTF.
