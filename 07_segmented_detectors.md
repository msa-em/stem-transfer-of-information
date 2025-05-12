---
title: Segmented Detectors
short_title: Segmented Detectors
numbering:
  enumerator: 7.%s
label : segmented_detectors_intro_page
---

So far we have discussed the CTF of phase retrieval techniques when detailed 2D images of the diffraction patterns are recorded with a pixelated detector.
However, pixelated detectors limit the achievable scan speed in experiments due to slow read-out times typically on the order of tens of μs [@10.1093/mictod/qaad005; @bekkevold_ultra-fast_2024].
For comparison, traditional HAADF imaging is commonly acquired with dwell times as low as $1 - 5$ μs, or even as fast as $< 100$ ns when multi-frame acquisitions are obtained to observe dynamic effects [@10.1093/jmicro/dfp052;@10.1093/jmicro/dfaa017].
To realize such sub-$10$ μs dwell times for phase retrieval techniques, we need to look to detectors with a minimal read-out overhead limiting the scan speed, which are still able to retrieve the desired phase information.

One candidate for such detectors are few-pixel annular segmented detectors, which are already in widespread use for both iCOM and OBF imaging.
The use of such detectors for iterative ptychography has been explored in recent years, with promising results [@10.1093/mam/ozae134].

In the following we investigate the impact of detector segmentation on the CTF of phase retrieval techniques iCOM, SSB, tcBF, and iterative ptychography.
Using the CTF to investigate and compare not just the phase retrieval techniques, but also the various detector geometries provides an unbiased comparison and allows for optimizing the balance between scan speed and information transfer.
