---
layout: post
title: Logistic Regression from scratch
image: img/green.jpg
author: Pranay Aryal
date: 2019-09-09T10:00:00.000Z
tags:
  - Python
---

In this articles, I will show you how to write the logistic regression algorithm from scratch.

Let's first create a function that will return the sigmoid value of any number.

If you remember, the sigmoid function is given by S(x) = e<sup>x</sup>/(e<sup>x</sup> + 1)

Let's write this in python
```py
def sigmoid(z):
    s = 1/(1 + np.exp(-z))
    return s
```

Let's write a function that will initialize our weight vector with zeros
```py
def initialize_with_zeros(dim):
    """
    dim - The dimensions of the matrix with zeros

    Returns:
    w - One dimensional array of dim zeros
    b - The intercept is an integer/float which is initialized to zero
    """

    w = np.zeros([dim, 1])
    b = 0

    return w, b
```

Now, let's write a function that does the forward propagation and computes the cost and the gradients.
We are going to be using the sigmoid function we created earlier.
```py
def propagate(w, b, X, Y):
    """

    Arguments:
    w - weight matrix
    b - intercept
    X - training array
    Y - output array

    Returns:
    grads - dictionary containing the gradient for w and the gradient for b
    cost - integer/float which is the total cost on the training set.
    """

    m = X.shape[1] ## getting the number of training examples
     
    A = sigmoid(np.dot(w.T, X) + b)

    ## creating logistic cost function
    left = Y * np.log(A)
    right = (1 - Y) * np.log(1 - A)
    ## cost has to be divided by number of training samples
    cost = -(1/m) * np.sum(left + right)

    ## computing gradients
    dw = np.dot(x, (A-Y).T)/m
    db = np.mean(A - Y)

    grads = {"dw": dw, "db": db}

    return grads, cost
```

Now let's optimize the algorithm by running multiple iterations. We will be using the `propagate()` function we just created.
```py
def optimize(w, b, X, Y, num_iterations, learning_rate, print_cost=False):
    """

    Arguments:
    w - weight
    b - intercept
    Y - The correct classes
    num_iterations - Number of iterations we want to run this
    learning_rate - Learning rate which is a hyperparameter.

    Returns:
    params - a dictionary containing the weights and biases
    grads - dictionary containing gradients

    """

    costs = []

    for i in range(num_iterations):
        grads, cost = propagate(w, b, X, Y)

        dw = grads["dw"]
        db = grads["db"]

        # w and b are updated with each iteration
        w = w - (learning_rate * dw)
        b = b - (learning_rate * db)

        # We will append the cost to the costs array for every 100 iteration
        if i % 100 == 0:
            costs.append(cost)

        if print_cost and i % 100 == 0:
            print ("Cost after iteration %i: %f" %(i, cost))
        
    params = {"w": w, "b": b}
    grads = {"dw": dw, "db": db}

    return params, grads, costs
```

Let's now write a function that will make predictions.
```py
def predict(w, b, X):
    """
    This function takes the final weights and biases and predicts on the test set

    Arguments:
    w - weight
    b - bias
    X - The data to make prediction on

    Returns:
    Y_prediction - An array containing prediction as a boolean
    """

    # Getting the number of examples
    m = X.shape[1]
    
    # Initialize with zeros
    Y_prediction = np.zeros(1, m)
    w = w.reshape(X.shape[0], 1)

    A = sigmoid(np.dot(w.T, X) + b)
    Y_prediction = (A > 0.5) * 1.00 #This will give a boolean vector

    return Y_prediction
```

Let's write the whole model.
```py
def model(X_train, Y_train, X_test, Y_test, num_iterations=2000, learning_rate=0.5, print_cost=False)
    """
    Arguments are quite self-explanatory

    Returns:
    d - dictionary containing information about the model
    """

    dim = 4
    w, b = initialize_with_zeros(dim)

    parameters, grads, costs = optimize(w, b, X_train, Y_train, num_iterations, learning_rate, print_cost)

    w = parameters["w"]
    b = parameters["b"]

    Y_prediction_test = predict(w, b, X_test)
    Y_prediction_train = predict(w, b, X_train)

    print("train accuracy: {} %".format(100 - np.mean(np.abs(Y_prediction_train - Y_train)) * 100))
    print("test accuracy: {} %".format(100 - np.mean(np.abs(Y_prediction_test - Y_test)) * 100))

    d = {
        "costs": costs,
        "Y_prediction_test": Y_prediction_test,
        "Y_prediction_train": Y_prediction_train,
        "w": w,
        "b": b,
        "learning_rate": learning_rate,
        "num_iterations": num_iterations
    }
```

I hope this will help.






