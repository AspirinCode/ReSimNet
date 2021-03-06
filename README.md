# ReSimNet
A Pytorch Implementation of paper
> ReSimNet: Drug Response Similarity Prediction using Siamese Neural Networks <br>
> Jeon and Park et al., 2018

## Abstract
Traditional drug discovery approaches identify a suitable target for a disease and find a compound that binds to the target. In this approach, structures of compounds are considered as the most important features because it is assumed that similar structures will bind to the same target. Therefore, structural analogs of the drugs that bind to the target are selected as drug candidates. However, even though compounds are not structural analogs, they may achieve the desired response and may be used for a disease. A new drug discovery method based on drug response, which can complement the traditional structure-based methods, is needed.

We implemented Siamese neural networks called ReSimNet that take as input two chemical compounds and predicts the CMap score of the two compounds, which we use to measure the transcriptional response similarity of the two counpounds. ReSimNet learns the embedding vector of a chemical compound in a transcriptional response space. ReSimNet is trained to minimize the difference between the cosine similarity of the embedding vectors of the two input compounds and the CMap score of the two compounds. ReSimNet can find pairs of compounds that are similar in response even though they may have dissimilar structures. In our quantitative evaluation, ReSimNet outperformed the baseline machine learning models. The ReSimNet ensemble model achieves a Pearson correlation of 0.518 (p value of <10^-6) and a precision@1% of 0.989. In addition, in the qualitative analysis, we tested ReSimNet on the ZINC15 database and showed that ReSimNet successfully identifies chemical compounds that are relevant to a prototype drug whose mechanism of action is known. ReSimNet can complement the existing structure-based virtual drug screening methods.

## Pipeline
![Full Pipeline](/images/pipeline_updated_kang2.png)

## Requirements
- Install [cuda-8.0](https://developer.nvidia.com/cuda-downlaods)
- Install [cudnn-v5.1](https://developer.nvidia.com/cudnn)
- Install [Pytorch 0.3.0](https://pytorch.org/)
- Install [Numpy 1.61.1](https://pypi.org/project/numpy/)
- Python version >= 3.4.3 is required

## Download Files You Need to Run ReSimNet

Clone our source codes

```bash
# clone the source code on your directory
$ git clone https://github.com/jhyuklee/ReSimNet.git
$ cd ReSimNet

# make folder to save and load your data
$ cd tasks
$ mkdir -p data

# make folder to save and load your model
cd ../../..
$ mkdir -p results
```

Download the files you need from

http://dmis.korea.ac.kr/downloads?id=ReSimNet

### 1. Dataset

#### Click the link "Download the Dataset".
Save this file to ./ReSimNet/tasks/data/ReSimNet-Dataset.pkl 

### 2. Pre-Trained Models

#### 2-1) Click the link "Download the Best Model".

Save this file to ./ReSimNet/results/ReSimNet-models-best.zip and Unzip. 

#### 2-2) Click the link "All 10 Models for Ensemble".

Save this file to ./ReSimNet/results/ReSimNet-model-ensemble.zip and Unzip. 

### 3. Example Input Pairs

#### Click the link "Download the Example Drugs".

Save this file to ./ReSimNet/tasks/data/pairs/examples.csv 

#### Click the link ""Download the FingerPrint Respresentation"".

Save this file to ./ReSimNet/tasks/data/pertid2fingerprint.pkl 


## Training the ReSimNet

```bash
# Train for new model.
$ bash train.sh

# Train for the new ensemble models.
$ bast train_ensemble.sh
```

## CMap Score Prediction using ReSimNet
For your own fingerprint pairs, ReSimNet provides a predicted CMap score for each pair. Running download.sh and predict.sh will first download pretrained ReSimNet with sample datasets, and save a result file for predicted CMap scores.
```bash
# Save scores of sample pair data
$ bash predict.sh
```
Input Fingerprint pair file must be a .csv file in which every row consists of two columns denoting two Fingerprints of each pair. Please, place files under './tasks/data/pairs/'. 
```bash
# Sample Fingerprints (./tasks/data/pairs/examples.csv)
id1,id2
BRD-K43164539,BRD-A45333398
BRD-K83289131,BRD-K82484965
BRD-K06817181,BRD-A41112154
BRD-K06817181,BRD-K67977190
BRD-K06817181,BRD-A87125127
BRD-K68095457,BRD-K38903228
BRD-K68095457,BRD-K01902415
BRD-K68095457,BRD-K06817181
```
Predicted CMap scores will be saved at each row of a file './results/input-pair-file.model-name.csv'.
```bash
# Sample results (./results/examples.csv.resimnet_pretrained.csv')
prediction
0.9146181344985962
0.9301251173019409
0.8519644737243652
0.9631381034851074
0.7272981405258179
```

## Liscense
Apache License 2.0
