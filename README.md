# Robust-Nework-Nonlocality

This repository contains the Python code to reproduce the results and explore the concepts presented in the paper: "Noise-robust proofs of quantum network nonlocality".

# 📝 Overview
Quantum networks, where multiple parties share entanglement from independent sources, open avenues for novel forms of quantum nonlocality. By skillfully combining entangled states and entangled measurements, it's possible to generate strong nonlocal correlations that span the entire network. However, most theoretical demonstrations of these effects have been confined to idealized, noiseless scenarios, assuming perfect pure entangled states and flawless projective measurements.

This work confronts this challenge by presenting noise-robust proofs of network quantum nonlocality. We focus on a specific class of quantum distributions generated on the triangle network topology, which inherently relies on entangled states and entangled measurements. A cornerstone of our approach is the development of approximate rigidity results for local distributions that exhibit properties like "parity token counting" with high probability.

The significance of this research lies in its practical implications. By considering quantum distributions arising from imperfect sources and measurements, we quantify the resilience of network nonlocality to realistic imperfections. Specifically, we establish noise robustness thresholds for phenomena such as dephasing noise (up to approximately 80%) and white noise (up to approximately 0.67%). Furthermore, we demonstrate that even distributions that are merely in the vicinity (measured by total-variation distance) of certain ideal nonlocal quantum distributions retain their nonlocality. This research paves the way for the experimental observation and practical implementation of quantum nonlocality in complex network configurations.

The Python code provided in this repository allows for the numerical simulation and verification of these findings, particularly for the triangle network under various noise models.
