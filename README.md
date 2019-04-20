# Data-Science-to-fight-poverty
Github for my notebook related to the class Info288 at UC Berkeley

About the course:

As new sources of digital data proliferate in developing economies, there is the exciting possibility that such data could be used to transform development research and policy. Recent examples show how **satellite imagery and deep learning** can be used to identify and target pockets of extreme poverty; how mobile phone metadata can help track and stop the spread of malaria and Ebola; how social media analytics can improve disaster response; and how machine learning algorithms can help smallholder farmers optimize planting and harvesting decisions – to name just a few examples. Through a careful reading of recent research papers and through hands-on analysis of non-traditional datasets, this course introduces students to the opportunities and challenges for data–intensive approaches to international development. Students must have graduate training in econometrics, machine learning, or a related field.

Source: sites.ischool.berkeley.edu/bdd/

Website of the class: https://sites.ischool.berkeley.edu/bdd/
Github of the teacher: https://github.com/jblumenstock

Related article: https://www.clubic.com/technologies-d-avenir/intelligence-artificielle/actualite-854056-facebook-cree-densite-population-afrique-aide-ia.html

## Introduction to poverty and economic development

Source: *Measuring Poverty* - Angus Deaton

What is poverty? How to fight it? What features are more correlated with poverty? Are they easily accessible? 

**Bias** when assessing poverty: some NGOs are trying to evaluate the poverty of the population to distribute food rations. This gives incetives to people to identifies they close relatives as being poor. Therefore, usually when poverty indicators are used for employment or humanitarian help, more people are identified as poor. As result, it is not always appropiate to use data from the population that either self-identify as poor or identify they relatives that way to implement a certain policy. If people can expect a higher beefit out of a undereported answer, they will probably do it. 

**What identify poor people**:
- spend most of their **money on food** (are they able to reach the 2k calories a day? : can be used as a threshold to define poverty (as a binary variable). The **thresold** need to be customized to the individual: is he able to reach his own daily calories need? (related to his location, physical activities (if he is working on the field the needs are going to be higher), morphological caracterisctics etc.). **Political issues** involving redistribution are usually involved in the definition of the poverty line
- they are at the **end of the distribution of income and consumption** (the poverty of one country can be evaluated by the variance and mean of its income distribution - using the variance introduce the concept of relative poverty where you would evaluate one's poverty by comparing it to others): poverty = **lack of income or consumption**
- have **poor healthy condition**: this is related to the environment, living in a poluted, unsanitary or warfare environment can lead to malnutrition, diseases and poor education
- have a **poor education** that prevent them from participating to the social life: this actually prevent poor people from getting a full role in the society. 

Currently, the **Human Development Index** published by the United Nation Development Program uses three features: income, life expectancy and literacy. They are lot of other features that can measure some other parts of human development. Yet, most of the time those features are correlated together. For intance, an improvement in public health is likely to improve also life expectancy. Similarly income growth will also improve non-income perverty measures. 

Does a poverty line actually make sense? Should not it be a sort of continuous poverty level evaluation instead of binary classification (degree of poverty). As people that are close together but on different side of the poverty line are actually living a similar situation and should not be classified as opposed. This can be achieved using the poverty gap: computing the difference between the poverty level of an individual and the poverty line so we can weight each individual's poverty and using a weighted sum over the entire population it would make it easier and more acurate to estimate the poverty of a given area. 

## Papers on Data Science & Poverty

### Combining satellite imagery and machine learning to predict poverty - 2016

The **goal** here is to estimate consuption expenditure and asset wealth using satellitee imagery.
**Tool** used: CNN
**Result**: the model can explain up to 75% of variation in local-level economic outcomes
**Value**: it makes it easier to target efforts to tackle poverty

Let start with the **problem**. Currently, lot of countries in the developping world have only few data available regarding economic development. This harm the ability to target intervention and effort to identify the needs in a particular place. In addition, it is hard to scale up the traditional data collection methods. 

One solution is to use **passively collected data**, from Mobile Phone, Stallite imagery or social media. In this paper, the idea is to **leverages luminosity at night in satellite imagery** to **estimate the economic activity**. Yet, in some impoverished areas, luminosity level can me quite low and therefore has few variability. In addition we don't have a lot of labeled data available. One solution to this problem is to use Transfer Learning. 

The steps are:
1. Using a **CNN pretrained on ImageNet**
2. **Fine tune the model** to predict nighttime light intensities
3. **Train a Ridge regression** to estimate cluster level expenditure or asset (using survey + images features from the model)

In the paper, the model is able to detect:
- Urban areas 
- Roads
- Agricultural areas
This was done in an unsupervised way. Finally, the model can **explain 37% to 55% of the variation in average household consumption**. 

Another interesting value of this approach is that model appear to **"travel well"**. Indeed, model trained on one country can still give relevant information on a different country, where it would have seen no data. This is particularly valuable for countries with no data available.


### Tile2Vec: Unsupervised representation learning for spatially distributed data - 2018

**Problem**: find techniques to mitigate the need for labeled data
The idea from this paper is to define a low-dimensional representation of the data that is more suitable for downstream ML tasks. 

**Goal**: to define an unsupervised representation learning algorithm that can learn semantically meaningful representation of satellite image data. This aim at improving the performance of classification tasks. This extend the notion of word2vec that assume that words appearing in identical context will have similar meaning. This is a feature extraction method that can be compared to other methods such as PCA or Autoencoders. 

The **assuptions** used are that tiles that are neighbors from a geographic point of view , should have similar semantics and therefore similar representations. An **analogy** is built here with the Word2Vec representation where we assume that word appearing in the same context are likely to have similar semantics. In our case, the context is defined a distance in the geophafic space. 

**Main task**: learn a mapping from images tiles to low-dimensional embeddings. To do so, a CNN is trained on triplets of tiles: on anchor tile ta, a neighbor tile tn (close geographically) and a distant tile td that is far away. The optimization task then minimizes the euclidean distance between the embedding of the anchor tile and the neighbor tile, while maximizing the distance between the anchor and the distant embeddings.  

This method is used on both sensing imageries and countries characteristics in order to predict poverty. 

**Applications**:
- land cover classification task: predicting what is on the earth surface using remotely sensed imagery. 
- regression task: predicting local poverty level using surveys data. The survey are used as label for poverty prediction task (next -).
- predict anual consuption expenditures from satellite imagery. 

Tile2Vec can learn representations at multiple scales that are sufficiently robust to use domain adaptation or transfer learning. 

**Generalization**: it can also leverage spatial cohernce for non-image datasets.

## Current trends

### Facebook is working on mapping Africa's population density 

Facebook is also actually trying to tackle the challenge of optimizing the humanitarian help alocation. To do so, they are using a Neural Network training on more than one million images. Then, they analysed 11.5 millions of satellite images in Africa to map people residence places. Those Computer Visions insights has been combined with some other gathered informations such as census data. Finally, they identified 110 millions homes and found out several inhabited areas. 

The end goal of this analysis is to help humanitarians organization when they have to choose where to concentrate there ressources. The information should enable to locate places and populations that are particularly in need and require closer attention. 
