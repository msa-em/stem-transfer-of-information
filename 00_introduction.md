---
title: Introduction
---

The contrast transfer function (CTF) is a well-known and well-documented topic in HRTEM, where it is akin to the object transfer function of visible light microscopy. 
Similarly, CTF is much reported for various phase retrieval techniques in scanning transmission electron microscopy (STEM).
The main difference being that in the STEM case it is not as trivial what the CTF is and how it is calculated, with multiple different definitions having been published. 
In its simplest definition, the CTF defines how well information at different spatial frequencies is transferred from the object to the final, reconstructed image. 
This information may be, under certain conditions, be directly obtained from the fast Fourier transform (FFT) of the reconstructed object. 
Still, some definitions multiply the CTF by the inverse error $\frac{\pi\vec{k}}{\sqrt{2}}$, essentially expressing the signal-to-noise ratio (SNR).
In literature, both of these definitions are used interchangeably as the CTF, resulting in a rather confusing landscape in which to discuss contrast transfer of various STEM techniques. 


In an attempt to better this, (cite Pete and others publishing on the DQE metric here) have implemented and thouroughly explained a metric of detector quantum efficiency (DQE). 

Regardless of the metric and definition used to assess the contrast transfer of your detector and reconstruction method, the object being reconstructed should be a white noise object in order to fairly assess the transfer of information. 
In this work, we implement a white noise object that has random phase and constant amplitude in Fourier space, whilst obeying the real-world constraint that it must be real in real-space. 
We then perform a single-slice 4D-STEM simulation and apply virtual detectors to assess both the fully pixelated and segmented detector CTF for integrated center of mass (iCOM) phase reconstructions, direct ptychograpy (SSB), and iterative ptychography. 
