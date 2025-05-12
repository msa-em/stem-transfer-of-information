---
title: Iterative Ptychography with a Segmented Detector
short_title: Segmented iterative ptycho
numbering:
  enumerator: 11.%s
label : segmented_ptycho_page
---

Since iterative ptychography is a flexible model-based inversion technique, we can adapt it to work on segmented detector measurements by applying a detector-binning step at the end of the forward model and similarly adapting the update step [@10.1093/mam/ozae134].
This gives us the freedom to define arbitrary detector geometries while still enjoying the flexibility of iterative ptychography, such as correcting for partial coherence using a mixed-state probe decomposition.

## Iterative Segmented Ptychography CTF

Similar to the case with a pixelated detector, the iterative nature of the technique precludes an analytical CTF expression and we proceed numerically using the white noise object introduced in @pixelated_ptycho_page.

[](#fig_segmented_iterative_ptycho) plots the numerical iterative ptychography CTF for various detector geometries.

:::{figure} #app:segmented_iterative_ptycho
:label: fig_segmented_iterative_ptycho
:placeholder: ./figures/segmented_iterative_ptycho_placeholder.png
Effect of various detector geometries and iterations on the CTF for iterative ptychography.
:::

We note the following:

- The detector geometry is reflected in the anisotropic 2D CTF at early iterations, but this is increasingly ameliorated as the reconstruction progresses.
- A small number of annular and radial segments performs poorly in the presence of probe aberrations, as fine features in the measured intensities are not properly resolved with the large effective pixel sizes.
  - This can be somewhat remedied using more annular and radial segments.
  