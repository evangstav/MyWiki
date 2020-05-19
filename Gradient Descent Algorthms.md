# Gradient Descent Algorithms

## Objective of Gradient descent

Gradient descent is a way to minimize an objective function $J( \theta )$ parameterized by a model's parameters 
{{$ 
\theta \in R^d
}}$ 
by updating the parameters in the opposite direction of the gradient of the objective function $\nabla_\thetaJ(\theta)$ with respect to the parameters. The learning rate $l$ determines the size of the steps we take to reach a (local) minimum. In other words, we follow the direction of the slope of the surface created by the objective function downhill untill we reach a valley.

## Gradient Descent Variants

### Batch Gradient descent

Batch gradient descent, computes the gradient of the cost function with respect to the parameters $\theta$ of the entire training dataset:
{{$
\theta = \theta - l . \nabla_\theta J(\theta)
}}$

BGD needs to calculate the gradients for the whole dataset to perform just one update, therefore it can be really slow and intractable for datasets that do not fit the memory. Also batch gradient descent does not allow us to update our model online, i.e. with new examples on the fly.

Example Code:
```python
for i in range(n_epochs):
    params_grad = evaluate_gradient(loss_function, parameters)
    params = params - learning_rate * params_grad
 ```
 




