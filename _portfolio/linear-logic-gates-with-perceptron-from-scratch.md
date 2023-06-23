---
layout: single
title: Draft Project - Linear Logic Gates with Perceptron from Scratch (WiP)
permalink: /blog/linear-logic-gates-with-perceptron-from-scratch/
---

The goal of this project was to re-build linear logic gates (AND, OR) in Python using machine learning but without relying on any machine learning libraries. I’ve already built a linear logic gate classifier using the perceptron before - [link](https://github.com/adobiss/ai-ml-portfolio/tree/main/Linear%20Perceptron), but upon code review decided to rebuild it from scratch as the preparation for potentially extending it to non-linear gates (XOR, XNOR, NAND).

The purpose of this project was to refresh the mathematical operations and the logic behind the perceptron (simple, but fundamental linear binary classifier), how to implement it in Python and to build deeper intuition about basic artificial neural network components: neuron, decision boundary and activation function.

**Language:** Python.  
**Libraries used:** NumPy, matplotlib.  
**Code built using:** version control with multiple branches via Git.  
**Code hosted on:** [GitHub](https://github.com/adobiss/linear-ml/tree/main/linear-perceptrons).  
**AI assistance used:** ChatGPT4.  

**Approach:**  
Instead of creating the script from scratch I used ChatGPT4 to create it for me and then dissected the script asking ChatGPT4 questions.

**ChatGPT4 role:**
- Initial script
- Script Q&A
- Early training stoppage implementation
- Decision boundary plot
- Git commands
- Various principle and best practices

**My role:**
- Dissected the script and compared it my old version
- Added epoch counter to the early stoppage
- Version control
- Analysed the performance

**Things learnt:**
- **Git:**
  - Creating new branches for every feature using Git commands. (to keep changes organised as well foundation for collaboration), better understanding of repository management (branch status, adding individual files, etc.).
- **Python:**
  - Using Classes – properties (incl. default values) and methods. Creating and training multiple classifiers (AND, OR gates) within the same script.
  - Unpacking – tuple unpacking (number of features, number of samples)
- **NumPy:**
  - Matrix operations using np.dot (N-D array and 1-D array)
  - Broadcasting
- **GPT-4:** useful perhaps best to write the code by yourself first and ask GPT-4 to review, and then implement the suggestions by yourself, will take longer but will be much easier to navigate the script, plus more practice writing the scripts which is useful

**Outcome:**
- The algorithms classifies correctly and converges quickly (3-5 epochs)
- Upon analysis one sample lies on the decision boundary (for both gates)
- The decision boundary is different from the old script even though the weights and bias are initiated as zeroes and the training process is the same – further investigation required
- Learning rate does not affect decision boundary, but only affects weight vector magnitude – further investigation required
- Neuron output can be modelled as both dot product between weight and input vectors or an output of higher (3-d) dimensional linear function
- Decision boundary can be represented as a 2d linear function or (x,y) intercept of a linear f(x,y)=z, not sure yet if this is useful

**Future considerations:**
- Further, more detailed script analysis is required to understand the unexpected behaviour
- Decision boundary vector vs. function approach analysis required (perhaps as a dedicated blog entry)
- The algorithm can be extended to SVM for decision boundary control and to non-linear gates (e.g. XOR to understand combining multiple decision boundaries)
- Write scripts yourself and ask GPT-4 to review