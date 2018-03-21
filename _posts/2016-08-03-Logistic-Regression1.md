---
layout: post
title:  "Logistic Regression"
categories: blog 
tags: [regression, logistic regression, classification, basic theories]
---
Logistic regression is a regression model where the outcome is categorical (mostly binary).

More concept and description can be found in [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression). Basically, the key part of logistic regression is: 

<img src="https://latex.codecogs.com/gif.latex?log\frac{p(\mathbf{x})}{1-p(\mathbf{x})}=\beta_0&space;&plus;&space;\boldsymbol{\beta}\mathbf{x}" title="log\frac{p(\mathbf{x})}{1-p(\mathbf{x})}=\beta_0 + \boldsymbol{\beta}\mathbf{x}" />,

where, <img src="https://latex.codecogs.com/gif.latex?p(\mathbf{x})&space;=&space;Pr(Y=1|X=\mathbf{x})" title="p(\mathbf{x}) = Pr(Y=1|X=\mathbf{x})" />. 

The logistic transformation makes both sides unbounded, thus avoiding nonsensical results.
 
Maximum likelihood estimation can be used to fitting the model and Newton’s method can be applied to the optimization.
 
Since the right-hand side of the regression equation is linear, logistic regression is considered to be a linear classifier. Its decision boundary can be clearly seen from the following figures. In the figures, three datasets are tested and the classification accuracy is 0.88, 0.42, and 0.97 respectively (source codes attached). Obviously, the decision boundary is linear. 

![](https://github.com/jay15summer/jay15summer.github.io/blob/master/images/logistic-regression1.png?raw=true)

```python
# Decision boundaries of logistic regression
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.colors import ListedColormap
from sklearn.cross_validation import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.datasets import make_moons, make_circles, make_classification
from sklearn.linear_model import LogisticRegression

h = .01  # step size in the mesh

names = ["Logistic Regression"
         ]
classifiers = [LogisticRegression(penalty='l1', C=1)
               ]


X, y = make_classification(n_features=2, n_redundant=0, n_informative=2,
                           random_state=1, n_clusters_per_class=1)
rng = np.random.RandomState(2)
X += 2 * rng.uniform(size=X.shape)
linearly_separable = (X, y)

datasets = [make_moons(noise=0.3, random_state=0),
            make_circles(noise=0.2, factor=0.5, random_state=1),
            linearly_separable
            ]

figure = plt.figure(figsize=(27, 9))
i = 1
# iterate over datasets
for ds in datasets:
    # split into training and test
    X, y = ds
    X = StandardScaler().fit_transform(X)
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=.4)

    x_min, x_max = X[:, 0].min() - .5, X[:, 0].max() + .5
    y_min, y_max = X[:, 1].min() - .5, X[:, 1].max() + .5
    xx, yy = np.meshgrid(np.arange(x_min, x_max, h),
                         np.arange(y_min, y_max, h))

    # plot the dataset first
    cm = plt.cm.RdBu
    cm_bright = ListedColormap(['#FF0000', '#0000FF'])
    ax = plt.subplot(len(datasets), len(classifiers) + 1, i)
    # Plot the training points
    ax.scatter(X_train[:, 0], X_train[:, 1], c=y_train, cmap=cm_bright)
    # and testing points
    ax.scatter(X_test[:, 0], X_test[:, 1], c=y_test, cmap=cm_bright, alpha=0.6)
    ax.set_xlim(xx.min(), xx.max())
    ax.set_ylim(yy.min(), yy.max())
    ax.set_xticks(())
    ax.set_yticks(())
    i += 1

    # iterate over classifiers (Here we only have one, more can be added)
    for name, clf in zip(names, classifiers):
        ax = plt.subplot(len(datasets), len(classifiers) + 1, i)
        clf.fit(X_train, y_train)
        score = clf.score(X_test, y_test)

        # Plot the decision boundary.
        if hasattr(clf, "decision_function"):
            Z = clf.decision_function(np.c_[xx.ravel(), yy.ravel()])
        else:
            Z = clf.predict_proba(np.c_[xx.ravel(), yy.ravel()])[:, 1]

        # Put the result into a color plot
        Z = Z.reshape(xx.shape)
        ax.contourf(xx, yy, Z, cmap=cm, alpha=.8)

        # Plot also the training points
        ax.scatter(X_train[:, 0], X_train[:, 1], c=y_train, cmap=cm_bright)
        # and testing points
        ax.scatter(X_test[:, 0], X_test[:, 1], c=y_test, cmap=cm_bright,
                   alpha=0.6)

        ax.set_xlim(xx.min(), xx.max())
        ax.set_ylim(yy.min(), yy.max())
        ax.set_xticks(())
        ax.set_yticks(())
        ax.set_title(name)
        ax.text(xx.max() - .3, yy.min() + .3, ('%.2f' % score).lstrip('0'),
                size=15, horizontalalignment='right')
        i += 1

figure.subplots_adjust(left=.02, right=.98)
plt.show()
```
