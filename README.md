## Cagatay's steps:

### Installation: 
I used the original `requirements.txt` to install the necessary packages on my Linux workstation. For my MacBook, I had to slightly modify the original installation procedure. I summarize the steps for mac installation below:

1. Create a new conda environment by running ```conda create --name aen --file requirements-caca.txt ```.
2. Activate the newly installed environment: ```conda activate aen```.
3. Install `pytorch` via pip, not conda (otherwise my MacBook complains): ```pip install pytorch==1.11.0```
4. Install `e2cnn`: ```pip install e2cnn```

- Note-1: I needed to add the `conda-forge` channel to my list of channels (that conda looks for finding packages) by running ```conda config --append channels conda-forge```.
- Note-2: Since I use a mac, I did not install `cudatoolkit==11.7.64`.

### Downloading the datasets
I downloaded the data from https://roselab1.ucsd.edu/seafile/d/8886a9ee4c5248afab26/. I created a folder `PhiFlow` in the main repo folder, then put the downloaded `Rotation` folder inside `PhiFlow`.

### Running the model
``` python3 run_model.py --relaxed_symmetry=Rotation --hidden_dim=92 --num_layers=5 --out_length=6 --alpha=1e-5 --batch_size=16 --learning_rate=0.001 --decay_rate=0.95 ```

- - - - - 

## Paper: 
Rui Wang*, Robin Walters*, Rose Yu; [Approximately Equivariant Networks for Imperfectly Symmetric Dynamics](https://arxiv.org/abs/2201.11969); International Conference on Machine Learning (ICML) 2022

## Abstract:
Incorporating symmetry as an inductive bias into neural network architecture has led to improvements in generalization, data efficiency, and physical consistency in dynamics modeling. Methods such as CNN or equivariant neural networks use weight tying to enforce symmetries such as shift invariance or rotational equivariance. However, despite the fact that physical laws obey many symmetries, real-world dynamical data rarely conforms to strict mathematical symmetry either due to noisy or incomplete data or to symmetry breaking features in the underlying dynamical system. We explore approximately equivariant networks which are biased towards preserving symmetry but are not strictly constrained to do so. By relaxing equivariance constraints, we find that our models can outperform both baselines with no symmetry bias and baselines with overly strict symmetry in both simulated turbulence domains and real-world multi-stream jet flow.

## Description of Files
1. data_prep.ipynb: code for generating PhiFlow translation, rotation and scaling datasets.

2. models: pytorch implementation of all non-equivariant, equivariant and approximately equivariant models.
     
3. run_model.py: model training and evaluation.

4. utils.py: pytorch dataset function and training helper functions.

## Requirements
- To install requirements
```
pip install -r requirements.txt
```

## Instructions
### Dataset and Preprocessing
- Install PhiFlow First 
```
git clone -b 2.0.1 --single-branch https://github.com/tum-pbs/PhiFlow.git
```

- Move data_prep.ipynb to the PhiFlow folder and run data_prep.ipynb to generate approximate translation, rotation and scaling symmetry smoke plume datasets.

- Or you can directly download preprocessed smoke plume and JetFlow datasets from [here](https://roselab1.ucsd.edu/seafile/d/8886a9ee4c5248afab26/). 

### Training
- Train relaxed translation group convoluton, relaxed rotation steeratble CNNs and relaxed scaling steeratble CNNs on smoke plume datasets.
```
sh run.sh
```

## Cite
```
@inproceedings{wang2022approximately,
title={Approximately Equivariant Networks for Imperfectly Symmetric Dynamics},
author={Rui Wang and Robin Walters and Rose Yu},
booktitle={International Conference on Machine Learning},
year={2022},
organization={PMLR}
}
```
