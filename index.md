---
short_title: STEM Transfer of Information
title: Iterative Ptychographic and iCOM Phase Reconstruction with Segmented and Fewer Element Array Detectors
numbering:
  heading_2: false
---

+++ {"part": "abstract"} 

Imaging beam-sensitive materials in scanning transmission electron microscopy (STEM) requires a very low electron dose to avoid damaging the sample. 
This also requires efficient electron detectors and phase retrieval techniques have shown great promise for these use-cases in recent years. 
Upon traversing the sample, the electron beam acquires phase shifts due to the magnetic and electric fields inside the sample. These phase shifts are lost upon detection since detectors only capture the absolute square of the electron wave functions. 
Using pixelated detectors to collect the full diffraction pattern for each scan position, producing a four-dimensional data set, so called 4D-STEM, these phase shifts may be retrieved through various kinds of phase retrieval techniques. 

One of the simplest methods is integrated center of mass (iCOM), which utilises the fact that the shift in the center of mass of the convergent beam electron diffraction (CBED) pattern is proportional to the gradient of the projected potential of the sample. 
Integrating this signal thus yields the projected potential of the sample. 
A different approach is to use the interference of the unscattered and scattered beams to iteratively reconstruct the object potential from the collected CBED patterns, with a technique called iterative ptychography. 

In recent years, phase retrieval techniques like these have revolutionized the sensitivity and information transfer possible with STEM. 
Still, 4D data sets are cumbersome and pixelated detectors limit the practicable scan speed due to their high read-out overhead. 
Therefore we explore the usability of these techniques with segmented detectors and lower-number pixel arrays. While iCOM is commonly used with segmented detectors, the use of iterative ptychography with such data sets is still in its infancy. 
This will allow for much higher scan speeds than 4D-STEM, and has potential to be useful also for in-situ characterisation of dynamical effects.

+++
