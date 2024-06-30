# ProtoVQ-VAE: Prototype-based Recommender System

## Overview
ProtoVQ-VAE makes use of vector quantization (VQ) applied to the latent space of a variational autoencoder (VAE),
to generate a prototype-based recommender system in the domain of collaborative filtering. More specifically, 
the system aims at generating prototypes that represent the interests of similar users. Instead of generating 
individual recommendations for each user, the user is mapped to a set of these prototypes which are most similar
to the user's previous choices, which are fed to the decoding part of the VAE.

The system is based on the seminal paper "Neural Discrete Representation Learning" by Oord et al. from 2018. As 
opposed to VQ-VAE, which they introduced in this paper and which was developed for image data, ProtoVQ-VAE modifies
this architecture to work with sparse data.

## Repository
### Structure
```bash
.
├── configs
│   ├── config.yaml
├── data
│   ├── lfm2b-1mon
│   │   ├── lfm2b-1mon.inter
├── data_exploration_preprocessing.ipynb
├── protovqvae.yml
├── protovq_vae_recbole.ipynb
├── README.md
```

### Files & Folders
- `protovqvae.yml`: Environment - installation see below.
- `protovq_vae_recbole.ipynb`: Main notebook containing the RecBole implementation of ProtoVQ-VAE.
- `configs/config.yaml`: RecBole configuration file
- `data/lfm2b-1mon/lfm2b-1mon.inter`: Dataset file in RecBole .inter format
- `data_exploration_preprocessing.ipynb`: Mixture of data exploration and data preprocessing - outputs .inter file.

### Installation and Configuration
#### Environment
- Install the environment via `conda env create -f protovqvae.yml`
- Use the conda environment `protovqvae` when running `protovq_vae_recbole.ipynb`.

#### Data
The dataset `lfm2b-1mon.inter` provided in this repository is a highly reduced version of the LFM-2b-1mon dataset
provided by Johannes Kepler University's Institute of Computational Perception, transformed into RecBole .inter format.
LFM-2b-1mon contains the last.fm listening events of one month of the  much bigger LFM-2b dataset and contains about
30.3 million listening events by 15.258 users from the year 2020.

In order to provide a dataset which also runs on less performant local GPUs, just items that were listened to by at 
least 100 users and users that listened to at least 100 items were kept - see further details in 
`data_exploration_preprocessing.ipynb`.

#### Configuration
Before executing the main notebook `protovq_vae_recbole.ipynb` on your local machine, you need to adapt the main
RecBole configuration file `config.yml`. More precisely, you need to enter the absolute path to the data folder - 
for example, if you use the below configuration ...

```bash
data_path: /home/your_user/code/ProtoVQ-VAE/data/
dataset: lfm2b-1mon
```

...  RecBole expects `lfm2b-1mon.inter` to be located here: 

`/home/your_user/code/ProtoVQ-VAE/data/lfm2b-1mon/lfm2b-1mon.inter`