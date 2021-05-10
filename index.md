---
layout: default
---

# Introduction

Display advertising can give the company much more benifit. Modern advertising recommendation mechanism predict the users' behavior by predicting advertisement Click-Through Rate (CTR). By giving a user and the page he is visiting, the algorithm will come with the probability that he will click on the given advertisement. The algorithm would make a huge profit to the companies by doing this.

Displaying advertisments can give the company much more benifit. Modern advertising recommendation mechanism predict the users' behavior by predicting advertisement Click-Through Rate (CTR). By giving a user and the page he is visiting, the algorithm will come with the probability that he will click on the given advertisement. The algorithm would make a huge profit to the companies by doing this.

The algorithm would help the company to meet the users' needs and make the functions efficient. For those multi-media companies like YouTube and Tiktok, it would help them put the related advertisement into specific videos which would increase the possibilty the user clicks on the advertisement and buys the related products. For those online shopping websites like Amazon and eBay, the algorithm can also be used to recommend related items based on the items the user is browsing. By using the algorithm, the user would get a better user experience in using the product which would bring more possibility for the sellers to sell their products and offer their services.

The project is a recommendation model, even though we are predicting CTR. We would like to show the potential users the advertisements have higher probability to be clicked. It is the recommender system which is considered one among the most powerful tools in the present digital world. In the field of recommender systems there are various methods and approaches which have been implemented. We use DeepFM as our benchmark and try to make some improvements.


# DataSet

We train and evaluate our model based on the [Criteo](https://www.kaggle.com/c/criteo-display-ad-challenge) dataset. Criteo is a famous advertising company and in the top level of this industry. It has 31 offices around the world and has one of the best engines in advertisement recommendation. Criteo data set is an online advertising dataset released by Criteo Labs. It is made by the data in Criteo in 7 days and becomes a well-know public dataset to benchmark the most accurate algorithms for CTR estimation. 

We train and evaluate our model based on the [Criteo](https://www.kaggle.com/c/criteo-display-ad-challenge) dataset. Criteo is a famous advertising company in the top level of this industry. It has 31 offices around the world and has one of the best engines in advertisement recommendation. Criteo data set is an online advertising dataset released by Criteo Labs. It is made by the data in Criteo in 7 days and becomes a well-know public dataset to benchmark the most accurate algorithms for CTR estimation. 

The Criteo Dataset is a public dataset has 40 million training samples and 5 million testing samples. It has 13 integer features and 26 categorical features and use log loss to evaluate models.
The data fields of Criteo Dataset:
* Label : Target variable that indicates if an ad was clicked (1) or not (0).
* L1-L13 : A total of 13 columns of integer features (mostly count features).
* C1-C26 : A total of 26 columns of categorical features. The values of these features have been hashed onto 32 bits for anonymization purposes. 

# Algorithms Detail
## Benchmark
### DeepFM

Compaing to Wide & Deep Learning, DeepFM use FM (Factorization Machine) instead of LR (logistic Regression) in the wide part and use concatenation of embadding vectors as the input of MLP (Multilayer Perceptron) in the deep part. DeepFM get over the need of feature engineering besides raw features and realized an end-to-end model with learning in both low and high order feature interactions. DeepFM trains a deep component and an FM component jointly. It does not need pre-training and introduces a sharing strategy of feature embedding to avoid feature engineering. Based on these, DeepFM gains a performance improvement with a lot of advantages.

![DeepFM](https://user-images.githubusercontent.com/49369552/117379697-9c322d80-af0a-11eb-97fd-413983fa283b.png)
<center style="font-size:14px;color:#C0C0C0;text-decoration:underline"> The architecture of DeepFM </center> <center style="font-size:14px;color:#778899;text-decoration:underline"> The architecture of DeepFM </center> 
## Our Works

### 1.	Connect FM with MLP

#### Model Structure

In DeepFM, FM models feature interactions in a linear way, which can be insufficient for capturing the non-linear and complex inherent structure of real-world data. To improve that, we try to combines the linearity of FM in modelling second-order feature interactions and the non-linearity of neural network in modelling higher-order feature interactions. We feed the 2 order feature interactions modeled by FM to MLP, and only keep the LR part on the left.

![](.\images\NFM.png)

<center style="font-size:14px;color:#C0C0C0;text-decoration:underline"> The architecture of NFM </center> 

#### compare with DeepFM
![](.\images\NFM vs DeepFM.png)

We compare the AUC on testing dataset of both models. From the plot we can see that NFM is slightly better than DeepFM.

### 2.	Attentional Factorization
#### Model Structure

Attentional Factorization Machine (AFM) is a variant of FM. Traditional FM sums the inner product of embedding vector uniformly. AFM can be seen as weighted sum of feature interactions. The weight is learned by a small MLP.

![AFM](https://user-images.githubusercontent.com/49369552/117373856-a4846b80-aefe-11eb-9b8a-f9244c2541c6.png)

<center style="font-size:14px;color:#C0C0C0;text-decoration:underline"> The architecture of AFM </center> 
### 2.	Attentional Factorization Machine + Deep Neural Network
#### Model Structure

AFM improves FM by discriminating the importance of different feature interactions. AFM learns the importance of each feature interaction from data via a neural attention network. The attention mechanism enables feature interactions to contribute differently to the prediction.

![AFM](https://user-images.githubusercontent.com/49369552/117581236-679ebb80-b12e-11eb-8ea7-2edbe801383d.png)
<center style="font-size:14px;color:#778899;text-decoration:underline"> The architecture of AFM </center> 

![DNN](https://user-images.githubusercontent.com/49369552/117581285-a765a300-b12e-11eb-9534-00940b82cb15.png)
<center style="font-size:14px;color:#778899;text-decoration:underline"> The architecture of DNN </center> 

#### Improvement

To further improve the AFM, we try to combine deep neural network with afm to enhance the capability for high order interactions between features. Like deepFM, the AFM parts and DNN parts have a share input and trained jointly for the combined prediction model in our approach.
