+++
title = "Numeric representation of text documents: doc2vec how it works and how you implement it"
date = '2018-01-18'
tags = [ "Deep Learning", "Text Mining", "Topic Modeling", "Class17/18",]
categories = ["seminar"]
banner = "img/seminar/topic_models/textMininigKlein.png"
author = "Class of Winter Term 2017 / 2018"
disqusShortname = "https-humbodt-wi-github-io-blog"
description = " "
+++

# Introduction

# Descriptive Statistics

# Theory

# Application of doc2vec in gensim

we apply **doc2vec** on facebook posts from politicans in the German election 2017

**GOAL:** to let the model find a distinctiveness in the data, e.g. a difference between party candidates

**Approach**:

- two models **PV-DBOW** and **PV-DM**
- 100 dimensions
- for 1, 5, 10, 50 and 100 epochs
- ...

*Remember:*
one post = one doc

**Solution:**

- Gensim allows to tag documents. Our tag = name of the candidate
- model creates and trains vectors for the candidates

For clarity we omit some of the code here, but you can check out the full code [here](https://gist.github.com/panoptikum/d3023bc7619814fcea5235e0f472052c). Due to the copyrights of Facebook we cannot provide the data set here.

If you want to use the interactive plotly library in your jupyter notebook, you have to put the following lines at the beginning of your notebook:

<script src="https://gist.github.com/panoptikum/b534310edb163cf48e5681d26b1ee8e3.js"></script>

Some other libraries are needed as well:

<script src="https://gist.github.com/panoptikum/e3a6774155c2e93e64f253d5faf2e1ad.js"></script>

we set our working, data and model directory:

<script src="https://gist.github.com/panoptikum/31d6fbf4ea29fd80c307812dcd7d041e.js"></script>

we load the data that we've cleaned a bit before (e.g. removal of facebook posts without text):

<script src="https://gist.github.com/panoptikum/6afdf5ce59b0b6b7ec1f6fe8c2766065.js"></script>

Party names are a quite distinctive pattern, so we remove them beforehand:

<script src="https://gist.github.com/panoptikum/cc4c3f5371a7c0fac944edf04dd687b5.js"></script>

this code chunk tokenizes and tags each posts with the candidate's name:

<script src="https://gist.github.com/panoptikum/17f05f9dfc26f48575540fda76e26ffd.js"></script>

doc2vec has a fast version which we activate with the following code:

<script src="https://gist.github.com/panoptikum/0dc7ca4687141448c1ca5480983ee25b.js"></script>

## doc2vec model

sets the parameters of the models:

<script src="https://gist.github.com/panoptikum/40cab8f6435e9b57998b9e312fd54950.js"></script>

builds the vocabulary once and transfer it to all models:

<script src="https://gist.github.com/panoptikum/f0d9a839ce1025bd5402430e411c795b.js"></script>

to be able to call the models by their name we use an ordered dictionary:

<script src="https://gist.github.com/panoptikum/cc038f4c7351ee12c27882a0318151d7.js"></script>

### training the models

here you can set the epochs of your choice. For debugging reasons We only ran one value of epochs at a time and not several:

<script src="https://gist.github.com/panoptikum/f41b2745cfc74986d2ae1542f8ce514e.js"></script>

We recommend to save the models for later use and if you test a set of parameters:

<script src="https://gist.github.com/panoptikum/6b8b40298c2f8b6afe4304872fb31d40.js"></script>

### a look on the resulting embeddings

To do some graphical analysis or to compute something with the model, we need candidate specific data such as party affiliation:

<script src="https://gist.github.com/panoptikum/103fe5b5085929e1881a2965d177291e.js"></script>

next we define some colors for the parties that we can identify the candidates in our graphs later on. Furthermore, we create an array that contains the party leaders that we can use a different shape for them. We do the same for the Party accounts:

<script src="https://gist.github.com/panoptikum/39fae3bdab4058d97085abe8765b5c43.js"></script>

#### plots

now we need the plotly graphic library and some other libraries. In addition, we load our trained models of PV-DM and PV-DBOW with 20 epochs:

<script src="https://gist.github.com/panoptikum/095f4daab1d97b5745722f5147e7bd0c.js"></script>

you can compare the models directly with each other, if you create a subplot. The following code chunks does this job, access the candidate embeddings (vector) reduces the dimensionality them to two dimensions and plots them:

<script src="https://gist.github.com/panoptikum/c7e3db70799548b1c33e5daab8ddafc3.js"></script>

let's finally look at the candidate embeddings (vectors) mapped into two dimension:

<script src="https://gist.github.com/panoptikum/ca40fcf7c0da73c829ce6b58f9ce161f.js"></script>

<iframe width="900" height="800" frameborder="0" scrolling="no" src="//plot.ly/~Stipe/122.embed"></iframe>

# Playing around with the model
