---
title: Integrated Center of Mass Imaging with a Segmented Detector
short_title: Segmented iCOM
numbering:
  enumerator: 7.%s
label : segmented_icom_page
---

:::{warning} To-Do:

- <s>Introduce segmented detectors</s>
- Introduce analytical iCOM CTF (detector segment autocorrelation with complex-probe)
- <s>Discuss radial vs annular segments</s>
- <s>Discuss CTF > 1</s>

:::

So far we have discussed the CTF of phase retrieval techniques when detailed 2D images of the diffraction patterns are recorded with a pixelated detector.
However, pixelated detectors limit the achievable scan speed in experiments due to slow read-out times typically on the order of tens of μs [@10.1093/mictod/qaad005; @bekkevold_ultra-fast_2024].
For comparison, traditional HAADF imaging is commonly acquired with dwell times as low as $1 - 5$ μs, or even as fast as $< 100$ ns when multi-frame acquisitions are obtained to observe dynamic effects [@10.1093/jmicro/dfp052;@10.1093/jmicro/dfaa017].
To realize such sub-$10$ μs dwell times for phase retrieval techniques, we need to look to detectors with a minimal read-out overhead limiting the scan speed, which are still able to retrieve the desired phase information.
One candidate for such detectors are few-pixel segmented detectors, which are already in widespread use for both iCOM and OBF imaging.

In the following we investigate the impact of detector segmentation on the CTF of phase retrieval techniques iCOM, SSB, tcBF, and iterative ptychography, starting here with iCOM.

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
\mathcal{L}^{\mathrm{COM}}_x(\bm{q}) &= \left[\psi \star \psi \, D_x \right](\bm{q}) - \left[\psi \, D_x \star \psi \right](\bm{q}) \\
\mathcal{L}^{\mathrm{COM}}_y(\bm{q}) &= \left[\psi \star \psi \, D_y \right](\bm{q}) - \left[\psi \, D_y \star \psi \right](\bm{q})
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
- Since the CTF relies on the center of mass of detector segment $j$, the outer collection angle of an annular detector should match the semi-convergence angle, $\alpha$, for the COM approximation to be accurate.
  - An outer collection angle $\gg q_{\mathrm{probe}}$ results in over-estimation of the COM signal, and thus produces a CTF above unity.
- This effect may be somewhat remedied by introducing radial rings which allows the detector to resolve the COM signal radially in addition to annularly.
- For detectors with few annular segments, the 2D CTF is anisotropic, resulting in non-round atoms when convolved with the STO WPO.
- The rotational-offset of the annular segments is reflected in the 2D CTF orientation.
  - Note this effect is obfuscated in the commonly-presented 1D radial averages.
- Offsetting half of the ring's segments by half of their annular span range (e.g. $45^\circ$ for four segments spanning $90^\circ$ each) further improves annular resolution, yielding a more isotropic CTF.
