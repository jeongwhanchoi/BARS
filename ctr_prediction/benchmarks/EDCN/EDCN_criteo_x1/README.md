## EDCN_criteo_x1

A hands-on guide to run the EDCN model on the Criteo_x1 dataset.

Author: [XUEPAI](https://github.com/xue-pai)

### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) Gold 6278C CPU @ 2.60GHz
  GPU: Tesla V100 32G
  RAM: 755G

  ```

+ Software

  ```python
  CUDA: 10.2
  python: 3.6.4
  pytorch: 1.0.0
  pandas: 0.22.0
  numpy: 1.19.2
  scipy: 1.5.4
  sklearn: 0.22.1
  pyyaml: 5.4.1
  h5py: 2.8.0
  tqdm: 4.60.0
  fuxictr: 1.2.1

  ```

### Dataset
Dataset ID: [Criteo_x1](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/Criteo#Criteo_x1). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.2.1](https://github.com/xue-pai/FuxiCTR/tree/v1.2.1) for this experiment. See the model code: [EDCN](https://github.com/xue-pai/FuxiCTR/blob/v1.2.1/fuxictr/pytorch/models/EDCN.py).

Running steps:

1. Download [FuxiCTR-v1.2.1](https://github.com/xue-pai/FuxiCTR/archive/refs/tags/v1.2.1.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Criteo/Criteo_x1`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [EDCN_criteo_x1_tuner_config_03](./EDCN_criteo_x1_tuner_config_03). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd EDCN_criteo_x1
    nohup python run_expid.py --config ./EDCN_criteo_x1_tuner_config_03 --expid EDCN_criteo_x1_005_5065d102 --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

| AUC | logloss  |
|:--------------------:|:--------------------:|
| 0.814837 | 0.437013  |


### Logs
```python
2022-05-28 11:24:28,847 P96652 INFO {
    "batch_norm": "True",
    "batch_size": "4096",
    "bridge_type": "hadamard_product",
    "data_format": "csv",
    "data_root": "../data/Criteo/",
    "dataset_id": "criteo_x1_7b681156",
    "debug": "False",
    "embedding_dim": "10",
    "embedding_regularizer": "1e-05",
    "epochs": "100",
    "every_x_epochs": "1",
    "feature_cols": "[{'active': True, 'dtype': 'float', 'name': ['I1', 'I2', 'I3', 'I4', 'I5', 'I6', 'I7', 'I8', 'I9', 'I10', 'I11', 'I12', 'I13'], 'type': 'numeric'}, {'active': True, 'dtype': 'float', 'name': ['C1', 'C2', 'C3', 'C4', 'C5', 'C6', 'C7', 'C8', 'C9', 'C10', 'C11', 'C12', 'C13', 'C14', 'C15', 'C16', 'C17', 'C18', 'C19', 'C20', 'C21', 'C22', 'C23', 'C24', 'C25', 'C26'], 'type': 'categorical'}]",
    "gpu": "4",
    "hidden_activations": "ReLU",
    "label_col": "{'dtype': 'float', 'name': 'label'}",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['AUC', 'logloss']",
    "min_categr_count": "1",
    "model": "EDCN",
    "model_id": "EDCN_criteo_x1_005_5065d102",
    "model_root": "./Criteo/EDCN_criteo_x1/",
    "monitor": "AUC",
    "monitor_mode": "max",
    "net_dropout": "0.2",
    "net_regularizer": "0",
    "num_cross_layers": "4",
    "num_workers": "3",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "save_best_only": "True",
    "seed": "2021",
    "shuffle": "True",
    "task": "binary_classification",
    "temperature": "5",
    "test_data": "../data/Criteo/Criteo_x1/test.csv",
    "train_data": "../data/Criteo/Criteo_x1/train.csv",
    "use_hdf5": "True",
    "use_regulation_module": "True",
    "valid_data": "../data/Criteo/Criteo_x1/valid.csv",
    "verbose": "0",
    "version": "pytorch"
}
2022-05-28 11:24:28,847 P96652 INFO Set up feature encoder...
2022-05-28 11:24:28,847 P96652 INFO Load feature_map from json: ../data/Criteo/criteo_x1_7b681156/feature_map.json
2022-05-28 11:24:28,848 P96652 INFO Loading data...
2022-05-28 11:24:28,849 P96652 INFO Loading data from h5: ../data/Criteo/criteo_x1_7b681156/train.h5
2022-05-28 11:24:34,110 P96652 INFO Loading data from h5: ../data/Criteo/criteo_x1_7b681156/valid.h5
2022-05-28 11:24:35,430 P96652 INFO Train samples: total/33003326, pos/8456369, neg/24546957, ratio/25.62%, blocks/1
2022-05-28 11:24:35,430 P96652 INFO Validation samples: total/8250124, pos/2114300, neg/6135824, ratio/25.63%, blocks/1
2022-05-28 11:24:35,430 P96652 INFO Loading train data done.
2022-05-28 11:24:41,022 P96652 INFO Total number of parameters: 21483963.
2022-05-28 11:24:41,022 P96652 INFO Start training: 8058 batches/epoch
2022-05-28 11:24:41,022 P96652 INFO ************ Epoch=1 start ************
2022-05-28 11:45:31,965 P96652 INFO [Metrics] AUC: 0.804447 - logloss: 0.446781
2022-05-28 11:45:31,966 P96652 INFO Save best model: monitor(max): 0.804447
2022-05-28 11:45:32,238 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 11:45:32,281 P96652 INFO Train loss: 0.461943
2022-05-28 11:45:32,281 P96652 INFO ************ Epoch=1 end ************
2022-05-28 12:06:21,682 P96652 INFO [Metrics] AUC: 0.806691 - logloss: 0.444953
2022-05-28 12:06:21,684 P96652 INFO Save best model: monitor(max): 0.806691
2022-05-28 12:06:21,781 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 12:06:21,828 P96652 INFO Train loss: 0.456041
2022-05-28 12:06:21,828 P96652 INFO ************ Epoch=2 end ************
2022-05-28 12:27:09,197 P96652 INFO [Metrics] AUC: 0.807770 - logloss: 0.443939
2022-05-28 12:27:09,199 P96652 INFO Save best model: monitor(max): 0.807770
2022-05-28 12:27:09,299 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 12:27:09,350 P96652 INFO Train loss: 0.454556
2022-05-28 12:27:09,350 P96652 INFO ************ Epoch=3 end ************
2022-05-28 12:47:54,908 P96652 INFO [Metrics] AUC: 0.808455 - logloss: 0.443738
2022-05-28 12:47:54,909 P96652 INFO Save best model: monitor(max): 0.808455
2022-05-28 12:47:55,014 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 12:47:55,062 P96652 INFO Train loss: 0.453836
2022-05-28 12:47:55,062 P96652 INFO ************ Epoch=4 end ************
2022-05-28 13:08:39,554 P96652 INFO [Metrics] AUC: 0.808899 - logloss: 0.442658
2022-05-28 13:08:39,555 P96652 INFO Save best model: monitor(max): 0.808899
2022-05-28 13:08:39,663 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 13:08:39,712 P96652 INFO Train loss: 0.453298
2022-05-28 13:08:39,712 P96652 INFO ************ Epoch=5 end ************
2022-05-28 13:29:21,900 P96652 INFO [Metrics] AUC: 0.809151 - logloss: 0.442369
2022-05-28 13:29:21,901 P96652 INFO Save best model: monitor(max): 0.809151
2022-05-28 13:29:22,007 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 13:29:22,059 P96652 INFO Train loss: 0.452919
2022-05-28 13:29:22,059 P96652 INFO ************ Epoch=6 end ************
2022-05-28 13:50:01,782 P96652 INFO [Metrics] AUC: 0.809572 - logloss: 0.442065
2022-05-28 13:50:01,784 P96652 INFO Save best model: monitor(max): 0.809572
2022-05-28 13:50:01,882 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 13:50:01,933 P96652 INFO Train loss: 0.452610
2022-05-28 13:50:01,933 P96652 INFO ************ Epoch=7 end ************
2022-05-28 14:10:37,604 P96652 INFO [Metrics] AUC: 0.809791 - logloss: 0.442213
2022-05-28 14:10:37,605 P96652 INFO Save best model: monitor(max): 0.809791
2022-05-28 14:10:37,700 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 14:10:37,743 P96652 INFO Train loss: 0.452375
2022-05-28 14:10:37,743 P96652 INFO ************ Epoch=8 end ************
2022-05-28 14:31:08,858 P96652 INFO [Metrics] AUC: 0.809863 - logloss: 0.442230
2022-05-28 14:31:08,859 P96652 INFO Save best model: monitor(max): 0.809863
2022-05-28 14:31:08,962 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 14:31:09,007 P96652 INFO Train loss: 0.452176
2022-05-28 14:31:09,007 P96652 INFO ************ Epoch=9 end ************
2022-05-28 14:51:36,269 P96652 INFO [Metrics] AUC: 0.810076 - logloss: 0.441605
2022-05-28 14:51:36,270 P96652 INFO Save best model: monitor(max): 0.810076
2022-05-28 14:51:36,378 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 14:51:36,426 P96652 INFO Train loss: 0.452007
2022-05-28 14:51:36,426 P96652 INFO ************ Epoch=10 end ************
2022-05-28 15:11:58,659 P96652 INFO [Metrics] AUC: 0.810190 - logloss: 0.441567
2022-05-28 15:11:58,660 P96652 INFO Save best model: monitor(max): 0.810190
2022-05-28 15:11:58,754 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 15:11:58,804 P96652 INFO Train loss: 0.451865
2022-05-28 15:11:58,804 P96652 INFO ************ Epoch=11 end ************
2022-05-28 15:32:19,156 P96652 INFO [Metrics] AUC: 0.810220 - logloss: 0.441478
2022-05-28 15:32:19,157 P96652 INFO Save best model: monitor(max): 0.810220
2022-05-28 15:32:19,272 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 15:32:19,321 P96652 INFO Train loss: 0.451767
2022-05-28 15:32:19,321 P96652 INFO ************ Epoch=12 end ************
2022-05-28 15:52:34,840 P96652 INFO [Metrics] AUC: 0.810260 - logloss: 0.441554
2022-05-28 15:52:34,842 P96652 INFO Save best model: monitor(max): 0.810260
2022-05-28 15:52:34,944 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 15:52:35,005 P96652 INFO Train loss: 0.451671
2022-05-28 15:52:35,005 P96652 INFO ************ Epoch=13 end ************
2022-05-28 16:12:50,782 P96652 INFO [Metrics] AUC: 0.810452 - logloss: 0.441271
2022-05-28 16:12:50,783 P96652 INFO Save best model: monitor(max): 0.810452
2022-05-28 16:12:50,886 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 16:12:50,933 P96652 INFO Train loss: 0.451572
2022-05-28 16:12:50,933 P96652 INFO ************ Epoch=14 end ************
2022-05-28 16:33:06,625 P96652 INFO [Metrics] AUC: 0.810624 - logloss: 0.441057
2022-05-28 16:33:06,626 P96652 INFO Save best model: monitor(max): 0.810624
2022-05-28 16:33:06,730 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 16:33:06,780 P96652 INFO Train loss: 0.451454
2022-05-28 16:33:06,781 P96652 INFO ************ Epoch=15 end ************
2022-05-28 16:53:23,644 P96652 INFO [Metrics] AUC: 0.810650 - logloss: 0.441288
2022-05-28 16:53:23,645 P96652 INFO Save best model: monitor(max): 0.810650
2022-05-28 16:53:23,752 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 16:53:23,792 P96652 INFO Train loss: 0.451392
2022-05-28 16:53:23,793 P96652 INFO ************ Epoch=16 end ************
2022-05-28 17:13:40,606 P96652 INFO [Metrics] AUC: 0.810762 - logloss: 0.441195
2022-05-28 17:13:40,607 P96652 INFO Save best model: monitor(max): 0.810762
2022-05-28 17:13:40,709 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 17:13:40,756 P96652 INFO Train loss: 0.451282
2022-05-28 17:13:40,756 P96652 INFO ************ Epoch=17 end ************
2022-05-28 17:33:55,221 P96652 INFO [Metrics] AUC: 0.810703 - logloss: 0.440986
2022-05-28 17:33:55,222 P96652 INFO Monitor(max) STOP: 0.810703 !
2022-05-28 17:33:55,222 P96652 INFO Reduce learning rate on plateau: 0.000100
2022-05-28 17:33:55,222 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 17:33:55,272 P96652 INFO Train loss: 0.451237
2022-05-28 17:33:55,272 P96652 INFO ************ Epoch=18 end ************
2022-05-28 17:54:06,886 P96652 INFO [Metrics] AUC: 0.813759 - logloss: 0.438182
2022-05-28 17:54:06,887 P96652 INFO Save best model: monitor(max): 0.813759
2022-05-28 17:54:06,988 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 17:54:07,038 P96652 INFO Train loss: 0.441784
2022-05-28 17:54:07,038 P96652 INFO ************ Epoch=19 end ************
2022-05-28 18:14:20,364 P96652 INFO [Metrics] AUC: 0.814299 - logloss: 0.437759
2022-05-28 18:14:20,365 P96652 INFO Save best model: monitor(max): 0.814299
2022-05-28 18:14:20,466 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 18:14:20,514 P96652 INFO Train loss: 0.437879
2022-05-28 18:14:20,514 P96652 INFO ************ Epoch=20 end ************
2022-05-28 18:24:13,330 P96652 INFO [Metrics] AUC: 0.814434 - logloss: 0.437542
2022-05-28 18:24:13,331 P96652 INFO Save best model: monitor(max): 0.814434
2022-05-28 18:24:13,433 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 18:24:13,470 P96652 INFO Train loss: 0.436047
2022-05-28 18:24:13,470 P96652 INFO ************ Epoch=21 end ************
2022-05-28 18:33:17,895 P96652 INFO [Metrics] AUC: 0.814342 - logloss: 0.437733
2022-05-28 18:33:17,896 P96652 INFO Monitor(max) STOP: 0.814342 !
2022-05-28 18:33:17,896 P96652 INFO Reduce learning rate on plateau: 0.000010
2022-05-28 18:33:17,896 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 18:33:17,941 P96652 INFO Train loss: 0.434592
2022-05-28 18:33:17,941 P96652 INFO ************ Epoch=22 end ************
2022-05-28 18:42:16,197 P96652 INFO [Metrics] AUC: 0.813711 - logloss: 0.438639
2022-05-28 18:42:16,198 P96652 INFO Monitor(max) STOP: 0.813711 !
2022-05-28 18:42:16,198 P96652 INFO Reduce learning rate on plateau: 0.000001
2022-05-28 18:42:16,198 P96652 INFO Early stopping at epoch=23
2022-05-28 18:42:16,198 P96652 INFO --- 8058/8058 batches finished ---
2022-05-28 18:42:16,236 P96652 INFO Train loss: 0.430363
2022-05-28 18:42:16,236 P96652 INFO Training finished.
2022-05-28 18:42:16,236 P96652 INFO Load best model: /cache/FuxiCTR/benchmarks/Criteo/EDCN_criteo_x1/criteo_x1_7b681156/EDCN_criteo_x1_005_5065d102.model
2022-05-28 18:42:20,649 P96652 INFO ****** Validation evaluation ******
2022-05-28 18:42:48,324 P96652 INFO [Metrics] AUC: 0.814434 - logloss: 0.437542
2022-05-28 18:42:48,409 P96652 INFO ******** Test evaluation ********
2022-05-28 18:42:48,410 P96652 INFO Loading data...
2022-05-28 18:42:48,411 P96652 INFO Loading data from h5: ../data/Criteo/criteo_x1_7b681156/test.h5
2022-05-28 18:42:49,209 P96652 INFO Test samples: total/4587167, pos/1174769, neg/3412398, ratio/25.61%, blocks/1
2022-05-28 18:42:49,209 P96652 INFO Loading test data done.
2022-05-28 18:43:04,646 P96652 INFO [Metrics] AUC: 0.814837 - logloss: 0.437013

```
