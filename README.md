# AIPI Final Project: Team MSEC

![HM](./img/retail_rocket.png)



## Introduction

This project is pure class. I hope you enjoy reading it.

## Data

We use two datasets: the H&M Personalized Fashion Recommendations dataset, and the Retailrocket recommender system dataset.





## Evaluation metrics

We use two offline evaluation metrics: Normalized Discounted Cumulative Gain (NDCG) and Hit Ratio (HR).

## Algorithms

We use SA2C and ...

## Results

First, we plot the results for each model, across both dataset. We look at HR and NDCG by purchase and by click.

| **Models**  | **HR@5** | **NDCG@5** | **HR@10** | **NDCG@10** | **HR@20** | **NDCG@20** |
| :---------: | :------: | :------: | :-------: | :-------: | :-------: | :-------: |
| RR: SASRec-NonDL |  0.0399  |  0.0279  |  0.0530   |  0.0322   |  0.0637   |  0.0349   |
| RR: SASRec-SA2C |  **0.0399**  |  **0.0279**  |  **0.0530**   |  **0.0322**   |  **0.0637**   |  **0.0349**   |
| HM: SASRec-NonDL |  0.0399  |  0.0279  |  0.0530   |  0.0322   |  0.0637   |  0.0349   |
| HM: SASRec-SA2C |  **0.0399**  |  **0.0279**  |  **0.0530**   |  **0.0322**   |  **0.0637**   |  **0.0349**   |

By buy

| **Models**  | **HR@5** | **NDCG@5** | **HR@10** | **NDCG@10** | **HR@20** | **NDCG@20** |
| :---------: | :------: | :------: | :-------: | :-------: | :-------: | :-------: |
| RR: SASRec-NonDL |  0.0399  |  0.0279  |  0.0530   |  0.0322   |  0.0637   |  0.0349   |
| RR: SASRec-SA2C |  **0.0399**  |  **0.0279**  |  **0.0530**   |  **0.0322**   |  **0.0637**   |  **0.0349**   |
| HM: SASRec-NonDL |  0.0399  |  0.0279  |  0.0530   |  0.0322   |  0.0637   |  0.0349   |
| HM: SASRec-SA2C |  **0.0399**  |  **0.0279**  |  **0.0530**   |  **0.0322**   |  **0.0637**   |  **0.0349**   |


## Conclusion

The authors are amazing


### Example

To models are run via the command line. The results are stored in the results folder, but this location can be changed with the results_path command line argument. 

```
python SA2C.py --model=GRU --epoch=15 --data=data_rr
```

## Code Structure
```
├── README.md
├── img
│   └── retail_rocket.png
├── notebooks
│   ├── ResultPlotting.ipynb
│   ├── CELossOnly_rr_experiments.ipynb
│   ├── sa2c_rr_experiments.ipynb
|   |── rr_tester.ipynb
|   |── hm_tester.ipynb
│   └── HM_SNQN_SASRec.ipynb
├── src
|   ├── models
|   |   ├── CELossOnly.py
|   |   ├── NextItNetModules.py
|   |   ├── pop.py
|   |   ├── SA2C.py
|   |   ├── SASRecModules.py
|   |   ├── SNQN.py
|   |   ├── split_data.py
|   |   ├── test.py
|   |   └── utility.py
|   └── preprocessing
|       |── gen_replay_buffer_hm.py
|       └── preprocess_kaggle.py
├── data
|   ├── data_hm
|   └── data_hm
└── results


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
