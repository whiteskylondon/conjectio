---
date: 2020-05-04T17:00:32Z
hero_image: "/content/images/lin-mei-NYyCqdBOKwc-unsplash.jpg"
title: Using NLP and LDA to map the evolution of the Neural Information Processing
  Systems conference
author: Daniel Roy

---
What’s interesting with NLP, is that you rarely see it mixed with time series analysis. So, in this post, we looked into examining topics changes over a period of time. We used here the dataset produced by Ben Hammer on the Neural Information Processing Systems conference, available [here](https://www.kaggle.com/benhamner/nips-papers). To paraphrase him, the NIPS symposium is ’_one of the top machine learning conferences in the world. It covers topics ranging from deep learning and computer vision to cognitive science and reinforcement learning_’. Solely using sci-kit, how can we determine the evolution of the subjects treated?

The dataset is super clean and we solely focused onto the papers titles. The set starts in 1989. finishes in 2017, the most recent year with complete records. We’re picking here 2010 and 2017 to compare the subjects. [All the code is available in our Kaggle’s kernel](https://www.kaggle.com/danielroyblackdiam/kernel2805e7026d/edit).

First conclusion: there's an explosion of papers! 631 in 2017 compared to 221 in 2010. Secondly, a simple bag of words count show that some of the key words in 2017 were not even covered in 2010, such as 'deep' \['learning'\].

At this point, we have to specify we obviously removed the usual stop words but their data-science equivalent such as ‘data’, ‘large’, ‘learning’ and ‘models’ which are either occurring extremely frequently or were not bringing a lot of information.

![](/content/images/Plot 3 (2).png)

This first chart has the problem to be distorted by the largest amount of publications in 2017. So we've normalised each subject, by dividing it by the sum of the subjects covered.

![](/content/images/Plot 6 (1).png)

The results are now incredibly clearer. What was popular in 2010 was a lot less in favour in 2017 and the most treated subjects in 2017 were barely treated in 2010. Terms like 'bayesian', 'classification', 'regression' lost in popularity while 'neural', 'networks', 'deep', 'gradient' became ubiquitous.

> _Data shows clearly how the machine learning field diverged away from statistics to move into pure algorithmic, sample based, solutions_

Another way to illustrate this is by running Latent Dirichlet Allocation on the corpus of subjects. LDA always provide subjects which are slightly surrealists, but however quite demonstrating the underlying subject surface.

    # Load the LDA model from sk-learn
    from sklearn.decomposition import LatentDirichletAllocation as LDA
     
    # Helper function
    def print_topics(model, count_vectorizer, n_top_words):
        words = count_vectorizer.get_feature_names()
        for topic_idx, topic in enumerate(model.components_):
            print("\nTopic #%d:" % topic_idx)
            print(" ".join([words[i]
                            for i in topic.argsort()[:-n_top_words - 1:-1]]))
            
    # Tweak the two parameters below (use int values below 15)
    number_topics = 5
    number_words = 5
    
    
    # Create and fit the LDA model
    lda = LDA(n_components=number_topics)
    lda.fit(count_data)
    
    
    # Print the topics found by the LDA model
    print("Topics found via LDA:")
    
    print_topics(lda, count_vectorizer, number_words)

And the outcome, here too, shows well the underlying reality. Machine Learning is now less probabilistic and more neural, deep, network driven.

![](/content/images/Screenshot 2020-05-04 at 17.10.56.png)

As a field, the analysis of variations of text data across time seems to be open. On one side stand the time-series librairies and tools (scikit, pandas) and on the other the pure NLP: gensim, nltk and the excellent spaCy.

To give credit were credits are due, this piece of work was freely interpreted from _The Hottest Topics in Machine Learning_ on [Datacamp](https://www.datacamp.com/?tap_a=5644-dce66f&tap_s=880795-41d646&utm_medium=affiliate&utm_source=danielroy1) by @larshulstaert.