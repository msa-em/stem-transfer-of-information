---
title: Tilt-Corrected Bright-Field STEM with a Segmented Detector
short_title: Segmented tcBF
numbering:
  enumerator: 9.%s
label : segmented_parallax_page
---

As we discussed in @pixelated_parallax_page, the principle of reciprocity implies that vBF images formed from individual pixels in the BF disk are equivalent to images formed under tilted planewave illumination.
In the presence of probe aberrations, these further exhibit lateral shifts.
Similarly, segmented detector images can be thought of as average shifted images formed under tilted planewave illumination, with angles corresponding to the detector angles.

## Analytical Segmented tcBF CTF

Since the tcBF technique computationally aligns these shifted vBF images to produce a sharper, coherent BF image, it is  reasonable to expect that tcBF will work similarly using vBF images formed from segmented detectors, albeit at the cost of some partial coherence.
This also serves to increase the signal-to-noise ratio in individual vBF images, improving the computational alignment [@10.48550/arXiv.2309.05250].

The segmented tcBF CTF can be derived analytically by binning the shift-decoupled aperture-overlap function, $\Beta(\bm{q},\bm{k})$, using the detector geometry:
:::{math}
:label: segmented_ssb_ctf_eq
\mathcal{L}^{\mathrm{S-tcBF}}(\bm{q}) = \frac{\mathrm{i}}{2} \sum_j \int D_j (\bm{k}) \Beta(\bm{q},\bm{k}) d\, \bm{k}.
:::

@fig_segmented_parallax plots the tcBF CTF for various detector geometries, highlighting how the symmetry of the detector is reflected in the symmetry of the two-dimensional CTF.

:::{figure} #app:segmented_parallax
:label: fig_segmented_parallax
:placeholder: ./figures/segmented_parallax_placeholder.png
Effect of various detector geometries on the CTF for tcBF.
:::

We note the following:

- The segmented 2D CTF similarly illustrates "Thon-ring" like oscillations [@10.1515/zna-1966-0417], albeit including imprints of the detector geometry as well.
  - As expected, the CTF approaches zero in the ideal case of no probe aberrations.
- Detector segments whose centroid lies outside the BF disk are omitted, since those better resemble dark-field images.
- The segmented CTF tends to "overshoot" the pixelated CTF since, similar to iCOM, it overestimates the center-of-mass gradient.
