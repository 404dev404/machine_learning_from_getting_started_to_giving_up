# Supervised Learning

## Introduction

The goal in supervised learning is to make *predictions from data*. For example, one popular application of supervised learning is email filtering. Here, an email (the data instance) needs to be classified as *spam* or *not-spam*. Following the approach of traditional computer science, one might be tempted to write a carefully designed program that follows some rules to decide if an email is spam or not. Although such a program might work reasonably well for a while, it has significant drawbacks. As email spam changes it would have to be rewritten. Spammers could attempt to reverse engineer the software and design messages that circumvent it. And even if it is successful, it could probably not easily be applied to different languages. Machine learning uses a different approach to generate a program that can make predictions from data. Instead of programming it by hand it is *learned* from past data. This process works if we have data instances for which we know exactly what the right prediction would have been. For example past data might be user-annotated as spam or not-spam. A machine learning algorithm can utilize such data to learn a program, a *classifier*, to predict the correct *label* of each annotated data instance. Other successful applications of machine learning include web-search ranking (predict which web-page the user will click on based on his/her search query), placing of online advertisements (predict the expected revenue of an ad, when placed on a homepage, which is seen by a specific user), visual object recognition (predict which object is an image -- e.g. a camera mounted on a self-driving car), face-detection (predict if an image patch contains a human face or not).

## Setup

Let us formalize the supervised machine learning setup. Our training data comes in pairs of inputs <a href="https://www.codecogs.com/eqnedit.php?latex=(\mathbf{x},&space;y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(\mathbf{x},&space;y)" title="(\mathbf{x}, y)" /></a>, where <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}&space;\in&space;\mathcal{R}^d" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}&space;\in&space;\mathcal{R}^d" title="\mathbf{x} \in \mathcal{R}^d" /></a> is the input instance and <a href="https://www.codecogs.com/eqnedit.php?latex=y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y" title="y" /></a> is its label. The entire training data is denoted as

<a href="https://www.codecogs.com/eqnedit.php?latex=D=\{&space;(\mathbf{x}_1,&space;y_1),&space;\ldots,&space;(\mathbf{x}_n,&space;y_n)&space;\}&space;\subseteq&space;\mathcal{R}^d&space;\times&space;\mathcal{C}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D=\{&space;(\mathbf{x}_1,&space;y_1),&space;\ldots,&space;(\mathbf{x}_n,&space;y_n)&space;\}&space;\subseteq&space;\mathcal{R}^d&space;\times&space;\mathcal{C}" title="D=\{ (\mathbf{x}_1, y_1), \ldots, (\mathbf{x}_n, y_n) \} \subseteq \mathcal{R}^d \times \mathcal{C}" /></a>

where:

- <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{R}^d" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{R}^d" title="\mathcal{R}^d" /></a> is the d-dimensional feature space
- <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i" title="\mathbf{x}_i" /></a> is the input vector of the <a href="https://www.codecogs.com/eqnedit.php?latex=i^{th}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i^{th}" title="i^{th}" /></a> sample
- <a href="https://www.codecogs.com/eqnedit.php?latex=y_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_i" title="y_i" /></a> is the label of the <a href="https://www.codecogs.com/eqnedit.php?latex=i^{th}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i^{th}" title="i^{th}" /></a> sample
- <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{C}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{C}" title="\mathcal{C}" /></a> is the label space

