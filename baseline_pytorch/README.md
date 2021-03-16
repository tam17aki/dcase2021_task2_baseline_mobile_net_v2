# dcase2021_task2_baseline_mobile_net_v2 (PyTorch ver.)
MobileNetV2-based baseline system for DCASE2021 Challenge Task 2 in **PyTorch**.

## Description
This system consists of two main scripts:
- `training.py`
  - "Development" mode: 
    - This script trains a model for each machine type by using the directory `dev_data/<machine_type>/train/`.
  - "Evaluation" mode: 
    - This script trains a model for each machine type by using the directory `eval_data/<machine_type>/train/`. (This directory will be from the "additional training dataset".)
- `test.py`
  - "Development" mode:
    - This script makes a csv file for each section including the anomaly scores for each wav file in the directories `dev_data/<machine_type>/source_test/` and `dev_data/<machine_type>/target_test/`.
    - The csv files are stored in the directory `result/`.
    - It also makes a csv file including AUC, pAUC, precision, recall, and F1-score for each section.
  - "Evaluation" mode: 
    - This script makes a csv file for each section including the anomaly scores for each wav file in the directories `eval_data/<machine_type>/source_test/` and `eval_data/<machine_type>/target_test/`. (These directories will be from the "evaluation dataset".)
    - The csv files are stored in the directory `result/`.

## Usage
### 1. Clone repository, Download datasets, Unzip dataset
You have already done these steps when you read this document.

### 2. Run training script (for the development dataset)
Run the training script `training.py`. 
Use the option `-d` for the development dataset `dev_data/<machine_type>/train/`.
```
$ python3 training.py -d
```
Options:

| Argument                    |                                   | Description                                                  | 
| --------------------------- | --------------------------------- | ------------------------------------------------------------ | 
| `-h`                        | `--help`                          | Application help.                                            | 
| `-v`                        | `--version`                       | Show application version.                                    | 
| `-d`                        | `--dev`                           | Mode for the development dataset                             |  
| `-e`                        | `--eval`                          | Mode for the additional training and evaluation datasets     | 

`training.py` trains a model for each machine type and store the trained models in the directory `model/`.

### 3. Run test script (for the development dataset)
Run the test script `test.py`.
Use the option `-d` for the development dataset `dev_data/<machine_type>/test/`.
```
$ python3 test.py -d
```
The options for `test.py` are the same as those for `training.py`.
`test.py` calculates an anomaly score for each wav file in the directories `dev_data/<machine_type>/source_test/` and `dev_data/<machine_type>/target_test/`.
A csv file for each section including the anomaly scores will be stored in the directory `result/`.
If the mode is "development", the script also outputs another csv file including AUC, pAUC, precision, recall, and F1-score for each section.

### 4. Check results
You can check the anomaly scores in the csv files `anomaly_score_<machine_type>_section_<section_index>_<domain>_test.csv` in the directory `result/`.

## Dependency
I develop the source code on Ubuntu 18.04 LTS only.

### Software packages
- Python3

### Python packages
- torch                         == 1.7.1
- torchinfo                     == 0.0.8
- torchvision                   == 0.8.2
- numpy                         == 1.20.1
- PyYAML                        == 5.3.1
- scikit-learn                  == 0.24.1
- scipy                         == 1.6.1
- librosa                       == 0.8.0
- setuptools                    == 54.1.1
