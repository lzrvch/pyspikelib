# Spikebench: an open benchmark for spike train time-series classification

by
Ivan Lazarevich,
Ilya Prokin,
Boris Gutkin,
Victor Kazantsev

We propose _spikebench_ — a benchmark consisting of several individual neuron spike train classification tasks based on open-access data from a range of animals and brain regions. We demonstrate that it is possible to achieve meaningful results in such a challenging benchmark using the massive time-series feature extraction approach, which is found to perform similarly to state-of-the-art deep learning approaches.

[Biorxiv link](https://www.biorxiv.org/content/10.1101/2021.03.24.436765v2)

## Abstract

Modern well-performing approaches to neural decoding are based on machine learning models such as decision tree ensembles and deep neural networks. The wide range of algorithms that can be utilized to learn from neural spike trains, which are essentially time-series data, results in the need for diverse and challenging benchmarks for neural decoding, similar to the ones in the fields of computer vision and natural language processing. In this work, we propose a spike train classification benchmark, based on open-access neural activity datasets and consisting of several learning tasks such as stimulus type classification, animal's behavioral state prediction and neuron type identification. We demonstrate that an approach based on hand-crafted time-series feature engineering establishes a strong baseline performing on par with state-of-the-art deep learning based models for neural decoding.


## Software implementation

All scripts used to generate the results and figures in the paper are in
the `paper_figures` folder (results generated by the code are saved in `paper_figures/csv`).

Minimalistic examples of benchmark usage are located in `examples`.

To get started, also have a look at the [colab notebook](https://colab.research.google.com/drive/1uDf81g1dwQ5LcYu-RBxWcVJBpEt0fcbb?usp=sharing).

## API

To download and preprocess the data one could use the loading methods

```{.python}
from spikebench import load_allen
from spikebench import load_fcx1
from spikebench import load_retina

X_train, X_test, y_train, y_test, groups_train, groups_test = load_retina()
```
where `groups_train`, `groups_test` are neuron identifiers for samples in the training and testing set, respectively.

The signature of all loader methods is the same (default values correspond to the ones used in the paper):

```{.python}
dataset_path, # location where the data will be downloaded to (if not already)
random_seed, # random seed to generate train/test splits
test_size, # float from 0 to 1 for the ratio of the testing set size
window_size, # length of each time series sample (# ISIs per sample)
step_size, # rolling window step (# ISIs) to generate samples
encoding, # string equal to "isi" (ISI encoding) or "sce" (binned spike count encoding)
bin_size, # bin size in case of binned spike count encoding
```