The data point <a href="https://www.codecogs.com/eqnedit.php?latex=(\mathbf{x}_i,&space;y_i)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(\mathbf{x}_i,&space;y_i)" title="(\mathbf{x}_i, y_i)" /></a> are drawn from some (unknown) distribution <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{P}(X,&space;Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{P}(X,&space;Y)" title="\mathcal{P}(X, Y)" /></a>. Ultimately we would like to learn a function <a href="https://www.codecogs.com/eqnedit.php?latex=h" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h" title="h" /></a> such that for a new pair <a href="https://www.codecogs.com/eqnedit.php?latex=(\mathbf{x},&space;y)&space;\sim&space;\mathcal{P}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(\mathbf{x},&space;y)&space;\sim&space;\mathcal{P}" title="(\mathbf{x}, y) \sim \mathcal{P}" /></a>, we have <a href="https://www.codecogs.com/eqnedit.php?latex=h(\mathbf{x})=y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(\mathbf{x})=y" title="h(\mathbf{x})=y" /></a> with high probability (or <a href="https://www.codecogs.com/eqnedit.php?latex=h(\mathbf{x})\approx&space;y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(\mathbf{x})\approx&space;y" title="h(\mathbf{x})\approx y" /></a>). We will get to this later. For now let us go through some examples of <a href="https://www.codecogs.com/eqnedit.php?latex=X" target="_blank"><img src="https://latex.codecogs.com/gif.latex?X" title="X" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=Y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Y" title="Y" /></a>.

### Examples of Label Spaces

There are multiple scenarios for the label space <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{C}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{C}" title="\mathcal{C}" /></a>:

| | | |
| - | - | - |
| Binary classification | <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{C}=\{&space;0,&space;1&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{C}=\{&space;0,&space;1&space;\}" title="\mathcal{C}=\{ 0, 1 \}" /></a> or <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{C}=\{&space;-1,&space;&plus;1&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{C}=\{&space;-1,&space;&plus;1&space;\}" title="\mathcal{C}=\{ -1, +1 \}" /></a> | E.g. spam filtering. An email is either spam (<a href="https://www.codecogs.com/eqnedit.php?latex=&plus;1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?&plus;1" title="+1" /></a>), or not (<a href="https://www.codecogs.com/eqnedit.php?latex=-1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?-1" title="-1" /></a>). |
| Multi-class classification | <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{C}=\{&space;1,&space;2,&space;\ldots,&space;K&space;\}&space;(K&space;\geq&space;2)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{C}=\{&space;1,&space;2,&space;\ldots,&space;K&space;\}&space;(K&space;\geq&space;2)" title="\mathcal{C}=\{ 1, 2, \ldots, K \} (K \geq 2)" /></a> | E.g. face classification. A person can be exactly one of <a href="https://www.codecogs.com/eqnedit.php?latex=K" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K" title="K" /></a> identities (e.g., 1="Barack Obama", 2="George W. Bush", etc.) |
| Regression | <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{C}=\mathbb{R}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{C}=\mathbb{R}" title="\mathcal{C}=\mathbb{R}" /></a> | E.g. predict future temperature or the height of a person. |

## Examples of Feature Vector

We call <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i" title="\mathbf{x}_i" /></a> a feature vector. Each one of its <a href="https://www.codecogs.com/eqnedit.php?latex=d" target="_blank"><img src="https://latex.codecogs.com/gif.latex?d" title="d" /></a> dimensions is a features describing the <a href="https://www.codecogs.com/eqnedit.php?latex=i^{th}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i^{th}" title="i^{th}" /></a> sample. Let us look at some examples:

- Patient Data in a hospital. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i&space;=&space;(x_i^1,&space;x_i^2,&space;\ldots,&space;x_i^d)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i&space;=&space;(x_i^1,&space;x_i^2,&space;\ldots,&space;x_i^d)" title="\mathbf{x}_i = (x_i^1, x_i^2, \ldots, x_i^d)" /></a>, where <a href="https://www.codecogs.com/eqnedit.php?latex=x_i^1=0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i^1=0" title="x_i^1=0" /></a> or <a href="https://www.codecogs.com/eqnedit.php?latex=1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?1" title="1" /></a>, may refer to the patient <a href="https://www.codecogs.com/eqnedit.php?latex=i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i" title="i" /></a>'s gender, <a href="https://www.codecogs.com/eqnedit.php?latex=x_i^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i^2" title="x_i^2" /></a> could be the height of patient <a href="https://www.codecogs.com/eqnedit.php?latex=i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i" title="i" /></a> in cm, and <a href="https://www.codecogs.com/eqnedit.php?latex=x_i^3" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i^3" title="x_i^3" /></a> may be his/her in years, etc. In this case, <a href="https://www.codecogs.com/eqnedit.php?latex=d&space;\leq&space;100" target="_blank"><img src="https://latex.codecogs.com/gif.latex?d&space;\leq&space;100" title="d \leq 100" /></a> and the feature vector is dense, i.e., the number of nonzero coordinates in <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i" title="\mathbf{x}_i" /></a> is large relative to <a href="https://www.codecogs.com/eqnedit.php?latex=d" target="_blank"><img src="https://latex.codecogs.com/gif.latex?d" title="d" /></a>.
- Text document in bag-of-words format. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i=(x_i^1,&space;x_i^2,&space;\ldots,&space;x_i^d)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i=(x_i^1,&space;x_i^2,&space;\ldots,&space;x_i^d)" title="\mathbf{x}_i=(x_i^1, x_i^2, \ldots, x_i^d)" /></a>, where <a href="https://www.codecogs.com/eqnedit.php?latex=x_i^{\alpha}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i^{\alpha}" title="x_i^{\alpha}" /></a> is the number of occurrences of the <a href="https://www.codecogs.com/eqnedit.php?latex={\alpha}^{th}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?{\alpha}^{th}" title="{\alpha}^{th}" /></a> word in a dictionary in document <a href="https://www.codecogs.com/eqnedit.php?latex=i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i" title="i" /></a> (often referred to as term frequencies). In this case, <a href="https://www.codecogs.com/eqnedit.php?latex=d&space;\sim&space;100,000&space;-&space;10M" target="_blank"><img src="https://latex.codecogs.com/gif.latex?d&space;\sim&space;100,000&space;-&space;10M" title="d \sim 100,000 - 10M" /></a> and the feature vector is sparse, i.e., <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i" title="\mathbf{x}_i" /></a> consists of mostly zeros. A common way to avoid the use of a dictionary is to use feature hashing instead of directly hash any string to a dimension index (the advantage is that no dictionary is needed, but a minor disadvantage can be that multiple words are hashed into the same dimension.) A popular inprovement over bag-of-words features is TF-IDF, which down-scales common words and highlights rare words.
- Images. Here, the features typically represent pixel values. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i&space;=&space;(x_i^1,&space;x_i^2,&space;\ldots,&space;x_i^{3k})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i&space;=&space;(x_i^1,&space;x_i^2,&space;\ldots,&space;x_i^{3k})" title="\mathbf{x}_i = (x_i^1, x_i^2, \ldots, x_i^{3k})" /></a>, where <a href="https://www.codecogs.com/eqnedit.php?latex=x_i^{3j-2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i^{3j-2}" title="x_i^{3j-2}" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=x_i^{3j-1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i^{3j-1}" title="x_i^{3j-1}" /></a>, and <a href="https://www.codecogs.com/eqnedit.php?latex=x_i^{3j}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i^{3j}" title="x_i^{3j}" /></a> refer to the red, green, and blue values of the <a href="https://www.codecogs.com/eqnedit.php?latex=j^{th}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?j^{th}" title="j^{th}" /></a> pixel in the image. In this case, <a href="https://www.codecogs.com/eqnedit.php?latex=d&space;\sim&space;100,000&space;-&space;10M" target="_blank"><img src="https://latex.codecogs.com/gif.latex?d&space;\sim&space;100,000&space;-&space;10M" title="d \sim 100,000 - 10M" /></a> and the feature fector is dense. A <a href="https://www.codecogs.com/eqnedit.php?latex=7MP" target="_blank"><img src="https://latex.codecogs.com/gif.latex?7MP" title="7MP" /></a> camera results in <a href="https://www.codecogs.com/eqnedit.php?latex=7M&space;\times&space;3&space;=&space;21M" target="_blank"><img src="https://latex.codecogs.com/gif.latex?7M&space;\times&space;3&space;=&space;21M" title="7M \times 3 = 21M" /></a> features.

























