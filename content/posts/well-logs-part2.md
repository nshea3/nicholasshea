---
title: "Well Logs Part 2"
date: 2019-07-15T11:35:57-07:00
draft: True
---

This is a continuation of [my first post on the SEG Facies Classification competition.](/posts/post-2-well-logs)

In the previous post I left off before implementing a baseline learner to see what results we might expect.

## Baseline Learner

I like to use depth-1 decision stumps and shallow decision trees as a first learner. Decision trees are easily interpretable once plotted. They also give us a sense of feature importance, since the greedy algorithm will split the more informative features earlier in the tree. 

Plotting decision trees has usually been a major pain point. Scikit-learn has plotting functionality, but it is dependent on graphviz. I've never successfully installed graphviz on Windows and I've tried several times. I was glad to find a package called [dtreeplt](https://github.com/nekoumei/dtreeplt) that can use matplotlib to create the trees. I've made a couple of improvements and I have a pull request out, though you're free to [download my version](https://github.com/nshea3/dtreeplt) and install it in developer mode (pip install -e).

Fully visualized: 

### Depth 1 decision tree: 

![Decision stub](https://i.imgur.com/PzTzsIc.png) 

We split first on the nonmarine/marine feature. This is reasonable because nonmarine and marine are supersets of the facies (Facies 1, 2, 3 are nonmarine, etc.), so splitting the data into nonmarine and marine puts our 9 classes into 2 distinct, non-overlapping groups (a single facies is either marine or non-marine). Intuitively, this results in much more "pure" nodes, and it's an important observation to make. If we have a sample that we know to be marine (or nonmarine), we've already eliminated about half of the possible labels!

### Decision tree

![Full decision tree](https://i.imgur.com/LCHU9m9.png)

The full decision tree starts to split on the physical wireline logs (neutron and gamma ray). At this depth, the tree is still not able to , but we are reaching the limits in terms of effectively visualizing the tree.

The practical decision tree learner has max_depth = 9, compared to max_depth = 2 for the tree pictured above. The tree does not overfit, surprisingly, though the cross validation accuracy is ultimately not competitive with 

![Practical decision tree](https://i.imgur.com/NklaA8m.png)

## Ensemble Learners

I was finally able to control overfitting. Initally, all of my learning curves looked like this:

![Learning curve](https://i.imgur.com/ttvbmow.png)
*Not great*

Clearly the learners here are fitting noise in the training data, so they classify every training sample perfectly and then fail to generalize to the cross-validation sample. 

By constraining the grid search parameters (max depth in particular) I was finally able to produce some higher-quality models.

### Decision Tree

![Decision tree learning curve](https://i.imgur.com/owmrwJx.png)

The decision tree learning curves do not look very promising. The learner performance plateaus at just under 1500 examples in the training set. It is not clear that more data can improve the performance of this particular learner.

The large gap between the training curve and validation curve indicates that the decision tree learner has a variance issue. High variance is an unfortunate characteristic of decision tree learners. A different set of grid search parameters might produce, though at the cost of 

### Extra Trees

![Extra trees learning curve](https://i.imgur.com/0Xpt2JW.png)

The extra trees learning curves also show a plateau at around 1500 examples. More data will not improve the learner's ability to generalize. The training accuracy curve and the large gap between training and validation accuracy does indicate that the learner may be overfit, so more work to control overfitting might be worthwhile. 

### Random Forest

![Random forest learning curve](https://i.imgur.com/1AUsWZ5.png)

The random forest learner performs very well on this task. The 

### Gradient Boosted Trees

![Gradient boosted trees learning curve](https://i.imgur.com/r7Xsma7.png)

The gradient boosted trees classifier had outstanding results on this learning task. The learning curves show that the model is complex enough to continue improving as the training set size increases, but not complex enough to overfit and inflate the training accuracy to the detriment of generalization. 

I spent the most time doing hyperparameter tuning on this learner since it had the best performance before tuning. Given the gap between the training and validation curves, I believe 

## Results

| Learner                | Cross Validation           |
| :----------------------|---------------------------:|
| Decision Tree          | 0.6331                     |
| Extra Trees            | 0.7228                     |
| Random Forest          | 0.7246                     |
| Gradient Boosted Trees | 0.7304                     |

### Validation 

The validation procedure described in the contest involved a blind well, where the facies labels were witheld. Contestants would run the . Obviously, this was surprising, given the points I made in the first post about testing against a sample that is dissimilar from the training data. The teams accounted for this using leave-one-out cross validation ([`sklearn.model_selection.LeaveOneOut`](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.LeaveOneOut.html)). Ultimately, automating the facies classification task would mean deploying a machine learning model that could accept wireline logs from new wells drilled in the area and return a facies classification. In this context, validation against a blind well is a very sensible approach to judging performance. 

I borrowed the validation code from the original notebook. The procedure involves saving the results of 100 runs (with different random seed) to . 

#### Distribution of F1 score over 100 runs: 
![Performance over 100 runs](https://i.imgur.com/aJu0CWh.png)

#### Confusion matrix:
![Confusion matrix](https://i.imgur.com/94t8RwV.png)

The results here do not compare especially well to published results. The mean and maximum scores in the distribution would be in the bottom quarter of the competition. Fortunately, there are a number of different ways to improve 

Following [the literature](https://arxiv.org/abs/1808.09856), and [published results from other competitors](https://github.com/seg/2016-ml-contest/blob/master/LA_Team/Facies_classification_LA_TEAM_05_VALIDATION.ipynb), I will invest my time in feature engineering and hyperparameter tuning. I prefer to do intensive grid searching and model training in the cloud and not on my laptop, so I'll share the [Google Colab notebook](https://colab.research.google.com/drive/1uWQ7JXWiqU1t3CG-qCYmnKInrhvrUFlR). 

Interestingly, including the `depth` feature produces disastrously bad results and I was forced. I would like to explore that further as well. 

I also plan to do some unsupervised learning on this data. 