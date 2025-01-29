---
short_title: Object Simulation and iCOM CTF
title: White Noise Object and iCOM Information Transfer
---

# Implementation of the white noise object
A white noise object is ideal for assessing the CTF of various phase reconstruction techniques because it contains phase information randomly distributed over all spatial frequencies.
This means that all spatial frequencies are uniformly represented in the object, such that the calculated CTF after simulation, detection, and reconstruction equally represent the transfer of all spatial frequencies. 
Importantly, the object also needs to be real in real-space, and the constant amplitude used for it should be small to obey the need for a weak phase object. 
A weak phase object imposes minimal modulation to the amplitude of the transmitted electron wavefunction, meaning that the object itself has a low scattering power. 
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
Because we decide that this white noise object is a weak phase object, a single-slice 4D-STEM simulation is sufficient. 
Performing a single-slice 4D-STEM simulation on this object allows us to apply various virtual detectors and use them to reconstruct the white noise object.
The FFT of the resulting reconstruction yields the 2D CTF of the phase retrieval technique with the specified detector. 
In [](#fig:annular_segmented_detectors) we calculate the CTF and the noise-normalised CTF (SNR) for iCOM phase reconstruction with an annular virtual detector of the geometry shown on the left.


:::{figure} #app:annular_segmented_detectors
:label: fig:annular_segmented_detectors
:placeholder: ./figures/icom_ctf_placeholder.png
Contrast transfer function of iCOM with annular segmented detectors.
:::

# Integrated Center of Mass Information Transfer
The shift in the center of mass (COM) of the convergent beam electron diffraction (CBED) pattern is proportional to the gradient of the phase shift which the STEM beam acquired by passing through the sample [@dekkers_differential_1974;@rose_nonstandard_1977].
These phase shifts are acquired due to the prescence of electric and magnetic fields inside the sample, and is given by
:::{math}
:label: phase_shift
\phi(\vec{r}_\perp) & = \phi_e(\vec{r}_\perp) + \phi_m(\vec{r}_\perp) \\
& = \frac{e}{\hbar v} \int_L V(\vec{r}_\perp, z) dz - \frac{e}{\hbar} \int_L \vec{A}(\vec{r}_\perp,z) \cdot d\vec{r}
:::
where $\phi_e(\vec{r}_\perp)$ denotes the electric field contribution and $\phi_m(\vec{r}_\perp)$ denotes the contribution from any magnetic fields present.
Thus, the COM signal is proportional to the projected electric and magnetic fields of the sample.
As a result, we may integrate this signal to obtain the estimated projected potential of the sample in the integrated COM (iCOM) signal [@lazic_phase_2016].

Since the iCOM signal originates from the shift of the CBED, and shifts further than $\alpha$ are not detectable, the information transfer for iCOM is limited by the auto-correlation of the probe with itself. 
This can be seen as the solid black line in the radially averaged CTF in [](#fig:annular_segmented_detectors), which tapers off to zero at $2\alpha$.
<!-- Using a pixelated detector to estimate the COM shifts will approach this best-case CTF. -->
Using an annular segmented detector to estimate the COM shifts will introduce artefacts in the CTF and reduce the achievable information transfer.
For example, the CTF for an annular detector with four segments will have a four-fold symmetry due to the detector geometry. 
This symmetry is reflected in the reconstructed image causing atomic columns to appear slightly square rather than the expected round shape. 
Importantly, this is an artefact of the detection and reconstruction setup -- not a feature of the sample itself.
This becomes obvious when using the white noise object known to have a uniformly random Fourier phase and constant Fourier amplitude for the reconstruction.


An observation that can be made through investigating the iCOM CTF is that experiments intending to use this phase retrieval method should always be done in-focus. 
Changing the defocus condition away from $\Delta f = 0$ will always degrade the information transfer, and may even lead to contrast inversions as has been extensively reported in the literature [@burger_influence_2020;@seifer_flexible_2021;@li_integrated_2022;@liang_optimizing_2023].
Naturally, the zero defocus condition may easily be upheld for the simulation of a thin sample while experimentally determining the zero defous condition for a finite thickness sample need not be trivial.
Additionally, the thicker the sample is the more likely it is that the weak phase object approximation does not hold and iCOM is a less adequate characterisation method for the sample. 


One property of iCOM phase reconstruction that is important to note is that since the COM is estimated using the intensity collected in a segment multiplied by the center of mass of the segment itself, the COM shift may be grossly overestimated by extending the outer collection angle beyond $\alpha$.
This can cause the radially averaged CTF to soar above unity, seemingly exceeding the best-case limit information transfer for iCOM. 

This work is based on [@bekkevold_ultra-fast_2024].
