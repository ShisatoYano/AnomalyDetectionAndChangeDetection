# AnomalyDetectionAndChangeDetection
---
Reading Log about a book, "Anomaly Detection and Change Detection"

## Table of contents
---
<!-- TOC -->

- [AnomalyDetectionAndChangeDetection](#anomalydetectionandchangedetection)
    - [Table of contents](#table-of-contents)
    - [Introduction](#introduction)
    - [Author](#author)
    - [Chapter1: The basic way of thinking about Anomaly Detection and Change Detection](#chapter1-the-basic-way-of-thinking-about-anomaly-detection-and-change-detection)
        - [Case of labeled data](#case-of-labeled-data)
        - [Case of unlabeled data](#case-of-unlabeled-data)
        - [Performance evaluation](#performance-evaluation)
        - [Break-even accuracy](#break-even-accuracy)
        - [ROC Curve(Receiver Operating Characteristic Curve)](#roc-curvereceiver-operating-characteristic-curve)

<!-- /TOC -->

## Introduction
---
This book is explaining about practical technologies of anomaly detection and change detection systematically based on the latest machine learning technologies. I extracted some important points which I was impressed and wrote them as memo in this article.  

## Author
---
* [Tsuyoshi Ide](http://ide-research.net/)
* [Masashi Sugiyama](http://www.ms.k.u-tokyo.ac.jp/sugi/)

## Chapter1: The basic way of thinking about Anomaly Detection and Change Detection
---
* The fundamental difference from the traditional way of thinking about AI is expressing the knowledges with not the words like a human but the words of probability.  

* The most important point of anomaly detection and change detection based on statistical machine learning is how to learn probability distribution depend on a property of data and how to define the difference levels of anomaly and change.  

### Case of labeled data

* Observed train data
$M$ dimension vector $\bm{x}$ and label $y$ which means anomaly or normal.  
$$
  \bm{D} = \{(x^{(1)},y^{(1)}), (x^{(2)},y^{(2)}), \cdots, (x^{(N)},y^{(N)})\}
$$
It is natural for us to think a different probability distribution depend on anomaly or normal, in other words, conditional distribution $p(x|y)$.  

* Anomaly score definition
$$
    a(x')=ln\frac{p(x'|y=1,D)}{p(x'|y=0,D)}
$$
If $p(x'|y=1,D)$ is superior to $p(x'|y=0,D)$, the label will be judged as anomaly.  
$ln$ meas natural logarithm. In the above definition, it is essential that anomaly score is defined as probability distribution ratio, in other words, density ratio or likelihood ratio. This is called "Neyman-Pearson decision rule" as follow.  

* Neyman - Pearson decision rule
If $ln\frac{p(x'|y=1,D)}{p(x'|y=0,D)}$ is over than a specified threshold, it will be judged as anomaly.  

### Case of unlabeled data
* Observed train data
$M$ dimension vector $\bm{x}$ and label $y$ which means anomaly or normal.  
$$
  \bm{D} = \{x^{(1)}, x^{(2)}, \cdots, x^{(N)}\}
$$
In this case, it is required that $D$ doesn't include any anomaly samples or s few ones to create a anomaly judging model. This is called "normal state model".  

* Anomaly score definition
Anormaly score is defined as negative log-likelihood. This definition ignore probability distribution of anomal state. 
$$
  a(x') = -ln p(x'|D)
$$

### Performance evaluation

* All of collected data is devided into "Training data" and "Validation data".  

* Cross validation:  
  * For example, one fifth of all is extracted as Training data at random and four fifth of all is used for Validation data.  
  * This validation is iterated 5 times and an average value of evaluation index.  

* Leave-one-out cross validation:  
  * In case of outlier detection  
  * When we have $N$ data, model is created with $N-1$ data and the rest, 1 data is used for validation.  
  * This validaton is iterated $N$ times.  

* Normal sample accuracy:  
  * Denominator: total number of normal sample in fact  
  * Numerator: number of sample judged as normal correctly  

* Anomalous sample accuracy:  
  * Denominator: total number of anomalous sample in fact  
  * Numerator: number of sample judged as anomalous correctly  

### Break-even accuracy

* When we compare different methods of performance, this index can express the performance with a single value. In other words, it is called "Break-even point".  

* Harmonic mean(Normal sample accuracy:$r_0$, Anomalous sample accuracy:$r_1$):  
$$
  f = \frac{2 r_0 r_1}{r_0 + r_1}
$$

* It is useful for us to calculate $f$ at different threshold and select a point which maximize the $f$ as Break-even point.  

### ROC Curve(Receiver Operating Characteristic Curve)

* In a case of anomaly detection or 2 patterns classification, an index based on ROC Curve is popular.  

* Threshold:$\tau$, $X-Y$ 2 dimension  
$$
  (X,Y) = (1-r_0(\tau),r_1(\tau))
$$

* An area between ROC Curve and X-axis is called "AUC(Area Under Curve)" and this is used for an index to show a performance of anomaly detector.  