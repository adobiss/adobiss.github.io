---
layout: single
title: "Problem-Solving in Machine Learning: Modelling Linear Logic Gates in Python"
permalink: /projects/linear-logic-gates-with-perceptron
---

* TOC
{:toc}

# Introduction

## Project Description

**Audience**: Employers in the field of Data Science and Machine learning. The project assumes technical understanding of artificial neural network (ANN) basic principles.

**Objective**: To create linear logic gate model in Python using perceptron algorithm and NumPy and compare its behaviour to that of a similar model created previously.

**Purpose**: To demonstrate the problem-solving and decision-making processes, as well as enhance basic ANN component understanding and their implementation in Python.

## Logic Gates (AND, OR)

Logic gates perform Boolean functions on binary inputs to produce a single binary output (see *Table 1*).

| A | B | A AND B | A OR B |
|---|---|:-------:|:------:|
| 0 | 0 |    0    |   0    |
| 0 | 1 |    0    |   1    |
| 1 | 0 |    0    |   1    |
| 1 | 1 |    1    |   1    |

<small>*Table 1. AND, OR logic gate truth table*<small>

AND, OR logic gates can each be modelled by plotting a single straight line ('hyperplane' or 'decision boundary') and classifying inputs on one side (the green dots) as AND, OR gate respectively (see *Figure 1*).
 
![AND, OR logic gate plot](/assets/images/and-or-logic-gate-plot.png)  
<small>*Figure 1. AND, OR logic gate plot*<small>

## Theoretical Principles Behind the Perceptron

Perceptron is a binary linear classifier. It uses supervised learning to stochastically optimise weight vector w_t and bias b_t via update rule:
 
![Weight update formula](/assets/formulas/weight-update-rule.svg)  
![Bias update formula](/assets/formulas/bias-update-rule.svg)

Where *r* - learning rate, *d_i* - the correct label, *y_i (t)* - the predicted label, *x_i* - the input vector.

