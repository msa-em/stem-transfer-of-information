---
title: Tilt-Corrected Bright-Field STEM with a Pixelated Detector
short_title: Pixelated tcBF
numbering:
  enumerator: 5.%s
label : pixelated_parallax_page
---

:::{warning} To-Do:
Add general parallax intro.
:::

A pixelated detector images the entire CBED pattern at every scan position, and thus the sum over all the detector pixels gives the BF image.
Similarly, a sum of only a subset of the pixels inside the BF disk yields an incoherent BF image, similar to a monolithic BF or ABF detector. 
Further, this is also true on a single pixel level, with the caveat that pixels outside the optic axis produce a shifted BF image in real space.
This is equivalent to a TEM image with tilted illumination by the principle of reciprocity. 
In tilt-corrected BF STEM, this is utilized by computationally aligning all of the tilted BF images back into one aligned BF image.
By doing so, each virtual BF image is aligned to the optic axis and their mean now gives a much sharper, coherent BF image. 

## Tilt-Corrected BF STEM CTF

The tilt-corrected BF STEM CTF can be understood by starting with the complex-valued aperture overlap function @ssb_gamma_eq, reproduced here for convenience:
:::{math}
:label: gamma_aperture_chi_eq
\Gamma(\bm{q},\bm{k}) = A(\bm{k})A(\bm{q}-\bm{k})\mathrm{e}^{-\mathrm{i}\chi(\bm{q}-\bm{k})}\mathrm{e}^{\mathrm{i}\chi(\bm{k})} - A(\bm{k})A(\bm{q}+\bm{k})\mathrm{e}^{\mathrm{i}\chi(\bm{q}+\bm{k})}\mathrm{e}^{-\mathrm{i}\chi(\bm{k})}.
:::

<!-- To proceed, we wish to factorize @gamma_aperture_chi_eq to read: -->
To proceed, we wish to factorize out the part containing the shifts needed to align the tilted BF images from @gamma_aperture_chi_eq.
The remaining terms we collect into a function $\Beta(\bm{q},\bm{k})$ such that we get
:::{math}
:label: gamma_factorization_eq
\begin{aligned}
\Gamma(\bm{q},\bm{k}) &\approx \Beta(\bm{q},\bm{k}) \mathrm{e}^{\mathrm{i}\nabla\chi \cdot \bm{k}} \\
\Beta(\bm{q},\bm{k}) &= A(\bm{k})\left(A(\bm{q}-\bm{k})\mathrm{e}^{-\mathrm{i}\chi(\bm{q})} - A(\bm{q}+\bm{k})\mathrm{e}^{\mathrm{i}\chi(\bm{q})}\right).
\end{aligned}
:::
<!-- where the term involving the gradient of the aberration surface, $\nabla \chi$, is a phase ramp corresponding to the lateral shifts observed in tcBF measurements. -->
Here, the term involving the gradient of the aberration surface, $\nabla \chi$, is the tilt-correction term.
Essentially, this is a phase ramp corresponding to the lateral shifts observed in tcBF measurements.
Since this tilt-correction term is ... it does not contribute to the CTF.

The tcBF CTF is then obtained by summing $\Beta(\bm{q},\bm{k})$ over $\bm{k}$:
:::{math}
:label: parallax_ctf_eq
\begin{aligned}
\mathrm{Im}\left\{\mathcal{L}^{tcBF}(\bm{q})\right\}  &= \int \Beta(\bm{q},\bm{k}) d\, \bm{k} \\
                                              &= -\left[A \star A\right](\bm{q}) \sin\left[\chi(\bm{q})\right],
\end{aligned}
:::
which we recognize as the axial CTF modulated by the aperture auto-correlation envelope.

:::{figure} #app:pixelated_parallax
:label: fig_pixelated_parallax
:placeholder: ./figures/pixelated_parallax_placeholder.png
Effect of various probe aberrations on the CTF for tcBF with a pixelated detector.
The resulting CTF is shown on the left panel, with its radial average in the middle panel, and its effect on example weak phase objects on the right panel.
:::

