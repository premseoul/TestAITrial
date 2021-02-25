# clinical-trial-outcome-prediction




## 1. Installation via Conda 

```bash

conda env create -f conda.yml


conda activate predict_drug_clinical_trial
```

The user can use conda.yml as reference to setup conda environment. 







































## 2. Raw Data 

```bash

ls ./ClinicalTrialGov  

```

It is downloaded from [ClinicalTrial.gov](https://clinicaltrials.gov/). 
It is 8.6+G, containing 348,891+ clinical trial records. 
The data size grows with time because more clinical trial records are added.  




































































## 3. Data Preprocess 


### 3.1 Collect all the 348,891 NCTIDs.
input: ClinicalTrialGov/   
output: data/all_xml 
```bash
find ClinicalTrialGov/ -name NCT*.xml | sort > data/all_xml
```


### 3.2 diseaes -> icd10
input: ClinicalTrialGov/* & data/all_xml   
output:	ctgov_data/diseases.csv  
```bash 
python src/collect_disease_from_raw.py
```


### 3.3 drug -> SMILES 
input:iqvia_data/drugbank_drugs_info.csv   
output:iqvia_data/drug2smiles.pkl   
```bash
### need optimize 
python src/drug2smiles.py 
```



### 3.4 Aggregation

input:     
* ctgov_data/diseases.csv  
* iqvia_data/drug2smiles.pkl  
* data/all_xml         

output: ctgov_data/raw_data.csv
```bash
python src/collect_raw_data.py | tee process.log 
```
It takes around 30 minutes.   




## 4. Dataset of clinical trial outcome prediction 



### 4.1 Data Split 

input: 



output:
* ctgov_data/phase_I_{train/valid/test}.csv 
* ctgov_data/phase_II.csv 
* ctgov_data/phase_III.csv 
* ctgov_data/trial.csv 


```bash
python src/data_split.py 
```


### 4.2 Data Statistics 

| Dataset  | Training | Test | Split Date |
|-----------------|-------------|-------------|
| Phase I |    |    |    |    |
| Phase II |    |   |    |    |
| Phase III |    |  |  |    |
| Indication |    |   |   |   |   


## 5. Learn and Inference 


### 5.1 Phase I Prediction

```bash

python src/learn_hint_phaseI.py


```


### 5.2 Phase II Prediction

```bash

python src/learn_hint_phaseII.py


```

### 5.3 Phase III Prediction

```bash

python src/learn_hint_phaseIII.py


```

### 5.4 Indication Prediction

```bash

python src/learn_hint_trial.py

```


## Quick Start 

* Setup Conda environment (1. Installation via Conda)
* Learning and Inference (5. Learn and Inference)



## Contact

Please contact futianfan@gmail.com for help or submit an issue. This is a joint work with [Kexin Huang](https://www.kexinhuang.com/), [Cao(Danica) Xiao](https://sites.google.com/view/danicaxiao/), Lucas M. Glass and [Jimeng Sun](http://sunlab.org/). 

























