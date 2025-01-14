## DeepFM_frappe_x1

A hands-on guide to run the DeepFM model on the Frappe_x1 dataset.

Author: [XUEPAI](https://github.com/xue-pai)

### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) CPU E5-2690 v4 @ 2.6GHz
  GPU: Tesla P100 16G
  RAM: 755G

  ```

+ Software

  ```python
  CUDA: 11.4
  python: 3.6.5
  pytorch: 1.0.1.post2
  pandas: 0.23.0
  numpy: 1.18.1
  scipy: 1.1.0
  sklearn: 0.23.1
  pyyaml: 5.1
  h5py: 2.7.1
  tqdm: 4.59.0
  fuxictr: 1.1.0
  ```

### Dataset
Dataset ID: [Frappe_x1](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/Frappe/README.md#Frappe_x1). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/tree/v1.1.0) for this experiment. See the model code: [DeepFM](https://github.com/xue-pai/FuxiCTR/blob/v1.1.0/fuxictr/pytorch/models/DeepFM.py).

Running steps:

1. Download [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/archive/refs/tags/v1.1.0.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Frappe/Frappe_x1`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [DeepFM_frappe_x1_tuner_config_02](./DeepFM_frappe_x1_tuner_config_02). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd DeepFM_frappe_x1
    nohup python run_expid.py --config ./DeepFM_frappe_x1_tuner_config_02 --expid DeepFM_frappe_x1_001_4ae3a56e --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

Total 5 runs:

| Runs | AUC | logloss  |
|:--------------------:|:--------------------:|:--------------------:|
| 1 | 0.984243 | 0.148174  |
| 2 | 0.983888 | 0.150042  |
| 3 | 0.983816 | 0.149387  |
| 4 | 0.983981 | 0.147299  |
| 5 | 0.983806 | 0.152410  |
| Avg | 0.983947 | 0.149462 |
| Std | &#177;0.00016081 | &#177;0.00175330 |


### Logs
```python
2022-02-10 19:31:05,374 P1904 INFO {
    "batch_norm": "True",
    "batch_size": "4096",
    "data_format": "csv",
    "data_root": "../data/Frappe/",
    "dataset_id": "frappe_x1_04e961e9",
    "debug": "False",
    "embedding_dim": "10",
    "embedding_regularizer": "0.05",
    "epochs": "100",
    "every_x_epochs": "1",
    "feature_cols": "[{'active': True, 'dtype': 'float', 'name': ['user', 'item', 'daytime', 'weekday', 'isweekend', 'homework', 'cost', 'weather', 'country', 'city'], 'type': 'categorical'}]",
    "gpu": "0",
    "hidden_activations": "relu",
    "hidden_units": "[400, 400, 400]",
    "label_col": "{'dtype': 'float', 'name': 'label'}",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['AUC', 'logloss']",
    "min_categr_count": "1",
    "model": "DeepFM",
    "model_id": "DeepFM_frappe_x1_001_4ae3a56e",
    "model_root": "./Frappe/DeepFM_frappe_x1/",
    "monitor": "AUC",
    "monitor_mode": "max",
    "net_dropout": "0.2",
    "net_regularizer": "0",
    "num_workers": "3",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "save_best_only": "True",
    "seed": "2021",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Frappe/Frappe_x1/test.csv",
    "train_data": "../data/Frappe/Frappe_x1/train.csv",
    "use_hdf5": "True",
    "valid_data": "../data/Frappe/Frappe_x1/valid.csv",
    "verbose": "1",
    "version": "pytorch"
}
2022-02-10 19:31:05,379 P1904 INFO Set up feature encoder...
2022-02-10 19:31:05,379 P1904 INFO Load feature_map from json: ../data/Frappe/frappe_x1_04e961e9/feature_map.json
2022-02-10 19:31:05,380 P1904 INFO Loading data...
2022-02-10 19:31:05,389 P1904 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/train.h5
2022-02-10 19:31:05,453 P1904 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/valid.h5
2022-02-10 19:31:05,476 P1904 INFO Train samples: total/202027, pos/67604, neg/134423, ratio/33.46%, blocks/1
2022-02-10 19:31:05,476 P1904 INFO Validation samples: total/57722, pos/19063, neg/38659, ratio/33.03%, blocks/1
2022-02-10 19:31:05,476 P1904 INFO Loading train data done.
2022-02-10 19:31:21,867 P1904 INFO Total number of parameters: 423280.
2022-02-10 19:31:21,867 P1904 INFO Start training: 50 batches/epoch
2022-02-10 19:31:21,867 P1904 INFO ************ Epoch=1 start ************
2022-02-10 19:31:33,917 P1904 INFO [Metrics] AUC: 0.937016 - logloss: 0.677712
2022-02-10 19:31:33,925 P1904 INFO Save best model: monitor(max): 0.937016
2022-02-10 19:31:33,946 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:31:34,133 P1904 INFO Train loss: 0.376398
2022-02-10 19:31:34,133 P1904 INFO ************ Epoch=1 end ************
2022-02-10 19:31:46,461 P1904 INFO [Metrics] AUC: 0.962204 - logloss: 0.242437
2022-02-10 19:31:46,469 P1904 INFO Save best model: monitor(max): 0.962204
2022-02-10 19:31:46,496 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:31:46,695 P1904 INFO Train loss: 0.274709
2022-02-10 19:31:46,695 P1904 INFO ************ Epoch=2 end ************
2022-02-10 19:31:58,394 P1904 INFO [Metrics] AUC: 0.973816 - logloss: 0.184279
2022-02-10 19:31:58,395 P1904 INFO Save best model: monitor(max): 0.973816
2022-02-10 19:31:58,470 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:31:58,672 P1904 INFO Train loss: 0.228124
2022-02-10 19:31:58,673 P1904 INFO ************ Epoch=3 end ************
2022-02-10 19:32:09,576 P1904 INFO [Metrics] AUC: 0.977910 - logloss: 0.169551
2022-02-10 19:32:09,581 P1904 INFO Save best model: monitor(max): 0.977910
2022-02-10 19:32:09,598 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:32:09,802 P1904 INFO Train loss: 0.202907
2022-02-10 19:32:09,802 P1904 INFO ************ Epoch=4 end ************
2022-02-10 19:32:22,289 P1904 INFO [Metrics] AUC: 0.978548 - logloss: 0.182297
2022-02-10 19:32:22,289 P1904 INFO Save best model: monitor(max): 0.978548
2022-02-10 19:32:22,342 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:32:22,583 P1904 INFO Train loss: 0.190405
2022-02-10 19:32:22,584 P1904 INFO ************ Epoch=5 end ************
2022-02-10 19:32:35,590 P1904 INFO [Metrics] AUC: 0.979666 - logloss: 0.172533
2022-02-10 19:32:35,622 P1904 INFO Save best model: monitor(max): 0.979666
2022-02-10 19:32:35,664 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:32:35,873 P1904 INFO Train loss: 0.184078
2022-02-10 19:32:35,873 P1904 INFO ************ Epoch=6 end ************
2022-02-10 19:32:46,355 P1904 INFO [Metrics] AUC: 0.981040 - logloss: 0.162076
2022-02-10 19:32:46,355 P1904 INFO Save best model: monitor(max): 0.981040
2022-02-10 19:32:46,379 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:32:46,511 P1904 INFO Train loss: 0.177385
2022-02-10 19:32:46,512 P1904 INFO ************ Epoch=7 end ************
2022-02-10 19:32:58,637 P1904 INFO [Metrics] AUC: 0.980844 - logloss: 0.186768
2022-02-10 19:32:58,637 P1904 INFO Monitor(max) STOP: 0.980844 !
2022-02-10 19:32:58,638 P1904 INFO Reduce learning rate on plateau: 0.000100
2022-02-10 19:32:58,638 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:32:58,844 P1904 INFO Train loss: 0.174715
2022-02-10 19:32:58,844 P1904 INFO ************ Epoch=8 end ************
2022-02-10 19:33:12,253 P1904 INFO [Metrics] AUC: 0.983941 - logloss: 0.140568
2022-02-10 19:33:12,254 P1904 INFO Save best model: monitor(max): 0.983941
2022-02-10 19:33:12,305 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:33:12,502 P1904 INFO Train loss: 0.146955
2022-02-10 19:33:12,502 P1904 INFO ************ Epoch=9 end ************
2022-02-10 19:33:25,564 P1904 INFO [Metrics] AUC: 0.984717 - logloss: 0.138608
2022-02-10 19:33:25,566 P1904 INFO Save best model: monitor(max): 0.984717
2022-02-10 19:33:25,597 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:33:25,794 P1904 INFO Train loss: 0.123157
2022-02-10 19:33:25,795 P1904 INFO ************ Epoch=10 end ************
2022-02-10 19:33:37,092 P1904 INFO [Metrics] AUC: 0.985039 - logloss: 0.138747
2022-02-10 19:33:37,092 P1904 INFO Save best model: monitor(max): 0.985039
2022-02-10 19:33:37,120 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:33:37,292 P1904 INFO Train loss: 0.109935
2022-02-10 19:33:37,292 P1904 INFO ************ Epoch=11 end ************
2022-02-10 19:33:49,292 P1904 INFO [Metrics] AUC: 0.985142 - logloss: 0.140442
2022-02-10 19:33:49,311 P1904 INFO Save best model: monitor(max): 0.985142
2022-02-10 19:33:49,337 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:33:49,486 P1904 INFO Train loss: 0.098911
2022-02-10 19:33:49,486 P1904 INFO ************ Epoch=12 end ************
2022-02-10 19:34:00,248 P1904 INFO [Metrics] AUC: 0.985168 - logloss: 0.142101
2022-02-10 19:34:00,249 P1904 INFO Save best model: monitor(max): 0.985168
2022-02-10 19:34:00,295 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:34:00,458 P1904 INFO Train loss: 0.091437
2022-02-10 19:34:00,458 P1904 INFO ************ Epoch=13 end ************
2022-02-10 19:34:11,109 P1904 INFO [Metrics] AUC: 0.984989 - logloss: 0.145891
2022-02-10 19:34:11,128 P1904 INFO Monitor(max) STOP: 0.984989 !
2022-02-10 19:34:11,129 P1904 INFO Reduce learning rate on plateau: 0.000010
2022-02-10 19:34:11,130 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:34:11,268 P1904 INFO Train loss: 0.084724
2022-02-10 19:34:11,268 P1904 INFO ************ Epoch=14 end ************
2022-02-10 19:34:19,498 P1904 INFO [Metrics] AUC: 0.984997 - logloss: 0.146024
2022-02-10 19:34:19,499 P1904 INFO Monitor(max) STOP: 0.984997 !
2022-02-10 19:34:19,499 P1904 INFO Reduce learning rate on plateau: 0.000001
2022-02-10 19:34:19,499 P1904 INFO Early stopping at epoch=15
2022-02-10 19:34:19,499 P1904 INFO --- 50/50 batches finished ---
2022-02-10 19:34:19,614 P1904 INFO Train loss: 0.078596
2022-02-10 19:34:19,614 P1904 INFO Training finished.
2022-02-10 19:34:19,615 P1904 INFO Load best model: /home/XXX/FuxiCTR/benchmarks/Frappe/DeepFM_frappe_x1/frappe_x1_04e961e9/DeepFM_frappe_x1_001_4ae3a56e.model
2022-02-10 19:34:19,652 P1904 INFO ****** Validation evaluation ******
2022-02-10 19:34:21,761 P1904 INFO [Metrics] AUC: 0.985168 - logloss: 0.142101
2022-02-10 19:34:22,024 P1904 INFO ******** Test evaluation ********
2022-02-10 19:34:22,024 P1904 INFO Loading data...
2022-02-10 19:34:22,041 P1904 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/test.h5
2022-02-10 19:34:22,051 P1904 INFO Test samples: total/28860, pos/9536, neg/19324, ratio/33.04%, blocks/1
2022-02-10 19:34:22,051 P1904 INFO Loading test data done.
2022-02-10 19:34:23,393 P1904 INFO [Metrics] AUC: 0.984243 - logloss: 0.148174

```
