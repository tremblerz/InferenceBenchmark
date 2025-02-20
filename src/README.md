# Usage
`python main.py`

`python main.py -b split_inference.json`

`python main.py -s system_config.json`

`python main.py -b split_inference.json -s system_config.json`

# Components
Like almost any other machine learning project, this benchmark also has standard components like data processing pipeling, models and etc. There are some components that are uniquely designed for this project. Such components include algorithms and evaluation metrics. All components are tied up together with the interface
## Benchmark specification
There are two separate configuration files that are used to specify a benchmark. One is system level configuration file used for specifying file paths and other infrastructure related information. The benchmark config consists of benchmark specific and system independent parameters. The `method` key indicates which technique is used to run the benchmark. The `exp_keys` key is a list of multiple nested keys that is used to have dynamic control on the experiments folder name which could be useful for experiments logging and comparison using either logs or tensorboard.
There are three different modes in which these experiments can be performed - "defense", "challenge", "attack". This has to be specified in the key `experiment_type`. By default, the `experiment_type` is set as "defense".
## Models
Currently supports ResNet-18 for different mechanisms with varying `split_layer`.
## Datasets
## Algorithms
Currently supported algorithms on the defense side include. These algorithms work for variable number of client side `split_layer`.
1. Split Inference `split_inference.json`
2. Uniform noise (currently supports Laplace and Gaussian distribution) `uniform_noise.json`
3. NoPeek `nopeek.json`
4. Siamese Embedding `siamese_embedding.json`
5. PCA Embedding `pca_embedding.json`

### Writing your own algorithm
Most of the code in the algos is modular enough for a user to only focus on writing the important part of the mechanism and rest all functions automatically. Implementor of a mechanism just needs to inherit the `SimbaDefense` class from `algos.simba_algo`. A user can also build upon existing mechanisms by inheriting them and overriding a particular function of the algorithm.
## Evaluation
Evaluation involves two category of metrics. One category of metric is specific to the algorithm and the other category of metric is generic for all of the algorithms and used for benchmarking.
## Scheduler
