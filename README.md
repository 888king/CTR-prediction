# CTR-prediction - cs547 final project
## Operating environment

please use `pip install -U deepctr-torch` to setup the operating environment.

## Download dataset

The dataset is hosted on Azure ML.
Each day can be downloaded at http://azuremlsampleexperiments.blob.core.windows.net/criteo/day_XX.gz, where XX goes from 0 to 23.

The following command downloads all days:

<code>curl -O http://azuremlsampleexperiments.blob.core.windows.net/criteo/day_{\`seq -s ‘,’ 0 23\`}.gz</code>

## Training and Evaluation

1. run `DeepFM_train.py` to train and evaluate DeepFM.
2. run `NFM_train.py` to train and evaluate NFM.
3. run `deepafm.ipynb` to train and evaluate AFM.

 ## Website

We show our results at [here](https://888king.github.io/CTR-prediction/).