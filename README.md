# Quantum Approximate Optimization Algorithm (QAOA) for Portfolio Optimization


## Introduction

This repository contains the implementation and experimental results of using the Quantum Approximate Optimization Algorithm (QAOA) for portfolio optimization. 
QAOA is a quantum algorithm that aims to solve combinatorial optimization problems, and portfolio optimization is a classic problem in finance seeking to construct an investment portfolio that maximizes returns while minimizing risk. 
The pursuit of optimal portfolio selection and optimization is a pressing endeavor, captivating researchers across classical, quantum, and hybrid methodologies. 
The complexity inherent in this pursuit stems from the dual imperative of identifying the optimal solution while contending with time constraints, especially pertinent in the realm of financial transactions.


Accurately predicting the stock market in real-time is an arduous feat, compounded by the vast volume of data and the influence of unpredictable external factors. 
Variables such as geopolitical events, natural disasters, or economic crises can dramatically impact market dynamics, defying traditional quantification methods. 

## Motivation

Our project aims to leverage the Quantum Approximate Optimization Algorithm (QAOA) to address portfolio optimization challenges. 
By employing a quantum simulator, we seek to elucidate the behavior of QAOA on small-scale systems, facilitating benchmarking against classical methodologies. 
Subsequently, this foundational understanding will serve as a springboard for extending our approach to increasingly complex systems.

## Implementation

The implementation is done using Python programming language and leveraging the circ library for quantum computing. The key components of the implementation include:

- Formulation of the Cost Function
The Portfolio Selection problem can be formulated as an optimization problem in which we aim to minimize a cost function of the form:

$$
C(\mathbf{z}) = \lambda\mathbf{z}^T\sigma\mathbf{z}-(1-\lambda)\mathbf{\mu \cdot z}
$$

Where $\mathbf{\mu}$ is the returns vector and $\sigma$ is the covariance matrix of the stocks. The vector $\mathbf{z}$ indicates which operation shall be performed for each stock.

- Encoding the problem into a suitable form for quantum computation.
Performing a 2-spin encoding of $z_i$

$$
z_i = \frac{s_i^+-s_i^-}{2} \quad ; \quad s_i^+, s_i^- \in \{-1,+1\}
$$

Leading to the cost function:

$$
C_{RR}(\mathbf{s}) = \lambda\sum_{i=1}^{N}\sum_{j=1}^N\frac{\sigma_{ij}}{4}\left(s_i^+s_j^+-s_i^+s_j^--s_i^-s_j^++s_i^-s_j^-\right) 
    - \left(1-\lambda\right)\sum_{i=1}^N\frac{\mu_i}{2}\left(s_i^+-s_i^-\right)
$$

The cost function has two components involving the risk and the returns expressed in gate notation:

$$
U_{C, risk} = \prod_{i, j} R_{Z_i^{+} Z_j^{+}}\left(-\frac{1}{2} \lambda \gamma \sigma_{i j}\right) R_{Z_i^{+} Z_j^{-}}\left(\frac{1}{2} \lambda \gamma \sigma_{i j}\right) R_{Z_i^{-} Z_j^{+}}\left(\frac{1}{2} \lambda \gamma \sigma_{i j}\right) R_{Z_i^{-} Z_j^{-}}\left(-\frac{1}{2} \lambda \gamma \sigma_{i j}\right)
$$

$$
U_{C, returns} = \prod_{k=1}R_{Z_k^+}\left(\gamma(1-\lambda) \mu_{\mathrm{k}}\right)R_{Z_k^-}\left(-\gamma(1-\lambda) \mu_{\mathrm{k}}\right)
$$

- Construction of the mixer operator with Soft and Hard Constraints
<!---
Mixer Hamiltonian:

$$
B = \sum_{i=1}^N\sigma_i^x \quad \implies U_B(\beta) = e^{-i\beta H_M} = \prod_{i=1}^NR_X(2\beta) \quad \text{ (in gate notation)}
$$

QAOA with Soft constraints has the penalty function, which is added to the cost function for minimization:

$$
P(\mathbf{s})=\frac{A}{4}\left(s_i^{+} s_j^{+}-s_i^{+} s_j^{-}-s_i^{+} s_j^{+}+s_i^{-} s_j^{-}\right)-A D\left(s_j^{+}-s_j^{-}\right)+A D^2
$$

Where $A$ is the penalty scaling parameter, and $D$ is the net total of discrete lots to be invested.

For the implementation, with the hard constraints, the initialized state is:

$$
\left|\psi_0\right\rangle=(|01\rangle)^{\otimes D} \otimes\left(\frac{1}{\sqrt{2}}|00\rangle+\frac{1}{\sqrt{2}}|11\rangle\right)^{\otimes(N-D)}
$$

With the mixer operator:

$$
U(B, \beta) = U(B_{odd}, \beta)U(B_{even}, \beta)U(B_{last}, \beta)
$$

where,

$$
B_{\text {odd }} = \sum_{a \hspace{1mm} odd}^{N-1}\sigma_a^x\sigma_{a+1}^x + \sigma_a^y\sigma_{a+1}^y
$$

$$
B_{\text {even }} = \sum_{a\hspace{1mm}even}^{N}\sigma_a^x\sigma_{a+1}^x + \sigma_a^y\sigma_{a+1}^y
$$

$$
B_{\text {last }} = \left\{\begin{array}{l}\sigma_N^x \sigma_1^x+\sigma_N^y \sigma_1^y, N \text { odd } \\
I, N \text { even }\end{array}\right.
$$
-->

- Using the cross-entropy classical optimization; Post-processing and analysis of results

## Dependencies and Usage

The following packages are required to run the code in this repository:
- [circ](https://pypi.org/project/circ/)
- [sympy](https://pypi.org/project/sympy/)
- [tqdm](https://pypi.org/project/tqdm/)

To use the code provided in this repository, follow these steps:

1. Clone the repository to your local machine.
2. Install the required dependencies specified in `requirements.txt`.
3. Paste in the main.py file the covariance matrix and returns vector of the desired set of stocks (an example of covariance matrix can be found in the Sigma.csv file)

In this repository we provide some examples of the usage of the code:
The QAOA_circuit example.ipynb notebook builds a symbolic implementation of the QAOA circuit for soft and hard constraints for the selected values of the circuit parameters beta and gamma. In Grid Search.ipynb we illustrate how Grid Search can be used to find the optimal parameters beta and gamma. Finally, in QAOA Comparison.ipynb, we build QAOA circuits with both soft and hard constraints and circuit depths one or two, and extract the best combination found, benchmarking it with a brute force approach.

## Results

We present experimental results showcasing the performance of QAOA in solving portfolio optimization problems. These results include comparisons with classical optimization methods and discussions on scalability and efficiency.

## Future Work

While this project provides valuable insights into the potential of QAOA for portfolio optimization, there are several avenues for future exploration, including:

- Fine-tuning algorithm parameters for better performance.
- Investigating the applicability of QAOA to more complex portfolio optimization scenarios.
- Exploring hardware-specific optimizations for quantum devices.

## Contributing

This project was a short research endeavor by the following collaborators:
- Sibasish Mishra
- Héctor Calero
- Kishore Kumar

## License

This project does not have a specific license. Use at your own discretion.

## Acknowledgements

We want to thank the developers of circ and other open-source libraries used in this project for their invaluable contributions to the field of quantum computing.

---

**Note**: This project is a research endeavor and may contain experimental code. Use at your own discretion.

