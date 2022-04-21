# FOREC: A Cross-Market Recommendation System
This repository provides the implementation of CIKM 2021 paper titled as "[Cross-Market Product Recommendation](https://arxiv.org/pdf/2109.05929.pdf)".

The general schema of our FOREC recommendation system is shown below. For a pair of markets, the middle part shows the market-agnostic model that we pre-train, and then fork and fine-tune for each market shown in the left and right. Note that FOREC is capable of working with any desired number of target markets. However, for simplicity, we only experiment with pairs of markets for the experiments. For further details, please refer to our paper. 




## Requirements:
We use conda with pycharm for our experimentations. Please refer to the `requirements.txt` for the list of libraries we use for our implementation. After setting up your environment, you can simply run this command `pip install -r requirements.txt`. 

- python 3.8 
- pandas & numpy (pandas-1.3.3, numpy-1.21.2)
- torch==1.10.0
- [learn2learn](https://github.com/learnables/learn2learn)
- [pytrec_eval](https://github.com/cvangysel/pytrec_eval)

## DATA
The `DATA` folder in this repository contains the cleaned and proccessed data that we use for our experiments. Please note that we made a few changes with releasing the data, and you might see slightly different numbers compared to the reported numbers in the paper. 

If you wish to repeat the process on other categories of data or change the data preprocessing steps, `prepare_data.ipynb` provides the code for downloading and preprocessing data. Please refer to that jupyter notebook for further details. Don't hesitate to contact us in case of any problem. 


## Train the baseline and FOREC models (with Evaluations):
We provide three training scripts, for training baselines (single market, GMF, MLP, NMF++ and MAML) as well as FOREC model. Here are the list of models that for training and evaluating with the scripts provided:
- `train_base.py` for GMF, MLP, NMF and their ++ versions as cross-market models
- `train_maml.py` for training our MAML baseline
- `train_forec.py` for trainig our proposed FOREC model


Note that since MAML and FOREC works on NMF architecture, you need to have same setting NMF++ model trained before proceeding with the MAML and FOREC training scripts. In addition, NMF requires that GMF and MLP models are trained, as it combines these two models into the architecture with some additional layers. See the middle part of the FOREC schema above. 

A jupyter notebook (`train_all.ipynb`) that generates correct commands for all these trainings on any desired target market and augmenting source market pairs. These scripts are written into `scripts` folder created by the notebook. The logging of the training is alos in this directory under `log` sub-directory. 

A jupyter notebook (`train_demo.ipynb`)  generates result for one market dataset for demonstration purpose.

Note that for each of these, the train script evaluates on validation and test data (leave-one-out procedure for splitting---see `data.py`). The detailed evaluation results are dumped into `Result Parameters` folder as csv files. 






## Citation
 [CIKM’21 paper](https://arxiv.org/pdf/2109.05929.pdf)


