Robust Network Nonlocality
This repository contains the Python code to reproduce the results and explore the concepts presented in the paper: "Noise-robust proofs of quantum network nonlocality".

📝 Overview
Quantum networks, where multiple parties share entanglement from independent sources, open avenues for novel forms of quantum nonlocality. By skillfully combining entangled states and entangled measurements, it's possible to generate strong nonlocal correlations that span the entire network. However, most theoretical demonstrations of these effects have been confined to idealized, noiseless scenarios, assuming perfect pure entangled states and flawless projective measurements.

This work confronts this challenge by presenting noise-robust proofs of network quantum nonlocality. We focus on a specific class of quantum distributions generated on the triangle network topology, which inherently relies on entangled states and entangled measurements. A cornerstone of our approach is the development of approximate rigidity results for local distributions that exhibit properties like "parity token counting" with high probability.

The significance of this research lies in its practical implications. By considering quantum distributions arising from imperfect sources and measurements, we quantify the resilience of network nonlocality to realistic imperfections. Specifically, we establish noise robustness thresholds for phenomena such as dephasing noise (up to approximately 80%) and white noise (up to approximately 0.67%). Furthermore, we demonstrate that even distributions that are merely in the vicinity (measured by total-variation distance) of certain ideal nonlocal quantum distributions retain their nonlocality. This research paves the way for the experimental observation and practical implementation of quantum nonlocality in complex network configurations.

The Python code provided in this repository allows for the numerical simulation and verification of these findings, particularly for the triangle network under various noise models.

🔬 Theoretical Background & Notebook Details
The research investigates the conditions under which quantum networks display correlations inexplicable by local hidden variable models, even with independent sources. This is achieved by moving beyond idealized scenarios and incorporating noise into the system. The "inflation" technique remains a conceptual background for bounding classical correlations, but the primary focus here is on the robustness of quantum correlations.

The core quantum state often considered for distribution is of the form:

∣ψ⟩=λ 
0
​	
 ∣01⟩+λ 
1
​	
 ∣10⟩
This state, or variations thereof, is distributed by sources within the network (e.g., the triangle network involving three parties, Alice, Bob, and Charlie, each receiving subsystems from two independent sources).

Key Notebooks and Formulations:

The Jupyter notebooks implement the mathematical framework to analyze these networks, primarily using Linear Programming (LP) solved with MOSEK to distinguish quantum nonlocal correlations from classical ones.

Noisless_MOSEK.ipynb:

Focus: Establishes the baseline by generating the quantum probability distribution in the absence of noise and formulates the LP to test for nonlocality in this ideal scenario.

States & Measurements: Defines the initial bipartite entangled state ∣ψ⟩ and the projective measurements ∣ϕ 
x,y
​	
 ⟩ performed by the parties.

∣ϕ 
1,0
​	
 ⟩
∣ϕ 
1,1
​	
 ⟩
∣ϕ 
0,0
​	
 ⟩
∣ϕ 
0,1
​	
 ⟩
​	
  
=u∣0,1⟩+v∣1,0⟩
=v∣0,1⟩−u∣1,0⟩
=w∣0,0⟩+z∣1,1⟩
=z∣0,0⟩−w∣1,1⟩
​	
 
LP Formulation: Sets up the constraints for a local hidden variable model in the network, including probability normalization and independence conditions reflecting the network structure. The objective function then tests if the quantum distribution lies outside the classical polytope.

LP_WhiteNoise_BEST_Q64.ipynb:

Focus: Investigates the impact of white noise on the nonlocality of the network. White noise can be introduced at the source level (affecting the shared state) and/or at the measurement stage.

State under Source White Noise: The initial state ρ 
S
​	
 =∣ψ⟩⟨ψ∣ is mixed with maximally mixed noise:

ρ=(1−W)ρ 
S
​	
 + 
D 
N
 
W
​	
 I
(where D is dimension, N is number of particles per source, typically W/4 for a two-qubit source).

Noisy Measurements: Measurements M 
x 
1
​	
 ,x 
2
​	
 
​	
  can also be affected:

M 
x 
1
​	
 ,x 
2
​	
 
′
​	
 =(1−η)M 
x 
1
​	
 ,x 
2
​	
 
​	
 +η 
d 
k
 
I
​	
 
(Note: The original text had M 
x 
1
​	
 ,x 
2
​	
 
′
​	
 +η 
d 
k
 
I
​	
 , which seems like a typo. Assuming it should be an assignment like (1−η)M 
x 
1
​	
 ,x 
2
​	
 
​	
 +η 
d 
k
 
I
​	
 . I've kept it closer to the previous version's formula structure, M 
x 
1
​	
 ,x 
2
​	
 
′
​	
 , implying the noisy measurement operator.)
