# Datasheet for the Black-Box Optimisation Dataset
<p align="justify">
This datasheet provides a comprehensive overview of the creation, development, and documentation of the dataset used in the **Black-Box Optimisation Capstone Project**, undertaken as part of the **Professional Certificate in Machine Learning and Artificial Intelligence** offered by **Imperial College London**.
</p>

## 1. Motivation
<p align="justify">
The dataset presented herein was created sequentially throughout the Black-Box Optimisation project. It supports the application of Bayesian optimisation techniques to eight unknown and computationally expensive objective functions with varying dimensionalities, ranging from 2D to 8D, under a limited evaluation budget.
</p>

<p align="justify">
The purpose of this dataset is to study and evaluate the performance of different optimisation techniques and methodologies for maximising the outputs of these eight black-box objective functions. The initial dataset was provided by the academic team at Imperial College London and served as the basis for defining the initial search space for the Bayesian optimisation framework.
</p>

## 2. Data Composition
<p align="justify">
The dataset contains numerical input values provided to the optimisation algorithm(s) and their corresponding output values, obtained by evaluating the actual objective functions. Detailed information about the initial dataset provided for each of the eight black-box objective functions is presented in **Table 1** below.
</p>
<p align="centre">

### Table 1: Initial Dataset
</p>
| Function | Initial Input Data Dimensions (# evaluations × # features) | Initial Output Data Dimensions (# evaluations) | Input and Output Data Type | Input Space Range | Output Space Range | Format |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 1 | 10 × 2 | 10 | Real numeric | [0, 1] | Varying | Floating with 6 digits of precision |
| 2 | 10 × 2 | 10 | Real numeric | [0, 1] | Varying | Floating with 6 digits of precision |
| 3 | 15 × 3 | 15 | Real numeric | [0, 1] | Varying | Floating with 6 digits of precision |
| 4 | 30 × 4 | 30 | Real numeric | [0, 1] | Varying | Floating with 6 digits of precision |
| 5 | 20 × 4 | 20 | Real numeric | [0, 1] | Varying | Floating with 6 digits of precision |
| 6 | 20 × 5 | 20 | Real numeric | [0, 1] | Varying | Floating with 6 digits of precision |
| 7 | 30 × 6 | 30 | Real numeric | [0, 1] | Varying | Floating with 6 digits of precision |
| 8 | 40 × 8 | 40 | Real numeric | [0, 1] | Varying | Floating with 6 digits of precision |

<p align="justify">
The initial dataset contained no missing evaluations, and **13 additional evaluations** were performed for each function over the course of the Capstone Project.
</p>

## 3. Collection Process
<p align="justify">
The initial dataset for each of the eight unknown objective functions was provided by the academic team at Imperial College London and contains a specific number of input–output observations, as shown in Table 1.
</p>
<p align="justify">
A surrogate model, in this case a **Gaussian Process (GP)**, is used to approximate the unknown objective function based on the available dataset. The surrogate model provides an estimate of the objective function output (mean) together with an associated measure of uncertainty (variance) across the input space.
</p>
<p align="justify">
An acquisition function, such as **Expected Improvement (EI)** or **Upper Confidence Bound (UCB)**, then uses the information provided by the surrogate model to identify the next query point to be evaluated. This query point is submitted to the Imperial College London academic team, who evaluate the corresponding objective function and return the true output.
</p>
<p align="justify">
The newly evaluated input–output pair is then added to the dataset for the respective function, thereby expanding the available data for subsequent optimisation iterations. This process is repeated for a total of **13 evaluations**, with one query submission and corresponding evaluation performed each week, representing the maximum available evaluation budget.
</p>
<p align="justify">
Details of the surrogate model and acquisition function used for each of the eight objective functions are provided in the individual **“Optimisation Strategy”** documentation, which will be supplied at the end of the project.
</p>

## 4. Preprocessing and Intended Use of the Data
<p align="justify">
No preprocessing was applied to the input data, as the input variables are well-defined real numerical values within the range **[0, 1]**.
</p>
<p align="justify">
Different transformations were applied to the output/target variables of each of the eight objective functions before the data was provided to the surrogate model. These transformations are summarised in **Table 2** below. The rationale for each transformation is provided in the individual **“Optimisation Strategy”** documentation for each function, which will be submitted at the end of the project.
</p>

### Table 2: Target Variable Transformation

| Function | Transformation |
|:---:|:---:|
| 1 | Rank/Copula |
| 2 | z-score standardisation |
| 3 |  $\hat{y}=-log(-y)$ |
| 4 | z-score standardisation |
| 5 | $\hat{y}=log(y)$ |
| 6 | z-score standardisation |
| 7 | $\hat{y}=log(y)$ |
| 8 | z-score standardisation |

### Intended Use of the Datasets
<p align="justify">
The datasets included in this repository are intended for **educational and research purposes related to black-box optimisation**. They may also be used in conjunction with the source files for each objective function, which will be provided at the end of the project.
</p>

### Inappropriate Use of the Datasets
<p align="justify">
As the datasets for each objective function were generated using functions that are not known to the author, they should not be used for purposes other than those described above.
</p>

## 5. Distribution and Maintenance

### Data Availability
<p align="justify">
The data for each of the eight objective functions is available in the corresponding **“Data”** folder within this repository. The complete datasets will be included by the end of the project.
</p>

### Licensing and Terms of Use
<p align="justify">
The datasets are intended for **educational and open-access research purposes**. Any use of the datasets should comply with the terms of use specified in this repository.
</p>