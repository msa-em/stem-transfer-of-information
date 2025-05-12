---
title: Integrated Center of Mass Imaging with a Segmented Detector
short_title: Segmented iCOM
numbering:
  enumerator: 8.%s
label : segmented_icom_page
---

One of the simplest ways to use the signal from a classical four-segmented detector is estimating the COM of the BF disk by subtracting opposing detector segments.
It was shown over a decade ago that this enables imaging of single atomic columns [@10.1038/nphys2337].
However, segmented detectors of other geometries may be realized as well, and the CTF framework lends itself well to investigating the information transfer dependency on the detector geometry.

## Analytical Segmented COM CTF

In @pixelated_icom_page, we saw that the analytical CTF for iCOM with a pixelated detector is the autocorrelation of the complex probe, since the pixelated detector function $D_j(\bm{k}) =\delta(\bm{k})$ covers every pixel in the detector as seen in @com_detector_eq.
However, for a segmented detector, the detector function for the $j^{\mathrm{th}}$ segment is given by:
:::{math}
:label: segmented_detector_eq
D_j(\bm{k}) =
\begin{cases}
1, & \text{for }\bm{k}\text{ inside detector segment }j \\
0, & \text{elsewhere}
\end{cases}
:::

The combined vectorial detector function is then given by:
:::{math}
:label: segmented_vectorial_detector_eq
\bm{D}(\bm{k}) = \sum_j k_x(\bm{k})D_j(\bm{k}) \hat{k}_x + \sum_j k_y(\bm{k})D_j(\bm{k}) \hat{k}_y,
:::

with the analytical segmented COM CTFs obtained by:
:::{math}
:label: segmented_com_ctf_eq
\begin{aligned}
\mathcal{L}^{\mathrm{S-COM}}_x(\bm{q}) &= \left[\psi \star \psi \, D_x \right](\bm{q}) - \left[\psi \, D_x \star \psi \right](\bm{q}) \\
\mathcal{L}^{\mathrm{S-COM}}_y(\bm{q}) &= \left[\psi \star \psi \, D_y \right](\bm{q}) - \left[\psi \, D_y \star \psi \right](\bm{q})
\end{aligned}
:::

## Detector Segmentation iCOM CTF

The iCOM CTF is then obtained from @segmented_com_ctf_eq using the same Fourier-integration technique given by @icom_ctf_eq.
@fig_segmented_icom plots the iCOM CTF for various detector geometries, highlighting how the symmetry of the detector is reflected in the symmetry of the two-dimensional CTF.

:::{figure} #app:segmented_icom
:label: fig_segmented_icom
:placeholder: ./figures/segmented_icom_placeholder.png
Effect of various detector geometries on the CTF for iCOM imaging.
:::

We note the following:

- As the number of annular and radial segments increases, the iCOM CTF approaches that of the pixelated detector.
  - Similarly to pixelated iCOM, the CTF degrades quickly with increasing defocus. The effect is even more pronounced with large, few detector elements.
- Since the CTF relies on the center of mass of detector segment $j$, the outer collection angle of an annular detector should match the semi-convergence angle, $\alpha$, for the COM approximation to be accurate.
  - An outer collection angle $\gg q_{\mathrm{probe}}$ results in over-estimation of the COM signal, and thus produces a CTF above unity.
- This effect may be somewhat remedied by introducing radial rings which allows the detector to resolve the COM signal radially in addition to annularly.
- For detectors with few annular segments, the 2D CTF is anisotropic, resulting in non-round atoms when convolved with the STO WPO.
- The rotational-offset of the annular segments is reflected in the 2D CTF orientation.
  - Note this effect is obfuscated in the commonly-presented 1D radial averages.
- Offsetting half of the ring's segments by half of their annular span range (e.g. $45^\circ$ for four segments spanning $90^\circ$ each) further improves annular resolution, yielding a more isotropic CTF.
