---
short_title: Object Simulation
title: White Noise Object
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