[](#fig_pixelated_parallax) plots @parallax_ctf_eq for low-order isotropic aberration coefficients, namely $C_{1,0}$ and $C_{3,0}$.
We note the following:

* Similar to HRTEM, the tcBF CTF features zero-crossings and thus contrast reversals.
This is often ameliorated using CTF "phase-flipping".
* Since the tcBF CTF shares the same zero-crossings as HRTEM, the Scherzer defocus is indeed the optimum configuration for an uncorrected microscope.

## Low-Order Approximation

Equation @gamma_factorization_eq is only satisfied if we approximate the shifted aberration surface $\chi(\bm{q} \pm \bm{k})$ with the first-order term of its Taylor expansion:
:::{math}
:label: shifted_chi_taylor_eq
\chi(\bm{q}\pm\bm{k}) = \chi(\bm{q}) \pm \nabla \chi(\bm{q})^T \cdot  \bm{k} + \frac{1}{2} \bm{k}^T \cdot H_{\chi}(\bm{q}) \cdot \bm{k} + \dots,
:::
where $H_{\chi}(\bm{q})$ is the Hessian of the aberration surface.

Truncating @shifted_chi_taylor_eq after the gradient term yields an exact result when the aberration phase function $\chi(\bm{q})$ is quadratic in $\bm{q}$.
This includes terms such as defocus and astigmatism, which are proportional to $q^2$, $q_x^2 - q_y^2$, and $2q_x q_y$.
For such quadratic forms, the Hessian is constant and the second-order error term becomes independent of $\bm{q}$, contributing only a global, physically irrelevant phase shift in @gamma_factorization_eq.
However, for higher-order aberration coefficients, such as coma and spherical aberration, @gamma_factorization_eq introduces non-trivial approximation errors which scale with $\bm{q}$ and increase for larger $\bm{k}$ support, reflecting the non-linear curvature of the aberration surface.

:::{table}
:label: hessian_error_table
:align: center

Table summarizing the gradient, Hessian, and Hessian-induced error terms for common low-order aberration coefficients.
Non-isotropic coefficients are expressed in Cartesian coordinates, and overall prefactors (e.g. $\pi \lambda$) have been omitted for clarity.

| Coefficient | $ \chi(\bm{q}) $ | $ \nabla \chi(\bm{q})^T $ | $H_{\chi} (\bm{q})$ | Hessian-induced error |
| :---: | :---: | :----: | :----: | :----: |
| $C_{1,0}$ | $q^2$ | $\begin{bmatrix} 2q_x \\ 2q_y \end{bmatrix}$ | $\begin{bmatrix} 2 & 0 \\ 0 & 2 \end{bmatrix}$ | $k_x^2 + k_y^2$ |
| $C_{1,2}^x$ | $q_x^2 - q_y^2$ | $\begin{bmatrix} 2q_x \\ -2q_y \end{bmatrix}$ | $\begin{bmatrix} 2 & 0 \\ 0 & -2 \end{bmatrix}$ | $k_x^2 - k_y^2$ |
| $C_{1,2}^y$ | $2q_x q_y$ | $\begin{bmatrix} 2q_y \\ 2q_x \end{bmatrix}$ | $\begin{bmatrix} 0 & 2 \\ 2 & 0 \end{bmatrix}$ | $2k_x k_y$ |
| $C_{2,1}^x$ | $q^2 q_x$ | $\begin{bmatrix} 3q_x^2 + q_y^2 \\ 2q_x q_y \end{bmatrix}$ | $\begin{bmatrix} \frac{6q_x^2 + q_y^2}{q} & \frac{3q_x q_y}{q} \\ \frac{3q_x q_y}{q} & \frac{q_x^2}{q} \end{bmatrix}$ | $\frac{q_x}{q}(k_x^2 + k_y^2) + 2\frac{q_y}{q}k_x k_y$ |
| $C_{2,1}^y$ | $q^2 q_y$ | $\begin{bmatrix} 2q_x q_y \\ q_x^2 + 3q_y^2 \end{bmatrix}$ | $\begin{bmatrix} \frac{q_y^2}{q} & \frac{3q_x q_y}{q} \\ \frac{3q_x q_y}{q} & \frac{q_x^2 + 6q_y^2}{q} \end{bmatrix}$ | $\frac{q_y}{q}(k_x^2 + k_y^2) + 2\frac{q_x}{q}k_x k_y$ |
| $C_{3,0}$ | $q^4$ | $\begin{bmatrix} 4q^2 q_x \\ 4q^2 q_y \end{bmatrix}$ | $\begin{bmatrix} 4(q^2 + 2q_x^2) & 8q_x q_y \\ 8q_x q_y & 4(q^2 + 2q_y^2) \end{bmatrix}$ | $q^2(k_x^2 + k_y^2) + 2(q_x k_x + q_y k_y)^2$ |

:::
