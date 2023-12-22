---
date: December 12, 2023 (13h48)
tags:
  - lesson
  - done
topic: "[[Machine Learnig]]"
class: "[[Courses#^ddc1b1|Hands-On Machine Learning]]"
professor: Aurélien Géron
place: "[[CIC|Library]]"
sr-due: 2023-12-25
sr-interval: 3
sr-ease: 250
---
`=this.file.tags`
# HOML - Chapter 4

This chapter covers what goes under the hood when we instantiate and train regression algorithms.

## Linear Regression

- Linear Regression formula and parameters
	- How to find the best parameter value
		- Cost function and performance measure relation in the optimization
			- RMSE and MSE vectorized formula
		- Normal Equation and SVD 
			- Definition
			- Comparison between formulas and differences in computing complexity
				- When they reach their limit and other positive things in light of computing complexity.
		- GD
			- Definition and how it works (eta, partial derivative)
			- MSE case and properties (type of function and type of derivative)
			- Data scale
			- Parameters space and consequences
			- Batch GD
				- Formula for cost function calculation for linear regression
				- Algorithm and parameter and/or hyperparameters
				- Observations on convergence (convergence rate, tolarence)
			- Stochastic GD
				- Difference from Batch GD
				- Trade-off of its stochastic nature
					- Other strategy for the stochasticism (IID)
				- Observations on convergence
					- Learning schedule
			- Mini Batch GD
				- What is the strategy?
				- Observations on convergence

Complete (m = instances, n = features):

| Algorithm | Large m | Out of core learning? | Large n | # hyperparameters | Scaling? | Sci-Kit Learn? |
| --------- | ------- | --------------------- | ------- | ----------------- | -------- | -------------- |
| f         |         |                       |         |                   |          |                |
| f         |         |                       |         |                   |          |                |
|  f         |         |                       |         |                   |          |                |
| f          |         |                       |         |                   |          |                |

## Polynomial Regression

---
## Questions
1. [[Quando é melhor usar um GD e um SVD?]]
2. [[Como definir uma boa função para learning scheduler?]]

---
# References
> d

---
# Questions (by ChatGPT)
#homl 