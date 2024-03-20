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

- Construction of the portfolio optimization problem as a binary optimization task.
- Encoding the problem into a suitable form for quantum computation.
- Utilizing Qiskit's QAOA module to perform the optimization.
- Post-processing and analysis of the obtained results.

## Dependencies and Usage

The following packages are required to run the code in this repository:
- [circ](https://pypi.org/project/circ/)
- [sympy](https://pypi.org/project/sympy/)
- [tqdm](https://pypi.org/project/tqdm/)

To use the code provided in this repository, follow these steps:

1. Clone the repository to your local machine.
2. Install the required dependencies specified in `requirements.txt`.
3. Run the main script `qaoa_portfolio_optimization.py` to execute the QAOA algorithm for portfolio optimization.
4. Adjust parameters and experiment with different settings as needed.

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

We would like to thank the developers of circ and other open-source libraries used in this project for their invaluable contributions to the field of quantum computing.

---

**Note**: This project is a research endeavor and may contain experimental code. Use at your own discretion.

