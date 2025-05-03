---
title: Integrated Center of Mass Imaging with a Segmented Detector
short_title: Segmented iCOM
numbering:
  enumerator: 7.%s
label : segmented_icom_page
---

:::{warning} To-Do:
- <s>Introduce segmented detectors</s>
- Introduce analytical iCOM CTF (detector segment autocorrelation with complex-probe)
- <s>Discuss radial vs annular segments</s>
- <s>Discuss CTF > 1</s>
:::

So far we have discussed the CTF of phase retrieval techniques when the whole CBED patterns including the detailed information they contain is recorded with a pixelated detector. 
However, pixelated detectors limit the scan speed in experiments because the read-out time is typically on the order of tens of μs.
For comparison, traditional HAADF imaging is not uncommonly acquired with dwell times around $1 - 5$ μs, and even $< 100$ ns may be used for multi-frame recording to observe dynamic effects [@10.1093/jmicro/dfp052;@10.1093/jmicro/dfaa017]. <!-- Could also cite Ishikawa's newest article: ;@10.1126/sciadv.adk6501]. -->
To realize such sub-$10$ μs dwell times for phase retrieval techniques, we need to look to detectors with a minimal read-out overhead limiting the scan speed, which are still able to retrieve the desired phase information.

One candidate for such detectors are segmented detectors, which are already in widespread use for both iCOM and SSB. 
In the following we investigate the impact of detector segmentation on the CTF of phase retrieval techniques iCOM, SSB, tcBF, and iterative ptychography, starting here with iCOM.

## Analytical segmented iCOM CTF
In @pixelated_icom_page we saw that the analytical CTF for iCOM with a pixelated detector is the probe autocorrelation because the detector function $D(\bm{k})$ covers every pixel in the detector as seen in @com_detector_eq.
However, for a segmented detector, the detector geometry function from @complex_detector_eq, reproduced here for convenience:
:::{math}
:label: segmented_detector_eq
D(\bm{k}) = \sum_j c_j D_j(\bm{k}),
:::
has to take the segment geometries into account.
The detector function for the $j$th segment is
:::{math}
D_j(\bm{k}) = 
\begin{cases}
1, & \text{for }\bm{k}\text{ inside detector segment }j \\
0, & \text{elsewhere}
\end{cases}
:::
and $c_j$ is the (possibly negative) center of mass of detector segment $j$.
Now the analytical CTF is given by the autocorrelation of each detector segment with the complex probe, which is shown visually in @fig_segmented_icom.
Here, we can see how the symmetry of the detector is reflected in the symmetry of the two-dimensional CTF.


:::{figure} #app:segmented_icom
:label: fig_segmented_icom
:placeholder: ./figures/segmented_icom_placeholder.png
Effect of various detector geometries on the CTF for iCOM imaging.
:::

## Detector impacts
Since the CTF relies on $c_j$, the center of mass of detector segment $j$, the outer collection angle of an annular detector should match the semi-convergence angle, $\alpha$, for the COM approximation to be accurate.
An outer collection angle $>> \alpha$ results in over-estimation of the COM signal, and thus produces a CTF above unity. 
This effect may be somewhat mediated by introducing radial rings which allows the detector to resolve differences in the CBED pattern intensity radially in addition to annularly. <!-- Azimuthally? -->
Also note that offsetting half of the ring's segments by half of their annular span range ($45^\circ$ for four segments spanning $90^\circ$ each) adds the benefit of better annular resolution, yielding a rounder CTF.
