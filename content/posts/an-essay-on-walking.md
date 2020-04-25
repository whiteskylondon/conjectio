---
date: 2020-04-25T22:43:31Z
title: Recreating Cambridge Analytica Python stack
author: Daniel Roy
hero_image: "/content/images/ca_scikit_02.jpeg"

---
Spend time working with scitkit-learn and you’ll be amazed at the sum of knowledge available at the help of only a few lines of code. However, similarly to browsing a restaurant menu made of hundred of pages, the choice can be, quite simply, overwhelming at time. I tried to narrow down a selection based on a case study: to recreate Cambridge Analytica’s Python stack.

**On the methodology**

To start with, I dived into the following sources.

The starting point was the excellent “_Weapons of Micro Destruction: How Our ‘Likes’ Hijacked Democracy_” post of Dave Smith, posted at the end of 2018 on Towards Data Science: https://towardsdatascience.com/weapons-of-micro-destruction-how-our-likes-hijacked-democracy-c9ab6fcd3d02
A former job offer “Cambridge Analytica Lead Data Scientist Job Description”: https://pastebin.com/LMKN64Da
The explicit “Private traits and attributes are predictable from digital records of human behavior” paper, referenced by many sources as a key-stone behind CA’s architecture: https://www.pnas.org/content/pnas/110/15/5802.full.pdf
Data’s far more valuable than models because if you have the data it’s very easy to build models — because models use just a few well understood statistical techniques to make them. I was able to go from not doing machine learning to knowing what I need to know in one week. That’s all it took. — Aleksandr Kogan

All in all, our intuition is that CA was using scikit-learn in its stack. This intuition is reinforced by the job offer above, for the CA head of Data Science. The job offer was apparently posted in January 2018. We can’t confirm its authenticity, but if it is, that gives us some pretty good insights on the tools used:

* scikit-learn
* SciPy 
* SQL 
* Hadoop 
* Spark


So, Hadoop was used for storing and retrieving data sets across clusters. Spark was used for data processing and, more precisely, I suppose PySpark. For now, we will leave the Data Storage questions aside and we will focus onto scikit-learn.

Recreating CA method with sci-kit algos

Time to start the ground work. And to go through the sci-kit documentation

https://scikit-learn.org/stable/_downloads/scikit-learn-docs.pdfTo resume: on one side CA had users, a list of likes for each user and, for a subset of the users, the corresponding OCEAN scores, on the big five personality traits:

* Openness to experience (inventive/curious vs. consistent/cautious)
* Conscientiousness (efficient/organized vs. easy-going/careless)
* Extroversion (outgoing/energetic vs. solitary/reserved) Agreeableness
* (friendly/compassionate vs. challenging/detached) Neuroticism 
* (sensitive/nervous vs. secure/confident) If curious, you can get yours here https://www.truity.com/test/big-five-personality-test

If we first focus on the first subset of users, i.e. the users replying to the psychometrics survey, we have a large and spare matrix (n users in millions, m pages in the hundreds of thousands corresponding to the x observation) with, for each users, a few hundreds of likes (170 in average in Kosinskia, Stillwella and Graepelb work in 2012) all theses corresponding to the observed Y values. A very sparse data-frame indeed.

Intuitively this calls for singular value decomposition and redundancy elimination, passing the whole dataset (and therefore not using IncrementalPCA), a procedure explaining the use of Hadoop/PySpark for the infrastructure.

**Dimensionality Reduction and Cross Decomposition**

The first idea would be to use PCA. However PCA lacks explanatory power. And being able to target some specific pages combination was key to CA strategy. Enters Linear and Quadratic Discriminant Analysis. As per scikit documentation “Linear Discriminant Analysis (LDA) tries to identify attributes that account for the most variance between classes. In particular, LDA, in contrast to PCA, is a supervised method, using known class labels.” And indeed CA had class labels with the OCEAN scores.

Linear Discriminant Analysis can only learn linear boundaries, while Quadratic Discriminant Analysis learn quadratic boundaries and is therefore more flexible.

Another avenue to explore is cross decomposition algorithms as they find “the fundamental relations between two matrices (X and Y). They are latent variable approaches to modeling the covariance structures in these two spaces. They will try to find the multidimensional direction in the X space that explains the maximum variance direction in the Y space”

**_scikit tools_**

    from sklearn import decomposition
    from sklearn.cross_decomposition import PLSCanonical, PLSRegression, CCA
    from sklearn.discriminant_analysis import LinearDiscriminantAnalysis, QuadraticDiscriminantAnalysis

**Linear Models**

However, according to Smith’s Medium publication we shall look into Linear models, supported by a quote of Aleksandr Kogan

“Instead of doing SVD, we did a LASSO regression instead, and that improved our accuracy.”

Linear LASSO, standing for ‘Least Absolute Shrinkage’ and ‘Selection Operator’, is equally easily interpretable. Search LASSO in the scikit documentation and you will get 691 references. Smith’s publication goes in incredible depth into the behaviour of the algorithm and scikit-learn has an range of variants of the LASSO: LassoLars, LassoCV, LassoLarsIC.

    scikit tools

    from sklearn.linear_model import Lasso

    from sklearn.linear_model import LassoCV

    from sklearn.linear_model import LassoLarsCV

**The clustering approach**

Finally at a higher, more representative level, clustering could have been a simple(r) approach to produce ‘populations’ and tailor the messages accordingly. It might have missed, however, the granularity that CA was aiming at getting. Though it would have been interesting to see if the linear approaches, applied on subsets of the larger population would have yielded different results (and of course, I don’t discuss here the ethic of the approach).

scikit tools

from sklearn.cluster import KMeans

from sklearn.tree import DecisionTreeClassifier

from sklearn.ensemble import RandomForestClassifier

**Last thoughts**

Trying my luck, I searched for ‘Cambridge Analytica’ on Github. You never know… You’ll retrieve 19 repositories, all irrelevant. However some media stories indicate that Aggregate IQ did a lot of algorithmic work on the behalf of CA and their algos leaked. I could not find the but I did not spend a lot of time on the issue either.

AIQ’s was indeed building - for CA’s account - some apps for Ted Cruz and Texas Governor Greg Abbott, as well as a Ukrainian steel magnate named Serhiy Taruta. The piece of software was oh so elegantly called Ripon a reference to the town of Ripon, Wisconsin, birthplace of the Republican Party. That code is maybe laying somewhere.

Finally, did CA use Natural Language Processing? Well if we focus onto Robert Mercer, one of the shareholders of CA we see that Mercer made its money working at Renaissance Technologies from 1993 - RenTec is possibly the world’s best performing hedge fund, only using algorithmic and high-frequency trading. However, before that, Mercer was working at IBM where he did produce significant results on NLP and machine translation. A Google patent search shows his name is on 32 of IBM’s NLP patents.

https://patents.google.com/?inventor=robert+mercer&assignee=International+Business+Machines+Corporation

You will find here an interesting, and quite candid, talk of Mercer about Automatic Machine Translation and his work at Renaissance, given at John Hopkins in 2013.

http://cs.jhu.edu/\~post/bitext/

I have not seen anything letting us infer that CA was using NLP at any point. However it’ll be interesting to see if Mercer is currently invested in any NLP related companies.