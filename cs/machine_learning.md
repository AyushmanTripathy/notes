# Machine Learning

from [Fundamentals of Machine Learning](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)

```
y = f(x)
```

-   y is the `label`
-   x is a vector called `features`
-   f is the function that is fitted to the data
-   coming up with f is called `training`
-   using the model (f) is called `inferencing`

types of ML are

## Supervised Machine Learning

training data includes features and labels
process is

1. Split training data
1. use an algorithim to fit training data to model
1. test accuracy of the model on testing data
1. repeat with different algorithims and parameters to get an acceptable accuracy

### Regression

label predicted is numeric value
example algorithim is `linear regression`
evaluation metrics are

1. Mean Absolute Error (average of errors)
2. Mean Squared Error (amplifies larger errors)
3. Root Mean Squared Error (error interms of label)

-   consistently wrong by small amounts is desirable

#### Coefficient of determination (R^2)

```
R^2 = 1 - (sum of (y - predicted_y)^2) / (sum of (y - mean_y)^2)
```

-   in [0, 1]
-   decribes proportion of variance explained by model
-   because there can be some natural random variance in the data
-   closer to 1, better model is fitting to testing data

#### Iterative training

-   features selection and preparation
-   algorithim selection
-   setting algorithim parameters (`hyperparameters`)

after multiple iterations, model results in best evaluation metric

## Classification

label represents a categorization or class

### Binary Classification

predicting a true or false
example algorithim is `logistic regression` (sigmoid)
evaluation metrics are

| predicted | actual | called         |
| --------- | ------ | -------------- |
| 0         | 0      | true negetive  |
| 1         | 0      | false positive |
| 0         | 1      | false negetive |
| 1         | 1      | true positive  |

1. Accuracy

```
(TN + TP) / (TN + TP + FP + FN)
```

-   fails if no of positives is less in data

2. Recall

```
TP / (TP + FN)
```

-   also called true positive rate
-   model correctly identifies what % of true cases

3. Precision

```
TP / (TP + FP)
```

-   true prediction is % correct

4. F1 score

```
(2 * precision * recall) / (precision + recall)
```

#### Received Operator Characteristics (ROC)

graph ploting true positive rate with false positive rate for every threshold value

-   randomly guessing would be you a diagonal line through origin
-   area under the curve will be 0.5 for random
-   perfect model would be a right angle
-   area under the curve will be 1 for prefect

### Multiclass Classification

predict form multiple possible classes the most possible class
need to calculate probability value for each class

1. One-vs-Rest (OvR) algorithims

-   calculate probability of each class separetly
-   separate function for all

2. Multinomial algorithims

-   probability of each class which add up to 1
-   example algorithim is `softmax`
-   overall accuracy, recall, precision and F1 can be calculated from sum of TN, TP, FN, FP

## Unsupervised Machine Learning

training data inclues only features

### Clustering

label is the cluster which observation is assigned
example algorithim is `K-means`, which is

1. features are n dimensional coordinates
1. deciding how many clusters we want, the k
1. k points are plotted at random, called centroids
1. each data point is assigned to nearest centroid
1. each centroid is moved to center of its data points
1. last 2 steps repeated untill clusters become stable or maximum iteration is reached.

#### Evaluation of cluster model

since no labels, evaluation depends on how well resulting clusters are separated

1. Average distance to cluster center
1. Average distance to other cluster centers
1. Maximum distance to cluster center
1. Silhouette (ratio of distance between points in same and different clusters,1 is more separation)

---

## Deep Learning

emulates the way human brains learn
Neural Networks consists of multiple layers of neurons, (a deeply nested function)

each neuron has

1. weight for each neuron in the layer before it
1. `activation function` which determines if meets the threshold to be passed to next layer

### Loss function

-   aggregate difference between predicted and know values
-   these values are vectors containing the output layer

### Learning

-   since entire network is a large nested function
-   using differential calculus to each weight is adjusted to minimize loss function
-   these optimisations involves a `gradient descent` approach
-   changes to weights are `backpropagated` through the network
-   repeated for `epochs` (iterations) untill loss is minimized

# Large Language Models

ML models for natural language processing tasks (NLP)
Transformer models are trained with large volumes of texts
Transformer model architecture consists of 

1. Encoder, creates semantic respresentation of text
1. Decoder, generates language sequences

BERT (Bidirectional Encoder Representation) by google for search engines
GPT (Generative Pretrained Transformer) by OpenAI

### Tokenization

text is divided into tokens
can be word, combination of words, punctuations
with training text, vocabulary can be increased

### Embeddings

each token has a associated numeric vector
each numeric elements represents a attribute
hence related tokens have similar embedding
