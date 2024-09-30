---
title: Transfer of Information
---

In order to fairly assess the transfer of information using any detection and reconstruction technique, the object being reconstructed should be a white noise object. 
That means that it should contain phase information randomly distributed over all spatial frequencies, while also obeying real-world constraints. 
In other words, the complex object
:::{math}
:label: complex_object
O = e^{iV({\vec{r}})}
:::
must have a potential, $V({\vec{r}})$, which is real-valued in real space and has a random phase and constant amplitude in Fourier space
:::{math}
:label: potentialFT
\tilde{V}(\vec{k}) = Ae^{2\pi i\varphi({\vec{k}})}.
:::
Performing a single-slice 4D-STEM simulation on this object allows us to apply various virtual detectors and use them to reconstruct the white noise object.
The noise-normalised Fourier transform of the resulting reconstruction yields the 2D contrast transfer function of the phase retrieval technique with the specified detector. 
In [Figure 1](fig:annular_segmented_detectors) the contrast transfer function is calculated for annular virtual detectors of the geometry shown on the left.



:::{figure} #app:annular_segmented_detectors
:name: fig_annular_segmented_detectors
:width: 100%
:placeholder: ./figures/icom_ctf_placeholder.png
Contrast transfer function of iCOM with annular segmented detectors.
:::

This work is based on [@bekkevold2024ultra]. 
