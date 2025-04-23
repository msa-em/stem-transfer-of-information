---
title: Integrated Center of Mass Imaging with a Pixelated Detector
short_title: Pixelated iCOM
numbering:
  enumerator: 3.%s
label : pixelated_icom_page
---

One of the unique features of STEM over TEM phase retrieval techniques is that signal subtraction is possible, and as we will see desirable in some configurations.
For a complicated detector geometry
:::{math}
:label: complex_detector_eq
D(\bm{k}) = \sum_j c_j D_j(\bm{k}),
:::
for real (possibly negative) coefficients $c_j$, the linearity of [](#complex_ctf_eq) suggests that the CTF for a complicated geometry follows the relation:
:::{math}
:label: complex_detector_ctf_eq
\mathcal{L}(\bm{Q}) = \sum_j c_j \mathcal{L}_j(\bm{Q}).
:::

## Center of Mass Imaging

:::{warning} To-Do:
Add general COM intro.
:::

One popular detector geometry utilizing signal subtraction is differential phase contrast (DPC), or more generally center-of-mass (COM) imaging.
Here, the detector function is vectorial and proportional to the position on the detector plane
:::{math}
:label: com_detector_eq
\begin{aligned}
\bm{D}(\bm{k})  &= \bm{k} \\
                &= k_x(\bm{k}) \hat{k}_x + k_y(\bm{k}) \hat{k}_y,
\end{aligned}
:::
where $\hat{k}_x$ and $\hat{k}_y$ are unit-vectors on the detector plane along the x- and y-directions respectively.

Inserting the COM detector components in [](#symmetric_asymmetric_correlations_eq), we obtain the following CTFs:
:::{math}
:label: asymmetric_correlation_ctf
\begin{aligned}
\mathcal{L}_x^{\mathrm{COM}}(\bm{Q}) &= \left[\psi \star \psi \, Q_x \right](\bm{Q}) - \left[\psi \, Q_x \star \psi \right](\bm{Q}) \\
\mathcal{L}_y^{\mathrm{COM}}(\bm{Q}) &= \left[\psi \star \psi \, Q_y \right](\bm{Q}) - \left[\psi \, Q_y \star \psi \right](\bm{Q}).
\end{aligned}
:::

:::{figure} #app:pixelated_icom_static
:label: fig_pixelated_icom_static
Center of mass imaging component CTFs, and how they combine to give the scalar iCOM CTF, for an in-focus probe.
:::

## Integrated Center of Mass Imaging

Following @complex_detector_ctf_eq, the vectorial CTF in @asymmetric_correlation_ctf can be combined to form a scalar CTF using the usual Fourier-integration method of obtain the integrated COM (iCOM) [@10.1016/bs.aiep.2017.01.006]:
:::{math}
:label: icom_ctf_eq
\mathcal{L}^{\mathrm{iCOM}}(\bm{Q}) = \frac{Q_x \,  \mathcal{L}_x^{\mathrm{COM}}(\bm{Q}) + Q_y \,  \mathcal{L}_y^{\mathrm{COM}}(\bm{Q})}{\mathrm{i} \left|Q\right|^2}.
:::

Note that this reduces to the much simpler complex-probe auto-correlation expression:
:::{math}
:label: icom_ctf_autocorrelation_eq
\Im\left\{\mathcal{L}^{\mathrm{iCOM}}(\bm{Q})\right\} = \left[\psi \star \psi \right](\bm{Q}).
:::

:::{figure} #app:pixelated_icom
:label: fig_pixelated_icom
:placeholder: ./figures/pixelated_icom_placeholder.png
Effect of various probe aberrations on the CTF for iCOM imaging with a pixelated detector.
The resulting CTF is shown on the left panel, with its radial average in the middle panel, and its effect on example weak phase objects on the right panel.
:::

[](#fig_pixelated_icom) plots @icom_ctf_autocorrelation_eq for the lowest-order isotropic aberrations.

Note that the CTF degrades quickly with increasing aberrations, hence iCOM is traditionally performed in-focus, and that the Scherzer defocus is not in-fact optimal for a specific chromatic aberration.
This is not surprising, since the CTF does not exhibit the same zero-crossings as the HRTEM CTF.

The right-most panel utilizes the linearity of the WPOA to convolve the resulting CTF with three sample potentials at various length-scales: i) a strontium titanate (STO) sample, ii) a metal-organic framework sample, and iii) an apoferritin protein sample.
Note that at large defocii, the CTF can exhibit contrast reversals.

Finally, it is interesting to note that analytical iCOM CTF suggests that the direct-component (DC) frequency is recovered exactly.
This is incorrect, since only holographic techniques can recover the absolute phase of a sample, and highglights the main limitation of CTF analysis -- namely that it completely neglects finite electron fluence and Poisson-limited detector measurements.
We remedy this point in [](#ssnr_page) where we introduce the spectral signal-to-noise (SSNR) statistical framework.