See [Wiki](https://en.wikipedia.org/wiki/Perceptron#Learning_algorithm) for more info.

# Logic Gate Models

## Previous Model: Perceptron 1

### Model Description

The model, which was coded manually without Large Language Model (LLM) assistance, is based on the mathematical description of the perceptron from an ANNs course on [Brilliant.org](https://brilliant.org/courses/artificial-neural-networks/).

* [GitHub repository](https://github.com/adobiss/numpy-ml/tree/main/linear-logic-gate-v1)

The model development process description is out of the scope of this project.

## New Model: Perceptron 2

### Model Description

GPT-4 was used to generate the bulk of the code to experiment with LLM assistance.

* [GitHub repository](https://github.com/adobiss/numpy-ml/tree/main/linear-logic-gate-v2)

### Model Development

Initial steps (GPT-4):

1. Initial algorithm generated
2. Tested by the author for code and prediction errors (none encountered)
3. Detailed algorithm explanation by GPT-4 with follow up questions 
4. Early stoppage added due to linear data separability (see *Figure 1*)
5. Decision boundary plot added

	Added by the author throughout the project:

6. Residual calculation condition
7. Linear output floating-point error tolerance threshold
8. Empirical learning rate selection
9. Activation function update
10. In-code documentation (author + GPT-4)
11. GitHub README (author + GPT-4)

# Challenges Encountered with Perceptron 2

## Initial Model Analysis

Decision boundary plot showed:

* Different final weights and decision boundary compared to Perceptron 1 (see *Figures 2, 3*)
* The positive class point [1 1] lying on the decision boundary, unlike in the case of Perceptron 1 (*see Figure 3*)
* Learning rate only affected final weight vector magnitude and not decision boundary (see *Figure 4*)
 
![Perceptron 1 final decision boundary (learning rate n/a)](/assets/images/perceptron-1-decision-boundary.png)  
<small>*Figure 2. Perceptron 1 final decision boundary (learning rate n/a)*<small>

![Perceptron 2 final decision boundary (learning rate 1)](/assets/images/perceptron-2-decision-boundary-lr-1.png)  
<small>*Figure 3. Perceptron 2 final decision boundary (learning rate 1)*<small>

![Perceptron 2 final decision boundary (learning rate 0.5)](/assets/images/perceptron-2-decision-boundary-lr-0-5.png)  
<small>*Figure 4. Perceptron 2 final decision boundary (learning rate 0.5)*<small>

## Perceptron 2 & 1 Weight Difference Analysis

Potential factors contributing to weight differences between Perceptron 2 & 1 were assessed and ruled out:

* Sample order
* Initial weights/ bias
* Learning rate

Despite slight implementation differences, both models used the same weight update formula: w ± x_i. However, tracking weight/ bias updates identified a divergence after step 11, when Perceptron 2 stopped updating 'prematurely' (see *Table 2*).

| Step # | Perceptron 2 |       | Perceptron 1 |       |
|--------|--------------|-------|--------------|-------|
|        | Bias         | Weights | Bias         | Weights |
|   1    |     -1      |  [0 0]  |     -1      |  [0 0]  |
|   2    |      0      |  [1 1]  |      0      |  [1 1]  |
|   3    |     -1      |  [1 1]  |     -1      |  [1 1]  |
|   4    |     -2      |  [0 1]  |     -2      |  [0 1]  |
|   5    |     -1      |  [1 2]  |     -1      |  [1 2]  |
|   6    |     -2      |  [0 2]  |     -2      |  [0 2]  |
|   7    |     -3      |  [0 1]  |     -3      |  [0 1]  |
|   8    |     -2      |  [1 2]  |     -2      |  [1 2]  |
|   9    |     -3      |  [1 1]  |     -3      |  [1 1]  |
|  10    |     -2      |  [2 2]  |     -2      |  [2 2]  |
|  <mark>11</mark>    |     <mark>-3</mark>      |  <mark>[1 2]</mark>  |    <mark>-3</mark>      |  <mark>[1 2]</mark>  |
|  12    |     …       |   …    |     -2      |  [2 3]  |

<small>*Table 2. Perceptron 2 & 1 training weight comparison*<small>

Decision boundary points are not a concern for logic gates as all possible inputs are included in the training data, and the outputs are strictly binary. However, this 'early stoppage' was not exhibited by Perceptron 1, necessitating a deeper investigation.

While Perceptron 1 used neuron output directly in its error function, Perceptron 2 utilised an activation function:

```python
def _unit_step_func(self, x):
	return np.where(x>=0, 1, 0)
```

The activation function would output '1' (or '0' if we changed `x>=0` to `x>0`) for a decision boundary point which in conjunction with the label range (0, 1) would result in 'correct' prediction (zero residual) for one of the classes and no weight update.

*Perceptron 2 update rule:*

```python
y_predicted = self.activation_func(linear_output)

# Perceptron Update Rule
update = self.lr * (y_[idx] - y_predicted) # Residual (Error function)

if update != 0: # Error function minimisation
	# proceed with weight update
```

On the other hand, Perceptron 1 employed (-1, 1) labels (Y) while also utilising a 'sign based' error function, enabling a weight update with a neuron output of '0':

*Perceptron 1 update rule:*

```python
if np.matmul(X_samples[i], w) * Y[i] <= 0: # Error function
	# proceed with weight update
```

Adopting a similar error function and labelling mechanism in Perceptron 2 could lead to complications:

* The error function should utilise the activation function, not the neuron output
* Introducing a 'sign function' as the activation function would shift the prediction range from (0, 1) to (-1, 1), which could pose potential system compatibility issues

In response, Perceptron 2 retained a slightly modified activation function: `return np.where(x>0, 1, 0)` instead of return `np.where(x>=0, 1, 0)`. 

Additionally, a conditional line was incorporated to assign a (-1) residual to the negative class on the decision boundary:

```python
if linear_output == 0 and y_[idx] == 0:
	update = self.lr * (-1)
```

This modification aligned Perceptron 2 & 1 decision boundaries and total training steps (see *Figures 5, 6*). Tested for AND, OR gates.

![Perceptron 1 final decision boundary (learning rate n/a)](/assets/images/perceptron-1-decision-boundary.png)   
<small>*Figure 5. Perceptron 1 final decision boundary (learning rate n/a)*<small>
 
![Perceptron 2 final decision boundary (learning rate 1)](/assets/images/perceptron-2-decision-boundary-fixed.png)  
<small>*Figure 6. Perceptron 2 final decision boundary (learning rate 1)*<small>

## Addressing Floating-Point Errors

With learning rate set at '0.1', the experiment resulted in a different decision boundary (see *Figure 7*). Interestingly, data point [0 1] appeared to fall right on this boundary line.

![Perceptron 2 final decision boundary (learning rate 0.1)](/assets/images/perceptron-2-decision-boundary-lr-0-1.png)  
<small>*Figure 7. Perceptron 2 final decision boundary (learning rate 0.1)*<small>

Detailed training stats highlighted a small decimal bias introduction at Step #7 and a near-zero neuron output (instead of zero) after Step #8 for Sample #3: [0 1] thus classifying the point 'correctly' and ending the training (see *Tables 3, 4*).

| <mark>Update #7</mark>  |
|:-----------------|
| Bias update: -0.1, weights update: [-0.  -0.1] |
| Bias after update: <mark>-0.30000000000000004</mark>, weights after update: [0.  0.1] |

<small>*Table 3. Training stats after step 7*<small>

| <mark>Update #8</mark>                                                             |
|:-------------------------------------------------------------------------|
| Bias update: 0.1, weights update: [0.1 0.1]                                |
| Bias after update: -0.20000000000000004, weights after update: [0.1 0.2] |
| <mark>Sample #3</mark>: [0 1]                                                          |
| Linear output: <mark>-2.7755575615628914e-17</mark>, predicted class: 0, correct class: 0 |

<small>*Table 4. Training stats after step 8*<small>

Quick research established that not all decimal numbers can be represented exactly in binary, leading to small round-off errors, which start around 15-17th decimal digits for Python float and NumPy array.

Several solutions were examined, each with its drawbacks:

* Python's decimal module: slower, increased code complexity
* `Round()`: risk of data loss due to rounding
* High-precision data types (e.g. `numpy.longdouble`): slower, greater memory usage, possible portability and compatibility issues
* Rearranging calculations: possible need for significant code refactoring
* Value threshold/ tolerance introduction: useful for float comparisons but prone to error accumulation

The introduction of a learning rate hyperparameter to Perceptron 1 resulted in the same floating-point error (regardless of the differences in implementation), indicating that rearranging calculations (i.e. removing the error *at source*) might not be a quick fix.

Given the simplicity of Perceptron 2, the issue was addressed only when it negatively affected performance, which was when '0' wasn't passed to the activation function for decision boundary points during training.

A conditional linear output was set using a tolerance threshold as a Perceptron class parameter (with a sensible default of '1e-9'), however the round() function would have achieved the same result:

```python
linear_output = np.dot(x_i, self.weights) + self.bias

if abs(linear_output) < self.tolerance:
	linear_output = 0 # Correct for floating point error
y_predicted = self.activation_func(linear_output)
```

![Perceptron 2 final decision boundary (learning rate 1)](/assets/images/perceptron-2-decision-boundary-lr-0-1-fixed.png)  
<small>*Figure 8. Perceptron 2 final decision boundary (learning rate 0.1)*<small>

## Analysis and Optimisation of Learning Rate

Without the floating-point error ending the training prematurely (see *Figure 8*), we arrived at the same final decision boundary for all learning rates with only the weight vector magnitude changing. Moreover, both weight vector and bias were effectively scaled by the learning rate at every step (see *Table 5*).

| Update # | Bias (r=0.1) | Bias (r=1) | Weights (r=0.1) | Weights (r=1) |
|----------|---------------|-------------|------------------|----------------|
|    #1    |    -0.1       |    -1       |      [0 0]       |      [0 0]     |
|    #2    |       0       |     0       |    [0.1 0.1]     |      [1 1]     |
|    #3    |    -0.1       |    -1       |    [0.1 0.1]     |      [1 1]     |
|    #4    |    -0.2       |    -2       |    [0 0.1]       |      [0 1]     |
|    #5    |    -0.1       |    -1       |    [0.1 0.2]     |      [1 2]     |
|   ...    |      ...      |    ...      |       ...        |       ...      |
|   #18    |    -0.4       |    -4       |    [0.2 0.3]     |      [2 3]     |

<small>*Table 5. Weight and bias comparison for learning rate (r) 0.1 vs. 1*<small>

The updates affected the decision boundary equally regardless of learning rate *r* because weights and bias were initiated as zeroes and the first non-zero weight was essentially an input vector scaled by *r: w_1=r \* x_i*. Since all subsequent updates are scaled by the same *r* we would get:

![First non-zero weight scaling by r](/assets/formulas/weight-1-learning-rate-scaling.svg),  
![Second non-zero weight scaling by r](/assets/formulas/weight-2-learning-rate-scaling-long.svg)  
![Second non-zero weight scaling by r repeated](/assets/formulas/weight-2-learning-rate-scaling-short.svg)

producing new weight vector *w_2* that has the same direction for all *r* (true for all *i* in *w_i*).

The bias was also scaled by the *r* resulting in 2-d hyperplane of the form:

![Decision boundary with r](/assets/formulas/decision-boundary-with-r.svg) 

which equals:

![Decision boundary divide by r](/assets/formulas/decision-boundary-divided-by-r.svg) 

However, the scaling pattern broke if we initialised weights and bias as '1s'.

With weights and bias initialised as '1s' and using AND gate as an example the number of steps did not follow the somewhat expected pattern (smaller rate, longer to converge). That's why an empirical method was used to establish the best learning rate and then fit the model using the best *r* (see *Figure 9*).

![Empirical learning rate selection](/assets/images/perceptron-2-empirical-learning-rate-selection.jpg)  
<small>*Figure 9. Empirical learning rate selection*<small>

## Updating and Improving the Activation Function

Adding a condition to the error function to penalise negative class decision boundary points seemed like an inelegant solution. It introduced unnecessary complexity and prevented the calculation of residuals with a single mathematical expression:

```python
if linear_output == 0 and y_[idx] == 0:
	update = self.lr * (-1)
else:
	update = self.lr * (y_[idx] - y_predicted)
```

Previously, GPT-4 had advised that in the case of sigmoid activation function the points on the decision boundary could output 0.5 (50%). 

This concept seemed appropriate for Perceptron's 2 activation function as well, with a boundary point producing an output of 0.5, situated between 0 and 1.

Residuals in the range (-0.5, 0.5) preserved the 'direction' of the required update, and the magnitude of the update was scaled by 0.5, reflecting that points on the decision boundary would typically require smaller updates for correct classification.

Researching perceptron and step functions on wiki showed identical activation function implementation, however provided more info on the unit step function range: the function can yield either '0', '0.5', or '1' for an input of '0', depending on interpretation. This allowed to extend the activation function's output without changing the function type itself.

An attempt to include the additional output by rewriting the `np.where(x>0, 1, 0)` function in an 'if/ elif/ else' format resulted in an error when the 'predict' method was invoked from the Perceptron class instance. This issue arose because while the 'fit' method passed a float to the activation function, 'predict' passed an array (all samples at once).

The simplest solution seemed to add additional condition to the existing `np.where` function. GPT-4 customised the existing `return np.where(x>0, 1, 0)` by introducing a nested condition, thus resolving the compatibility issue:

```python
return np.where(x < 0, 0, 
                       np.where(x == 0, 0.5, 1))
```

# Conclusion

## Summary

Perceptron's 2 decision boundary evolution was studied in-depth. Despite differences in implementation from Perceptron 1, identical outcomes were achieved, validating algorithm comprehension.

Binary computation limitations were encountered with the most appropriate solution implemented.

The mathematical description of how learning rate scaled the weights provided a deeper understanding and enabled alternative solutions.

By modifying Perceptron 2's activation function, we gained insight into its role, relation to other components and activation function choice. This modification also reduced the model's complexity.

## Lessons Learnt

* The usefulness of tracking weight updates at every step demonstrated that a more analytical approach must be employed going forward instead of spending too much time on an algorithm logic alone.
* Identical error function behaviour was assumed for both models even though the labels differed. Training data format implications must be considered more carefully.
* The initial conclusion about learning rate not affecting the decision boundary was incorrect (i.e. floating-point error). A broader (hyper)parameter value range must be tested next time.

## Future Considerations

* Create `linear_output` class method that also applies floating-point error tolerance threshold (to be reused in both *fit* and *predict* Perceptron class methods).
* Alternative solutions to floating-point errors, such as using the `round()` function or rearranging calculations can be explored.
* Experiment with various weight initialisation values, their effect on learning rate and the resulting 'updates to converge' pattern.

## Next Steps

* Implementing diverse input vectors (e.g. using real-life data) to study the impact of larger inputs and outliers.

Perceptron 2 extensions could include:

* support vector machine (for boundary distance)
* non-linear logic gate XOR (for multiple decision boundaries)
* multiclass classification (to compare with binary classification)

## LLM Assistance

GPT-4 as an LLM can accelerate development, albeit with requirement for reverse-engineering.

It's a learning source for new methods and best practices, however practical implementation without LLMs remains crucial.

LLMs can be used to generate code from scratch or for code review.