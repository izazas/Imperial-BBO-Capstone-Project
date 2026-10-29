# Model Card: Black-Box Bayesian Optimisation using Gaussian Processes

## Model Overview
- **Model Name:** Black-Box Bayesian Optimisation using Gaussian Processes
- **Type:** Bayesian optimisation using an Anisotropic Matérn 5/2 kernel for surrogate model and an Expected Improvement (EI) acquisition function.
- **Task:** Maximise the output of eight unknown objective functions
- **Version:** V1.0
- **Developer:** Ilias Zazas
- **License:** Academic use
- **Software and Libraries:**
  - Python `3.13.9`
  - NumPy `2.3.5`
  - SciPy `1.16.3`
  - scikit-learn `1.9.0`
  - Matplotlib `3.11.1`
  - `SEED = 42`

## Intended Use
<p align="justify">
The dataset and model are primarily intended for <b>educational purposes</b> in the field of global optimisation of continuous, black-box objective functions limited by a finite evaluation budget.
</p>

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

### Weeks 1 to 6: learning rounds
-	RBF ARD kernels in weeks 1 to 3, then an isotropic Matérn kernel.
-	No noise term, and mostly no random seed.
-	UCB, LCB and EI settings changed by hand.
- The results were uneven and not reproducible.
### Week 7: the main rebuild. The notebooks were rewritten around a more careful and stractured format:
-	a noise term added;
-	a target transform chosen from the data;
-	ARD against isotropic kernels chosen by marginal likelihood or leave-one-out (LOO) density;
-	Fixed seeds, so weeks 7 to 13 can be re-run.
### Weeks 8 to 10: calibration and local search.
-	Started checking the model against what it actually predicted by using LOO on the queried points and comparing last week’s prediction with the outcome.
-	I added trust regions and cross-check models: an additive quadratic for F6, a slab regression for F4 and a local bowl for F3.
-	Made the acquisition more exploitative ($\xi$ 0.01 down to 0.005, 0.002 or 0.0001).
### Weeks 11 to 13: ensembles and structure tests.
-	Several models were compared, and queries were scored by consensus (F7, F8) or by single-variable steps.
-	Checked whether the function had a simple exact form (F8).

## Performance
<p align="justify">
Performance is evaluated using the <b>highest unnormalized observed output value</b> achieved across all evaluations.
</p>

<div align="center">

### Table 1: Performance Summary after all 13 Rounds

| Function | Initial Best Value | Final Best | Improvement |
| :---: | :---: | :---: | :---: |
| **Function 1** | $7.710875 \times 10^{-16}$ | $1.9634$ | $1.96339$ |
| **Function 2** | $0.611205$ | $0.695095$ | $0.083890$ |
| **Function 3** | $-0.034835$ | $-0.002265$ | $0.032569$ |
| **Function 4** | $-4.025542$ | $0.6555$ | $4.681042$ |
| **Function 5** | $1088.859618$ | $8662.48$ | $7573.620381$ |
| **Function 6** | $-0.714265$ | $-0.2513$ | $0.462965$ |
| **Function 7** | $1.364968$ | $2.7833$ | $1.418332$ |
| **Function 8** | $9.598482$ | $10.0000$ | $0.401518$ |

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

- Weeks 1 to 6 are not reproducible as I did not use a fixed seed. Weeks 7 to 13 are reproducible (seed 42).
- Environment specifications (library versions) are fully documented in the *Model Overview*.
- **Note:** Reproducibility may still vary slightly based on platform-specific execution environments and underlying low-level numerical implementations.

### Ethical Considerations

- **Data Privacy & Bias:** The datasets consist exclusively of synthetic numerical data from black-box objective functions without personal, demographic, sensitive, or human-subject information. Algorithmic bias and privacy concerns are not directly applicable.
- **Future Deployment:** Any application of this methodology to real-world decision systems involving human subjects will require comprehensive assessment regarding ethics, fairness, privacy, and safety.
