# COVID-19 DREAM Challenge: Baseline Model

## Overview
This repository describes how to build and run locally the
baseline model of the [COVID-19 DREAM Challenge](https://www.synapse.org/#!Synapse:syn18404605). The goal of this [DREAM Challenge](http://dreamchallenges.org/) is to develop models that take as input the electronic health records (EHRs) of a patient and outputs the probability of this patient tested positive for COVID-19.

## Description of the model
This baseline model takes 15 features including clinical symptoms and vital signs and refers to research conducted by Feng et al. [link](https://www.medrxiv.org/content/10.1101/2020.03.19.20039099v1)
This baseline model isn't trained on any real COVID patient data. Each patient is given a risk score based on the presence of the 14 features. A threshold of risk score is chosen basing on 10% test positive rate in Washington state. Patients whose risk scores are above threshold are assigned test-positive probability as 1, otherwise 0.

| Feature|OMOP concept-id|Domain|Threshold|
|-|-|-|-|
|age|year_of_birth|person|>55|
|temperature|3020891|measurement|>37.5'C|
|heart rate|3027018|measurement|>100n/min|
|diastolic blood pressure|3012888|measurement|>85mmHg|
|systolic blood pressure|3004249|measurement|>140mmHg|
|hematocrit|3023314|measurement|>44|
|neutrophils|3013650|measurement|>8|
|lymphocytes|3004327|measurement|>9.5|
|oxygen saturation in artery blood|3016502|measurement|<94%|
|cough|35211275|condition|-|
|pain in throat|35211283|condition|-|
|chest pain on breathing|35211284|condition|-|
|headache|35211388|condition|-|
|fatigue|45534458|condition|-|
|shortness of breath|45534422|condition|-|


## Dockerize the model

1. Clone this GitHub repository
2. `docker build -t docker.synapse.org/syn12345/my_model:v0.1 example/app`

## Run the baseline model locally on synthetic data
This section describes how to run the model locally, that is, without using the IT infrastructure of the [COVID_19 DREAM challenge](https://www.synapse.org/#!Synapse:syn18404605)(need updates).

### Description of the data
[Learn more about OMOP Synpuf data](https://www.synapse.org/#!Synapse:syn18405992/wiki/594233)(need updates)

### Download the data
[The Synpuf data are available here](https://www.synapse.org/#!Synapse:syn20685954). After downloading them, uncompress the archive and place the data folder where it can later be accessed by the dockerized model (see below).(need updates)

### Run the model locally on Synpuf data
Once the baseline model has been dockerized (see above), run the following command to train the model on Synpuf data:

```
docker run -v <path to data folder>:/data:ro
-v <path to scratch folder>:/scratch:rw
-v <path to output folder>:/output:rw
 docker.synapse.org/syn12345/my_model:v0.1 bash /app/COVID_baseline.sh
```

where

- `<path to data folder>` is the absolute path to the data (e.g. `/home/charlie/ehr_experiment/synpuf_data/data`).
- `<path to scratch folder>` is the absolute path to the scratch folder (e.g. `/home/charlie/ehr_experiment/scratch`).
- `<path to output folder>` is the absolute path to where the  the predictions will be exported (e.g. `/home/charlie/ehr_experiment/output`))





If the docker model runs successfully, the prediction file `predictions.csv` file will be created in the output folder. This file has two columns: 1) person_id and 2) test-positive probability. Note: make sure the column 2) contains no NA and the values are between 0 and 1.

## Make a submission to COVID-19 DREAM challenge

Please see this Synapse page for instructions on how to make a submission [link](https://www.synapse.org/#!Synapse:syn21849256/wiki/601875)
