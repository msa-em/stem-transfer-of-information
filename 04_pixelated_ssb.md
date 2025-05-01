---
title: Direct Ptychography with a Pixelated Detector
short_title: Pixelated SSB
numbering:
  enumerator: 4.%s
label : pixelated_ssb_page
---

:::{warning} To-Do:
Add general direct ptycho intro.
:::

The regions of the CBED pattern where the first diffracted beam overlaps with the direct beam contain phase information from the interference between the two beams.
These double-overlap regions are therefore a source which may be utilized to extract the phase modulation applied on the beam electrons by the sample. 
Since the expected phase difference between the direct and the first diffracted beam is $\pi$, any phase modulation differing from that may be attributed to the sample.
Notably, the diffracted beam on both sides of the direct beam are equivalent, and only one of them should be used to retrieve the phase information, which gives rise to the name "single side-band" ptychography.
<!-- Notably, the diffracted beam at $g$ and $-g$ are equivalent, and only one of them should be used to retrieve the phase information, which gives rise to the name "single side-band" ptychography. -->

## Direct Ptychography CTF

In contrast to the detector response functions we have investigated so far, direct ptychography can utilize all the phase information in the complex-valued aperture-overlap function @ssb_gamma_eq.
This suggests that its CTF is instead given by the non-zero regions of @ssb_gamma_eq, and thus given by:

:::{math}
:label: ssb_ctf_eq
\mathcal{L}^{\mathrm{SSB}}(\bm{q}) = \frac{\mathrm{i}}{2} \int  \left|\Gamma(\bm{q},\bm{k}) \right| d\, \bm{k}.
:::

While the absolute value inside the integrand precludes a cleaner expression using correlation functions, which rely on linearity, @ssb_ctf_eq can be parallelized efficiently across spatial frequencies, $\bm{q}$.

For completeness, we note in passing that for the ideal case of $\chi(\bm{k})=0$, @ssb_ctf_eq reduces to the well-known geometric "double-minus-triple overlap" expression given by:

:::{math}
:label: geometric_ssb_ctf_eq
\mathrm{Im}\left\{\mathcal{L}^{\mathrm{ideal \, SSB}}(\bm{q})\right\} = \begin{cases} [A \star A](\bm{q}) - [A \star A](2\,\bm{q}) & if \left| \bm{q} \right| \lt q_0 \\
[A \star A](\bm{q}) & \mathrm{otherwise}
\end{cases}
:::

:::{figure} #app:pixelated_ssb
:label: fig_pixelated_ssb
:placeholder: ./figures/pixelated_ssb_placeholder.png
Effect of various probe aberrations on the CTF for SSB direct ptychography with a pixelated detector.
The resulting CTF is shown on the left panel, with its radial average in the middle panel, and its effect on example weak phase objects on the right panel.
:::

[](#fig_pixelated_ssb) plots @ssb_ctf_eq for low-order isotropic aberration coefficients, namely $C_{1,0}$ and $C_{3,0}$.
We note the following:

* The CTF tends to zero for $\bm{q} \rightarrow 0$ and $\bm{q} \rightarrow 2\, q_{\mathrm{probe}}$, peaking in between.
* The CTF is purely positive, leading to no contrast reversals with thickness / aberrations.
* Similar to iCOM, the Scherzer condition is suboptimal, since the CTF exhibits no zero-crossings.
