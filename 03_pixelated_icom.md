---
title: Integrated Center of Mass Imaging with a Pixelated Detector
short_title: Pixelated iCOM
numbering:
  enumerator: 3.%s
label : pixelated_icom_page
---

## Center of Mass Imaging

One of the unique features of STEM over TEM phase retrieval techniques is that signal subtraction is possible, and as we will see desirable in some configurations, with a complicated detector geometry
:::{math}
:label: complex_detector_eq
D(\bm{k}) = \sum_j c_j D_j(\bm{k}),
:::
for real (possibly negative) coefficients $c_j$.
The linearity of [](#complex_ctf_eq) suggests that similarly the CTF for a complicated geometry follows the relation:
:::{math}
:label: complex_detector_ctf_eq
\mathcal{L}(\bm{Q}) = \sum_j c_j \mathcal{L}_j(\bm{Q}).
:::

One popular detector geometry utilizing signal subtraction is differential phase contrast (DPC), or more generally center-of-mass (COM) imaging.
Here, the detector function is vectorial and proportional to the position on the detector plane
:::{math}
:label: com_detector_eq
\begin{aligned}
\bm{D}(\bm{k})  &= \bm{k} \\
                &= D_x(\bm{k}) \hat{k}_x + D_y(\bm{k}) \hat{k}_y,
\end{aligned}
:::
where $\hat{k}_x$ and $\hat{k}_y$ are unit-vectors on the detector plane along the x- and y-directions respectively.

Inserting each detector component in [](#complex_ctf_eq), we obtain:
:::{math}
:label: asymmetric_correlation_ctf
\mathcal{L}_x(\bm{Q}) = 
:::

## To-Dos

- Introduce analytical iCOM CTF (complex-probe autocorrelation)
- Introduce test objects and CTF convolution
- Discuss Scherzer defocus being suboptimal for iCOM

:::{figure} #app:pixelated_icom
:label: fig_pixelated_icom
:placeholder: ./figures/pixelated_icom_placeholder.png
Effect of various probe aberrations on the CTF for iCOM imaging with a pixelated detector.
The resulting CTF is shown on the left panel, with its radial average in the middle panel, and its effect on example weak phase objects on the right panel.
:::
