---
title: Conclusions
numbering:
  enumerator: 14.%s
label : conclusions
---

Phase retrieval methods play a key role in extracting useful information from diffraction intensities recorded using both pixelated and segmented detectors.
In this work we have introduced a rigorous framework for comparing the best-case scenario CTF for various experimental conditions and detector geometries.
Using this framework, we confirm some previously demonstrated observations including that iCOM needs to be performed in-focus, SSB and OBF are intimately related, and that tcBF and iterative ptychography CTFs exhibit "Thon-like" oscillations for defocused probes.
In addition, we elucidate the connection between tcBF and SSB, and utilize this to propose a novel reconstruction algorithm to enable direct ptychography with sub-sampled acquisitions.

Investigations of segmented detector CTFs confirm how the geometry of the detector is reflected in the anisotropy of the CTF, causing information along some directions to be better resolved than others.
In summary, the main observation is that more annular segments produce more isotropic CTFs, and more radial rings reduce errors arising from overestimating the detector segment COM.
Put simply, more detector elements produce CTFs closer to the fully pixelated case CTFs for all the phase methods.
Still, even with fewer detector elements it is possible to achieve high quality phase reconstructions, which simultaneously leveraging the faster scan speeds afforded by non-pixelated detectors for improved temporal resolution in STEM.

Finally, we allude to the need for evaluating the noise in reconstruction techniques on finite electron fluence acquisitions.
We introduce a robust statistical framework to evaluate this using the SSNR and demonstrate it for the previously-demonstrated case of iCOM.
The framework generalizes well to other phase retrieval techniques, and we reserve those results for future work since they do not lend themselves well to interactive explorations.
