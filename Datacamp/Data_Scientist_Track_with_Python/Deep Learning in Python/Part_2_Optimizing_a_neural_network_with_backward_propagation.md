11/2017  
# Datacamp - Deep Learning in Python (Data Scientist Track with Python)  
[Deep Learning in Python](https://www.datacamp.com/courses/deep-learning-in-python)

---

***Course Description***  

Deep learning is the machine learning technique behind the most exciting capabilities in diverse areas like robotics, natural language processing, image recognition and artificial intelligence (including the famous AlphaGo). In this course, you'll gain hands-on, practical knowledge of how to use deep learning with Keras 2.0, the latest version of a cutting edge library for deep learning in Python.      

# Part 2 : Optimizing a neural network with backward propagation   

Here, you'll learn how to optimize the predictions generated by your neural networks. You'll do this using a method called backward propagation, which is one of the most important techniques in deep learning. Understanding how it works will give you a strong foundation to build from in the second half of the course.  

## How many clusters?    

For the exercises in this chapter, you'll continue working with the network to predict transactions for a bank.  

What is the error (predicted - actual) for the following network when the input data is [3, 2] and the actual value of the target (what you are trying to predict) is 5? It may be helpful to get out a pen and piece of paper to calculate these values.  

![ch2_ex2_3](https://github.com/NicoDupont/Mooc/blob/master/Datacamp/Data_Scientist_Track_with_Python/Deep%Learning%in%Python/img/ch2_ex2_3.png)

### Possible Answers  => 11

 - 5.
 - 6.
 - 11.
 - 16.

```python
```

### Results :  

Well done! The network generates a prediction of 16, which results in an error of 11.  

---


## Understanding how weights change model accuracy    

Imagine you have to make a prediction for a single data point. The actual value of the target is 7. The weight going from node_0 to the output is 2, as shown below. If you increased it slightly, changing it to 2.01, would the predictions become more accurate, less accurate, or stay the same?  

![ch2_ex2_3 (1)](https://github.com/NicoDupont/Mooc/blob/master/Datacamp/Data_Scientist_Track_with_Python/Deep%Learning%in%Python/img/ch2_ex2_3.png)

### Possible Answers => 2

 - More accurate.
 - Less accurate
 - Stay the same.

```python
```

### Results :  

Exactly! Increasing the weight to 2.01 would increase the resulting error from 9 to 9.08, making the predictions less accurate.  

---


## Coding how weight changes affect accuracy    

Now you'll get to change weights in a real network and see how they affect model accuracy!  

Have a look at the following neural network: Ch2Ex4  

![ch2ex4.png](https://github.com/NicoDupont/Mooc/blob/master/Datacamp/Data_Scientist_Track_with_Python/Deep%Learning%in%Python/img/ch2ex4.png)

Its weights have been pre-loaded as weights_0. Your task in this exercise is to update a single weight in weights_0 to create weights_1, which gives a perfect prediction (in which the predicted value is equal to target_actual: 3).  

Use a pen and paper if necessary to experiment with different combinations. You'll use the predict_with_network() function, which takes an array of data as the first argument, and weights as the second argument.  

### Instructions

 - Create a dictionary of weights called weights_1 where you have changed 1 weight from weights_0 (You only need to make 1 edit to weights_0 to generate the perfect prediction).
 - Obtain predictions with the new weights using the predict_with_network() function with input_data and weights_1.
 - Calculate the error for the new weights by subtracting target_actual from model_output_1.
 - Hit 'Submit Answer' to see how the errors compare!

```python
# The data point you will make a prediction for
input_data = np.array([0, 3])

# Sample weights
weights_0 = {'node_0': [2, 1],
             'node_1': [1, 2],
             'output': [1, 1]
            }

# The actual target value, used to calculate the error
target_actual = 3

# Make prediction using original weights
model_output_0 = predict_with_network(input_data, weights_0)

# Calculate error: error_0
error_0 = model_output_0 - target_actual

# Create weights that cause the network to make perfect prediction (3): weights_1
weights_1 = {'node_0': [2, 1],
             'node_1': [1, 0],
             'output': [1, 1]
            }

# Make prediction using new weights: model_output_1
model_output_1 = predict_with_network(input_data, weights_1)

# Calculate error: error_1
error_1 = model_output_1 - target_actual

# Print error_0 and error_1
print(error_0)
print(error_1)
```

### Results :  

Fantastic! The network now generates a perfect prediction with an error of 0.  

    <script.py> output:
        6
        0

---


## Scaling up to multiple data points      

You've seen how different weights will have different accuracies on a single prediction. But usually, you'll want to measure model accuracy on many points. You'll now write code to compare model accuracies for two different sets of weights, which have been stored as weights_0 and weights_1.  

input_data is a list of arrays. Each item in that list contains the data to make a single prediction. target_actuals is a list of numbers. Each item in that list is the actual value we are trying to predict.  

In this exercise, you'll use the mean_squared_error() function from sklearn.metrics. It takes the true values and the predicted values as arguments.  

You'll also use the preloaded predict_with_network() function, which takes an array of data as the first argument, and weights as the second argument.  

### Instructions

 - Import mean_squared_error from sklearn.metrics.
 - Using a for loop to iterate over each row of input_data:
   - Make predictions for each row with weights_0 using the predict_with_network() function and append it to model_output_0.
   - Do the same for weights_1, appending the predictions to model_output_1.
 - Calculate the mean squared error of model_output_0 and then model_output_1 using the mean_squared_error() function. The first argument should be the actual values (target_actuals), and the second argument should be the predicted values (model_output_0 or model_output_1).

```python
from sklearn.metrics import mean_squared_error

# Create model_output_0
model_output_0 = []
# Create model_output_0
model_output_1 = []

# Loop over input_data
for row in input_data:
    # Append prediction to model_output_0
    model_output_0.append(predict_with_network(row,weights_0))

    # Append prediction to model_output_1
    model_output_1.append(predict_with_network(row,weights_1))

# Calculate the mean squared error for model_output_0: mse_0
mse_0 = mean_squared_error(target_actuals,model_output_0)

# Calculate the mean squared error for model_output_1: mse_1
mse_1 = mean_squared_error(target_actuals,model_output_1)

# Print mse_0 and mse_1
print("Mean squared error with weights_0: %f" %mse_0)
print("Mean squared error with weights_1: %f" %mse_1)
```

### Results :  

Excellent work! It looks like model_output_1 has a higher mean squared error.  

    <script.py> output:
        Mean squared error with weights_0: 294.000000
        Mean squared error with weights_1: 395.062500

---


## Calculating slopes   

You're now going to practice calculating slopes. When plotting the mean-squared error loss function against predictions, the slope is 2 * x * (y-xb), or 2 * input_data * error. Note that x and b may have multiple numbers (x is a vector for each data point, and b is a vector). In this case, the output will also be a vector, which is exactly what you want.  

You're ready to write the code to calculate this slope while using a single data point. You'll use pre-defined weights called weights as well as data for a single point called input_data. The actual value of the target you want to predict is stored in target.  

### Instructions

 - Calculate the predictions, preds, by multiplying weights by the input_data and computing their sum.
 - Calculate the error, which is the difference between target and preds. Notice that this error corresponds to y-xb in the gradient expression.
 - Calculate the slope of the loss function with respect to the prediction. To do this, you need to take the product of input_data and error and multiply that by 2.

```python
# Calculate the predictions: preds
preds = (input_data*weights).sum()

# Calculate the error: error
error = preds - target

# Calculate the slope: slope
slope = 2 * input_data * error

# Print the slope
print(slope)
```

### Results :  

Well done! You can now use this slope to improve the weights of the model!  

    <script.py> output:
        [14 28 42]

---


## Improving model weights      

Hurray! You've just calculated the slopes you need. Now it's time to use those slopes to improve your model. If you add the slopes to your weights, you will move in the right direction. However, it's possible to move too far in that direction. So you will want to take a small step in that direction first, using a lower learning rate, and verify that the model is improving.  

The weights have been pre-loaded as weights, the actual value of the target as target, and the input data as input_data. The predictions from the initial weights are stored as preds.  

### Instructions

 - Set the learning rate to be 0.01 and calculate the error from the original predictions. This has been done for you.
 - Calculate the updated weights by subtracting the product of learning_rate and slope from weights.
 - Calculate the updated predictions by multiplying weights_updated with input_data and computing their sum.
 - Calculate the error for the new predictions. Store the result as error_updated.
 - Hit 'Submit Answer' to compare the updated error to the original!

```python
# Set the learning rate: learning_rate
learning_rate = 0.01

# Calculate the predictions: preds
preds = (weights * input_data).sum()

# Calculate the error: error
error = preds - target

# Calculate the slope: slope
slope = 2 * input_data * error

# Update the weights: weights_updated
weights_updated = weights - (learning_rate*slope)

# Get updated predictions: preds_updated
preds_updated = (weights_updated * input_data).sum()

# Calculate updated error: error_updated
error_updated = preds_updated - target

# Print the original error
print(error)

# Print the updated error
print(error_updated)
```

### Results :  

Fantastic! Updating the model weights did indeed decrease the error!  

    <script.py> output:
        7
        5.04

---


## Making multiple updates to weights     

You're now going to make multiple updates so you can dramatically improve your model weights, and see how the predictions improve with each update.  

To keep your code clean, there is a pre-loaded get_slope() function that takes input_data, target, and weights as arguments. There is also a get_mse() function that takes the same arguments. The input_data, target, and weights have been pre-loaded.  

This network does not have any hidden layers, and it goes directly from the input (with 3 nodes) to an output node. Note that weights is a single array.  

We have also pre-loaded matplotlib.pyplot, and the error history will be plotted after you have done your gradient descent steps.  

### Instructions

 - Using a for loop to iteratively update weights:
   - Calculate the slope using the get_slope() function.
   - Update the weights using a learning rate of 0.01.
   - Calculate the mean squared error (mse) with the updated weights using the get_mse() function.
   - Append mse to mse_hist.
 - Hit 'Submit Answer' to visualize mse_hist. What trend do you notice?

```python
n_updates = 20
mse_hist = []

# Iterate over the number of updates
for i in range(n_updates):
    # Calculate the slope: slope
    slope = get_slope(input_data, target, weights)

    # Update the weights: weights
    weights = weights - (0.01 * slope)

    # Calculate mse with new weights: mse
    mse = get_mse(input_data, target, weights)

    # Append the mse to mse_hist
    mse_hist.append(mse)

# Plot the mse history
plt.plot(mse_hist)
plt.xlabel('Iterations')
plt.ylabel('Mean Squared Error')
plt.show()
```

### Results :  

![graph1](https://github.com/NicoDupont/Mooc/blob/master/Datacamp/Data_Scientist_Track_with_Python/Deep%Learning%in%Python/img/graph1.svg)

---


## The relationship between forward and backward propagation     

If you have gone through 4 iterations of calculating slopes (using backward propagation) and then updated weights, how many times must you have done forward propagation?  

### Possible Answers  => 3 (4)

 - 0.
 - 1.
 - 4.
 - 8.

```python
```

### Results :  

Exactly! Each time you generate predictions using forward propagation, you update the weights using backward propagation.  

---


## Thinking about backward propagation    

If your predictions were all exactly right, and your errors were all exactly 0, the slope of the loss function with respect to your predictions would also be 0. In that circumstance, which of the following statements would be correct?  

### Possible Answers => 1

 - The updates to all weights in the network would also be 0.
 - The updates to all weights in the network would be dependent on the activation functions.
 - The updates to all weights in the network would be proportional to values from the input data.

```python
```

### Results :  

Correct! In this situation, the updates to all weights in the network would indeed also be 0.  

---


## How many clusters?    

In the network shown below, we have done forward propagation, and node values calculated as part of forward propagation are shown in white. The weights are shown in black. Layers after the question mark show the slopes calculated as part of back-prop, rather than the forward-prop values. Those slope values are shown in purple.    

This network again uses the ReLU activation function, so the slope of the activation function is 1 for any node receiving a positive value as input. Assume the node being examined had a positive value (so the activation function's slope is 1).    

![ch2ex14_1](https://github.com/NicoDupont/Mooc/blob/master/Datacamp/Data_Scientist_Track_with_Python/Deep%Learning%in%Python/img/ch2ex14_1.png)

What is the slope needed to update the weight with the question mark?  

![ch2ex14_2](https://github.com/NicoDupont/Mooc/blob/master/Datacamp/Data_Scientist_Track_with_Python/Deep%Learning%in%Python/img/ch2ex14_2.png)

### Possible answers => 3 (6)

 - 0.
 - 2.
 - 6.
 - Not enough information.

```python
```

### Results :  

Well done! The slope needed to update this weight is indeed 6. You're now ready to start building deep learning models with keras!  

---