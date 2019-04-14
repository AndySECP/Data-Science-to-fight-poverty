# Data-Science-to-fight-poverty
Github for my notebook related to the class Info288 at UC Berkeley

About the course:

As new sources of digital data proliferate in developing economies, there is the exciting possibility that such data could be used to transform development research and policy. Recent examples show how **satellite imagery and deep learning** can be used to identify and target pockets of extreme poverty; how mobile phone metadata can help track and stop the spread of malaria and Ebola; how social media analytics can improve disaster response; and how machine learning algorithms can help smallholder farmers optimize planting and harvesting decisions – to name just a few examples. Through a careful reading of recent research papers and through hands-on analysis of non-traditional datasets, this course introduces students to the opportunities and challenges for data–intensive approaches to international development. Students must have graduate training in econometrics, machine learning, or a related field.

Source: sites.ischool.berkeley.edu/bdd/

Website of the class: https://sites.ischool.berkeley.edu/bdd/
Github of the teacher: https://github.com/jblumenstock

Related article: https://www.clubic.com/technologies-d-avenir/intelligence-artificielle/actualite-854056-facebook-cree-densite-population-afrique-aide-ia.html

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


## Current trends

### Facebook is working on mapping Africa's population density 

Facebook is also actually trying to tackle the challenge of optimizing the humanitarian help alocation. To do so, they are using a Neural Network training on more than one million images. Then, they analysed 11.5 millions of satellite images in Africa to map people residence places. Those Computer Visions insights has been combined with some other gathered informations such as census data. Finally, they identified 110 millions homes and found out several inhabited areas. 

The end goal of this analysis is to help humanitarians organization when they have to choose where to concentrate there ressources. The information should enable to locate places and populations that are particularly in need and require closer attention. 
