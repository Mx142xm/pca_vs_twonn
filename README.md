# How Many Dimensions Do Data Need?

A small exploratory experiment comparing PCA and TwoNN on synthetic data generated from two latent variables.

## Research Question

How do different dimensionality estimation methods behave when data are generated from a low-dimensional structure and then corrupted by noise?

## What This Project Does

The experiment generates synthetic data using two latent variables and represents them through ten observed features. It then adds different levels of Gaussian noise and compares two approaches to dimensionality estimation:

- **Principal Component Analysis (PCA):** measures how many principal components are needed to explain at least 95% and 99% of the total variance.
- **TwoNN:** estimates intrinsic dimension based on distances to the two nearest neighbours.

The results are visualized to examine how the estimates change as the noise level increases.

## Why This Is Relevant

A research challenge in digital predistortion (DPD) considers whether high-dimensional signal inputs can be represented in a lower-dimensional space while preserving the information needed by the model.

Estimating the dimensionality of data can be a preliminary step in investigating this idea.

This project focuses only on that preliminary question. It does not implement a DPD model, use real radio-frequency measurements, or demonstrate that dimensionality reduction preserves DPD prediction quality.

## Methods

### PCA

PCA finds orthogonal directions that successively explain as much variance in the data as possible.

In this experiment, I record the minimum number of principal components needed to explain 95% and 99% of the observed variance.

These component counts depend on the chosen variance thresholds. They are not direct estimates of intrinsic dimension.

### TwoNN

TwoNN estimates intrinsic dimension using the ratios between distances to the first and second nearest neighbours.

Unlike PCA, TwoNN is based on local neighbourhood geometry rather than the amount of variance explained by linear components.

Its estimate depends on the data distribution, sample size, noise, and the assumptions underlying the method.

## Experimental Setup

1. Generate two latent variables.
2. Construct ten observed features using linear and nonlinear transformations.
3. Add independent Gaussian noise at four levels: 0.00, 0.01, 0.05, and 0.20.
4. Standardize the features.
5. Calculate PCA component counts for 95% and 99% explained variance.
6. Estimate intrinsic dimension using TwoNN.
7. Compare the results in a plot.

A fixed random seed is used to make the experiment reproducible.

## Main Observations

The noise-free data are generated from two latent variables, but PCA may require more than two components to explain a high proportion of the variance because the observed features include nonlinear transformations.

TwoNN estimates the local intrinsic dimension from nearest-neighbour distances. As noise increases, the observed data can depart from the original low-dimensional structure, causing the estimate to change.

The two methods measure different properties and their outputs should not be interpreted as interchangeable estimates.

## Limitations

- The data are synthetic and intentionally simplified.
- The experiment does not establish the intrinsic dimension of real RF signals.
- PCA component counts depend on the selected explained-variance threshold.
- TwoNN can be sensitive to noise, sample size, and the local geometry of the data.
- The experiment does not evaluate prediction error, DPD performance, or total computational cost.
- The results cannot be assumed to generalize to real telecommunications systems.

## Conclusion

This experiment illustrates that the number of observed features does not necessarily reflect the dimensionality of the underlying data structure.

It also shows why dimensionality estimates should be interpreted in the context of the method used and the characteristics of the data.

A possible next step would be to investigate whether dimensionality reduction can preserve the predictive quality of a simplified DPD model.

## How to Run
### Local Environment

Install the required packages:

```bash
pip install -r requirements.txt
```

Run the experiment:

```bash
python src/experiment.py
```

## Repository Structure

```text
intrinsic-dimension-mini-project/
├── README.md
├── requirements.txt
└── src/
    └── experiment.py
```
