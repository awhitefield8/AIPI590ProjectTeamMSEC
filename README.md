# AIPI Final Project: Team MSEC

![HM](./img/retail_rocket.png)



## Introduction

In this project we train different session based product recommenders. We compare the performance of the recommenders across two datasets.

## Data

We use two datasets: the H&M Personalized Fashion Recommendations dataset (HM), and the Retailrocket recommender system dataset (RR). The HM Fashoin dataset contains the purchase data containing the time and the time of purchase for many customers. It also has product descriptions and images that are not used in this work. Retail Rocket contains data on the time and date of items clicked on and purchased by consumers.


## Evaluation metrics

We use two offline evaluation metrics: Normalized Discounted Cumulative Gain (NDCG) and Hit Ratio (HR). The Hit Rate is whether the item that the consumer next clicked on or bought is in the top k items reported by the model. NDCG is a metric for evaluating the quality of the results. It looks at the hit rate and discounts the hit for its position in the top k. Lower down the lower the gain. It is then normalized by dividing by the best possible dicounted cumulative gain.


## Algorithms

We use SA2C and a standard deep learning set up of a GRU using only cross entropy loss to train the network. In this project we want to look at the gains from adding a reinforcement learning regularization to cross entropy loss.

## Results

We run compare the metric development for various values of K (5,10,15 and 20). We look at metrics applied to clicks and to purchases. Note that for the HM data, there is no click data so the charts are a flat line that should be ignored.

![HM](./results/charts/SA2CResultsRetailRocketresults.png)

![HM](./results/charts/CELossOnlyResultsRetailRocketresults.png)

![HM](./results/charts/SA2CResultsHMresults.png)

![HM](./results/charts/CELossOnlyHMresults.png)


We then compare HR and NDCG metrics across algorithms and dataset. In the tables in the following section, each column refers to a metric applied and level of K. For example, **HR@5** corresponds to the the hit rate at K=5.

### Purchases

We first look at the results based on purchases. 

| **Models**         | **HR@5** | **NDCG@5** | **HR@10** | **NDCG@10** | **HR@15** | **NDCG@15** | **HR@20** | **NDCG@20** |
| :---------:        | :------: | :------:   | :-------: | :-------:   | :-------: | :-------:   | :-------: | :-------:   |
| RR: GRU-NonDL   |   0.3657  |  0.2934    |  0.4214   |   0.3115    |  0.4534  |  0.3199      |   0.4717  |   0.3242     | 
| RR: GRU-SA2C   |   0.5350  |   0.4570    |   0.5872   |   0.4742    |   0.6095  |   0.4801    | 0.6263  |    0.4841     | 
| RR: SASRec-SA2C   |   0.5987  |  0.5113    |  0.6439   |   0.5260    |  0.6652  |  0.5317      |   0.6798  |   0.5351    | 
| HM: GRU-NonDL   |  0.0123  |  0.0086   |  0.0168   |   0.0100    |  0.0202  |  0.0109      | 0.0226 |   0.0115     | 
| HM: GRU-SA2C   |  0.0121  |   0.0087   |  0.0183   |   0.0107    |   0.0216  |  0.0116     | 0.0242  |   0.0122     | 
| HM: SASRec-SA2C   |   0.0330 |  0.0228    |  0.0444   |   0.0265    |  0.0508  |  0.0282    |   0.0554  |   0.02929    | 


### Clicks

We then compare the results based on clicks. Note that this data does not exist for the HM data.

| **Models**         | **HR@5** | **NDCG@5** | **HR@10** | **NDCG@10** | **HR@15** | **NDCG@15** | **HR@20** | **NDCG@20** |
| :---------:        | :------: | :------:   | :-------: | :-------:   | :-------: | :-------:   | :-------: | :-------:   |
| RR: GRU-NonDL   |  0.1811  |  0.1386    |  0.2227   |   0.1520    |  0.2469  |  0.1585      | 0.2637   |   0.1625     | 
| RR: GRU-SA2C   |  0.2713  |  0.2136    |  0.3199   |   0.2294    |   0.3469  |  0.2365     | 0.3649  |   0.2408     | 
| RR: SASRec-SA2C   |   0.2883  |  0.2257    |  0.3420   |   0.2431    |  0.3706  |  0.2507      |   0.3901  |   0.2553    | 


## Conclusion

The GRU-SA2C methods outperform the NonDL methods across the two datasets. We would expect this because without using reinforcement learning the model will not properly discount out of training distribution results. So adding this regularization term of advantage helps the model stay within the range of it's training data. Using a transformer improved the metrics bu about 1% in the RetailRocket data set and about 0.02% in the H&M data.


### Example

The models are run via the command line. The results are stored in the results folder, but this location can be changed with the results_path command line argument. 

```
python SA2C.py --model=GRU --epoch=15 --data=../../data/data_rr/
```

## Code Structure
```
????????? README.md
????????? img
???   ????????? retail_rocket.png
????????? notebooks
???   ????????? ResultPlotting.ipynb
???   ????????? CELossOnly_rr_experiments.ipynb
???   ????????? sa2c_rr_experiments.ipynb
???   ????????? CELossOnly_hm_experiments.ipynb
???   ????????? sa2c_hm_experiments.ipynb
???   ????????? sa2c_sasrec_rr_experiments.ipynb
???   ????????? sa2c_sasrec_hm_experiments.ipynb
|   |?????? rr_tester.ipynb
|   |?????? hm_tester.ipynb
???   ????????? HM_SNQN_SASRec.ipynb
????????? src
|   ????????? models
|   |   ????????? CELossOnly.py
|   |   ????????? NextItNetModules.py
|   |   ????????? pop.py
|   |   ????????? SA2C.py
|   |   ????????? SASRecModules.py
|   |   ????????? SNQN.py
|   |   ????????? split_data.py
|   |   ????????? test.py
|   |   ????????? utility.py
|   ????????? preprocessing
|       |?????? gen_replay_buffer_hm.py
|       ????????? preprocess_kaggle.py
????????? data
|   ????????? data_hm
|   ????????? data_hm
????????? results

```


## References


Xin, Xin, et al. "Supervised Advantage Actor-Critic for Recommender Systems." Proceedings of the Fifteenth ACM International Conference on Web Search and Data Mining. 2022.
[<a href="https://arxiv.org/abs/2111.03474 ">arxiv</a>]

Vaswani, Ashish, et al. "Attention is all you need." Advances in neural information processing systems 30 (2017).



## Data sources

H&M Personalized Fashion Recommendations  [<a href="https://www.kaggle.com/competitions/h-and-m-personalized-fashion-recommendations/data?select=transactions_train.csv">dataset</a>]

Retailrocket Recommender System [<a href="https://www.kaggle.com/datasets/retailrocket/ecommerce-dataset?select=category_tree.csv
">dataset</a>]


### Authors: Jordan Axelrod, Alexander Whitefield

### Contributions

Jordan Axelrod

Creating the nonDL model and the data visualizations. Researched different data sources. Ran the models on the HM data. Created data collection methods inside evaluate and the main if statement of SA2C and CEOnly. Wrote portions of the report. 

Alexander Whitefield

Created the data pipeline for the RetailRocket data. Ran the models on the RetailRocket data. Converted the repository from Tensorflow v1 to Tensorflow v2. Wrote portions of the report. 