(where d is local dimension, k is number of particles measured, typically ηI/4 for a two-qubit measurement).

The notebook aims to find the critical noise parameters (W,η) beyond which nonlocality is lost. The f 
ϵ
​	
  function mentioned is likely related to specific bounds or conditions under this noise model.

Dephasing_noise_LP.ipynb:

Focus: Analyzes the robustness of network nonlocality against dephasing noise. Dephasing affects the off-diagonal elements of the density matrix in a specific basis.

State under Dephasing Noise: For the state ∣ψ⟩=λ 
0
​	
 ∣01⟩+λ 
1
​	
 ∣10⟩, the dephased state becomes:

ρ 
D
​	
 =(1−d)∣ψ⟩⟨ψ∣+d(λ 
0
2
​	
 ∣01⟩⟨01∣+λ 
1
2
​	
 ∣10⟩⟨10∣)
The notebook then uses LP to find the critical dephasing parameter d.

TV_Noise_LP_MOSEK.ipynb:

Focus: This notebook appears to analyze robustness against a general mixing noise, often parameterized by a visibility V, which can be related to Total Variation (TV) distance from an ideal distribution or mixing with white noise.

State under General Mixing Noise: The noisy state is typically of the form:

ρ=Vρ 
ideal
​	
 +(1−V)ρ 
noise
​	
 
where ρ 
noise
​	
  is often the maximally mixed state. The LP is used to determine the minimum visibility V for which nonlocality can still be observed.

💻 Code Structure & Usage
The primary code is organized into Jupyter Notebooks. Each notebook contains:

Python code for numerical simulations.

LaTeX annotations explaining the theoretical steps and formulas.

Implementations of network topologies, quantum states, measurements, and noise models.

Linear Programming (LP) formulations solved using MOSEK to certify nonlocality.

Plotting routines to visualize the results (e.g., regions of nonlocality vs. noise parameters).

Prerequisites:

Ensure you have the following Python libraries installed:

NumPy: For numerical computations.

pip install numpy

SciPy: For scientific computing, potentially including optimization routines.

pip install scipy

MOSEK: A high-performance solver for large-scale optimization problems, crucial for the LPs. A MOSEK license (free academic licenses are available) and its Python bindings are required.

pip install mosek

Matplotlib: For generating plots.

pip install matplotlib

SymPy: For symbolic mathematics (used in Dephasing_noise_LP.ipynb).

pip install sympy

tqdm: For displaying progress bars during lengthy computations.

pip install tqdm

(CVXPY): While MOSEK is used directly, CVXPY might be a useful higher-level interface for some users if they wish to modify the LPs.

# pip install cvxpy

Running the Code:

Clone the repository:

git clone [https://github.com/SadraBoreiri/Robust-Nework-Nonlocality.git](https://github.com/SadraBoreiri/Robust-Nework-Nonlocality.git)
cd Robust-Nework-Nonlocality

Install dependencies:
Ensure all prerequisites listed above are installed and MOSEK is correctly configured with a valid license.

Launch Jupyter Notebook:

jupyter notebook

Navigate to and open the desired .ipynb file (e.g., LP_WhiteNoise_BEST_Q64.ipynb). Run the cells sequentially. The embedded LaTeX and comments will guide you through the logic and calculations.

📊 Expected Outputs
By running the Jupyter notebooks, you should be able to:

Reproduce the key numerical results and figures presented in the paper, particularly the plots showing nonlocal regions as a function of noise parameters and state/measurement choices.

Calculate critical noise thresholds for observing nonlocality in the triangle network under different noise models (white noise, dephasing noise).

Gain a practical understanding of how Linear Programming can be used to certify network nonlocality and assess its robustness.

🧑‍🔬 Author
Sadra Boreiri (Primary author of the paper and code)
Co-authors of the paper: Bora Ulu, Nicolas Brunner, Pavel Sekatski

📄 Citation
If you use this code or the findings from the paper in your research, please cite the paper:

S. Boreiri, B. Ulu, N. Brunner, and P. Sekatski. Noise-robust proofs of quantum network nonlocality. arXiv:2311.02182 [quant-ph] (2023).

@article{Boreiri2023robust,
  title={Noise-robust proofs of quantum network nonlocality},
  author={Boreiri, Sadra and Ulu, Bora and Brunner, Nicolas and Sekatski, Pavel},
  journal={arXiv preprint arXiv:2311.02182},
  year={2023},
  eprint={2311.02182},
  archivePrefix={arXiv},
  primaryClass={quant-ph}
}

⚖️ License
Please include a license file in your repository (e.g., MIT, Apache 2.0). If you haven't chosen one, you might consider adding a standard open-source license such as the MIT License. For now, this is a placeholder:

This project is licensed under the [NAME OF LICENSE] - see the LICENSE.md file for details (if available).
