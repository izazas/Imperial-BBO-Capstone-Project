# Black-Box Optimisation (BBO) Challenge

## Overview
<p align="justify">
This repository documents a Black-Box Optimisation (BBO) capstone project for Imperial College. The task was to maximise eight unknown functions, with 2 to 8 inputs each, all bounded to [0, 1]. Only one query per function was allowed each week, over 13 weeks. 
</p>

## Project Objective
<p align="justify">
This project tackled eight “black-box” puzzles: hidden mathematical functions, each with between two and eight input settings, whose inner workings were unknown. The goal was to find the settings that give the highest output while testing only one point per function each week. After each result came back, I updated a statistical model that estimated where good values were likely to lie and how confident it was. I then chose the next test point to balance exploring new regions against refining promising ones. Every function beat its starting best. Function 5 rose from about 1,089 to 8,662, Function 4 went from negative to positive, and Function 8 reached 10.0.
</p>


## Problem Specification
* **Objective Functions:** 8 continuous black-box functions (varying from 2D to 8D).
* **Input Domain:** All continuous numeric input features are bounded within $[0, 1]$.
* **Optimization Goal:** Maximize the true scalar output for each function under a fixed evaluation budget.

## Weekly Evaluation Workflow
Evaluations are conducted on a weekly submission schedule with the Imperial College support team:

1. **Query Selection:** Candidate points are generated using our Bayesian optimization strategy.
2. **Submission Format:** Coordinates are submitted as dash-delimited strings matching the function's dimensionality.
   * *Example (3D Function):* `0.123456-0.654321-0.345678`
3. **Data Integration:** The returned scalar outputs are added to each function's dataset to update surrogate predictions for subsequent rounds.

## Technical Approach
<p align="justify">
The first six weeks were exploratory, using <b>RBF</b> and then <b>Matérn</b> kernels with hand-tuned <b>UCB</b>, <b>LCB</b> and <b>EI</b> acquisition functions and no fixed seeds. Some queries performed well, such as F4’s first query (0.58) and F8’s 9.987, but none of the results could be reproduced. Week 7 rebuilt the approach: a noise term, kernel selection by marginal likelihood or leave-one-out, fixed seeds, and data-driven transforms (log for F1, F5 and F7; standardisation for F6 and F8). Weeks 8–10 added calibration and trust regions because the GPs over-predicted away from the best point; in F8, for example, weeks 7–10 were predicted above 10 but returned only 9.96–9.98.
</p>
<p align="justify">
In weeks 11–13 the question changed from “where is the model’s maximum?” to “which model best predicts the top points?” This led to ensembles in F5, F7 and F8, single-variable steps in F6, and structural fits in F8. Once the best value in a function was settled, the remaining queries were used to gather information. Assuming the score is the best value observed, a lower-returning probe carries no penalty. F5’s week-13 query, for instance, repeated the corner point to confirm its exact value.
</p>


## Performance Summary after all 13 Rounds
<div align="center">

### Performance Summary Table
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

## Software and Libraries used
<p align="justify">
Weeks 1 to 6 are not reproducible as I did not use a fixed seed. Weeks 7 to 13 are reproducible (seed 42).
</p>

<div align="center">

|S/W - Library| Version|
| :---: | :---: |
|python      | 3.13.9|
|numpy       | 2.3.5|
|scipy       | 1.16.3|
|scikit-learn| 1.9.0|
|matplotlib  | 3.11.1|
|SEED        | 42|

</div>

## Repository Structure

The repository has two parts:

- `docs/` holds the two project-level documents:
   - *datasheet.md* describes the data.
   - *model_card.md* describes the optimisation approach.
- `Black_Box_Functions/` holds one self-contained folder per function. Each folder has the same four parts:
   1. Strategy report: one `Function_n_BBO_Strategy_Report.md` per function. It covers the week-by-week strategy, why it changed and the final result.
   2. Weekly notebooks: 13 notebooks, `Fn_Week_01` to `Fn_Week_13_Final`. Each one is the code that fitted the surrogate and chose that week’s query. Weeks 1 to 6 are exploratory and not reproducible, because no seed was fixed. Weeks 7 to 13 are reproducible.
   3. Data: 13 `Week_n_Data` folders of NumPy arrays, `inputs.npy` and `outputs.npy`. Each folder is the cumulative dataset at that week, so Week 1 is the initial design and Week 13 is the full history. That makes 208 .npy files (8 functions × 13 weeks × 2).
   4. Report figures: the `PNG` charts used in the report, such as progress by week and strategy evolution.

The structure follows the workflow. The data arrays are the inputs, the notebooks are the process and the reports and figures are the interpretation. Weekly folders make it possible to replay any week’s surrogate model on exactly the data that existed at the time.



## Documentation
[Datasheet](docs/datasheet.md)<br>
[Model Card](docs/model_card.md)<br>
[Function 1 BBO Strategy Report](Black_Box_Functions/Function_1/Function_1_BBO_Strategy_Report.md)<br>
[Function 2 BBO Strategy Report](Black_Box_Functions/Function_2/Function_2_BBO_Strategy_Report.md)<br>
[Function 3 BBO Strategy Report](Black_Box_Functions/Function_3/Function_3_BBO_Strategy_Report.md)<br>
[Function 4 BBO Strategy Report](Black_Box_Functions/Function_4/Function_4_BBO_Strategy_Report.md)<br>
[Function 5 BBO Strategy Report](Black_Box_Functions/Function_5/Function_5_BBO_Strategy_Report.md)<br>
[Function 6 BBO Strategy Report](Black_Box_Functions/Function_6/Function_6_BBO_Strategy_Report.md)<br>
[Function 7 BBO Strategy Report](Black_Box_Functions/Function_7/Function_7_BBO_Strategy_Report.md)<br>
[Function 8 BBO Strategy Report](Black_Box_Functions/Function_8/Function_8_BBO_Strategy_Report.md)