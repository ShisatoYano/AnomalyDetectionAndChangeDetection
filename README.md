# AnomalyDetectionAndChangeDetection
---
Reading Log about a book, "Anomaly Detection and Change Detection"

## Table of contents
---
<!-- TOC -->

- [AnomalyDetectionAndChangeDetection](#anomalydetectionandchangedetection)
    - [Table of contents](#table-of-contents)
    - [Introduction](#introduction)
    - [Chapter1: The basic way of thinking about Anomaly Detection and Change Detection](#chapter1-the-basic-way-of-thinking-about-anomaly-detection-and-change-detection)
        - [a case of labeled data](#a-case-of-labeled-data)
        - [a case of unlabeled data](#a-case-of-unlabeled-data)

<!-- /TOC -->

## Introduction
---
This book is explaining about practical technologies of anomaly detection and change detection systematically based on the latest machine learning technologies. I extracted some important points which I was impressed and wrote them as memo in this article.  

## Chapter1: The basic way of thinking about Anomaly Detection and Change Detection
---
* The fundamental difference from the traditional way of thinking about AI is expressing the knowledges with not the words like a human but the words of probability.  

* The most important point of anomaly detection and change detection based on statistical machine learning is how to learn probability distribution depend on a property of data and how to define the difference levels of anomaly and change.  

### a case of labeled data

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

### a case of unlabeled data
* Observed train data
$M$ dimension vector $\bm{x}$ and label $y$ which means anomaly or normal.  
$$
  \bm{D} = \{x^{(1)}, x^{(2)}, \cdots, x^{(N)}\}
$$
In this case, it is required that $D$ doesn't include any anomaly samples or s few ones to create a anomaly judging model. This is called "normal state model".  

* Anomaly score definition