# Model Card: Black-Box Bayesian Optimisation using Gaussian Processes

## Model Overview

- **Model Name:** Black-Box Bayesian Optimisation using Gaussian Processes
- **Type:** Bayesian optimisation using an Anisotropic Matérn 5/2 kernel for surrogate model and an Expected Improvement (EI) acquisition function.
- **Task:** Maximise the output of eight unknown objective functions
- **Version:** V1.0
- **Developer:** Ilias Zazas
- **License:** Academic use
- **Software and Libraries:**
  - Python `3.9.13`
  - NumPy `1.26.4`
  - SciPy `1.13.1`
  - scikit-learn `1.6.1`
  - Matplotlib `3.9.4`
  - `SEED = 42`


## Intended Use

The dataset and model are primarily intended for **educational purposes** in the field of global optimisation of continuous, black-box objective functions limited by a finite evaluation budget.

### Potential Use Cases
The datasets and associated optimisation approaches may be applicable to a range of problems, including:
- **Machine Learning:** Hyperparameter and model configuration optimisation.
- **Engineering:** Aerodynamic, structural, or mechanical design optimisation.
- **Robotics:** Controller or policy parameter tuning.
- **Chemical Processes:** Optimising process parameters or operating conditions.

## Limitations and Excluded Applications

The datasets and optimisation methodology are **not intended** for:
1. **Safety-critical and real-time control applications:** Sequential optimisation may not satisfy stringent latency requirements.
2. **Very large-scale optimisation:** The number of objective evaluations required by BBO may become impractical.
3. **Categorical/Discontinuous inputs:** Optimising functions with discontinuities and/or categorical inputs.


## Optimisation Strategy Evolution

### Rounds 1–5: Initial Exploration & Strategy Shift
- Employed a predominantly exploratory strategy for all eight objective functions.
- **Surrogate Model:** Radial Basis Function (RBF) with isotropic length scales.
- **Acquisition Function:** Upper Confidence Bound (UCB).
- **Parameter Tuning:** The $\beta$ parameter was progressively reduced from $4.0$ to $2.5$ across rounds to gradually shift strategy towards greater exploitation of promising regions.

### Round 6: EDA, Transformation, and Strategy Upgrade
- Conducted detailed Exploratory Data Analysis (EDA).
- Scaled or transformed target variables for each function to improve surrogate predictions.
- **Surrogate Model:** Changed to a Matérn 5/2 kernel with anisotropic length scales to account for non-smooth behaviour and varying rates of variation across dimensions.
- **Acquisition Function:** Switched to Expected Improvement (EI) with $\xi = 0.01$, providing a controlled balance between exploration and exploitation.

### Rounds 7–9: Targeted Exploitation
- The $\xi$ parameter was progressively reduced for selected objective functions to emphasize exploitation of highly promising regions.
- Maintained existing $\xi$ values for remaining functions to preserve a balanced strategy.


## Performance

Performance is evaluated using the **highest unnormalized observed output value** achieved across all evaluations.

<div align="center">

### Table 1: Performance Summary after 9 Rounds

| Function | Initial Best Value | Current Best | Improvement |
| :---: | :---: | :---: | :---: |
| **Function 1** | $7.710875 \times 10^{-16}$ | $4.175390 \times 10^{-10}$ | $4.175382 \times 10^{-10}$ |
| **Function 2** | $0.611205$ | $0.695095$ | $0.083890$ |
| **Function 3** | $-0.034835$ | $-0.008171$ | $0.026664$ |
| **Function 4** | $-4.025542$ | $0.615944$ | $4.641486$ |
| **Function 5** | $1088.859618$ | $8449.496898$ | $7360.637279$ |
| **Function 6** | $-0.714265$ | $-0.404822$ | $0.309443$ |
| **Function 7** | $1.364968$ | $2.609268$ | $1.244300$ |
| **Function 8** | $9.598482$ | $9.997061$ | $0.398579$ |

</div>

## Assumptions and Limitations

### Assumptions
- Objective functions are sufficiently smooth or locally predictable for the surrogate model to yield useful estimates from limited observations.
- Bounded search space adequately represents the region of interest.
- Observed evaluations provide reliable information regarding underlying functions.
- Surrogate model and acquisition function accurately capture the trade-off between exploration and exploitation.

### Limitations & Failure Modes
- Poor surrogate predictions in sparsely sampled or highly non-smooth regions.
- High sensitivity to kernel selection and hyperparameter choices.
- Premature convergence to local optima when exploitation is prioritised too early.
- Insufficient exploration when uncertainty is overemphasised.
- Performance degradation on highly noisy, discontinuous, multimodal, or high-dimensional functions given limited evaluation budgets.


## Reproducibility and Ethical Considerations

### Reproducibility
- All predicted query points were generated with a fixed random seed (`seed=42`).
- Environment specifications (library versions) are fully documented in the *Model Overview*.
- *Note:* Reproducibility may still vary slightly based on platform-specific execution environments and underlying low-level numerical implementations.

### Ethical Considerations
- **Data Privacy & Bias:** The datasets consist exclusively of synthetic numerical data from black-box objective functions without personal, demographic, sensitive, or human-subject information. Algorithmic bias and privacy concerns are not directly applicable.
- **Future Deployment:** Any application of this methodology to real-world decision systems involving human subjects will require comprehensive assessment regarding ethics, fairness, privacy, and safety.