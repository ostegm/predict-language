# Predicting Language From Text
This repo is contains the scripts and notebooks used to train a convolutional neural network on a corpus of text and predict the language of that text


### Info on the raw data
The data is pulled from [statmt.org](http://www.statmt.org/europarl/) and comes as zipped directory containing many text files grouped into subdirectories by language. 

The follwing is an example of the original data:
```
├── en
|   ├── ep-00-01-17.txt
|   └── ep-00-01-18.txt
|   └──...
├── es
|   ├── ep-00-01-17.txt
|   └── ep-00-01-18.txt
|   └──...
├── ...
```


### Preparation Steps

Prior to running the CNN against the labeled data, we need to do some cleaning steps. The "exploratory work" notebook is the notebook used to perform these steps. 

- Split each sentence at 70 words. Pad any sentences shorter than 70 words with the special <PAD> token to all other sentences to make them 70 words. Padding sentences to the same length is useful because it allows us to efficiently batch our data since each example in a batch must be of the same length.
- Build a vocabulary index and map each word to an integer between 0 and N (the vocabulary size).
- Convert each sentence into a vector of integers.

### Training
Basing the neural network on a [WildMl.org blog post](https://github.com/dennybritz/cnn-text-classification-tf) that aims to predict sentiment from movie reviews. The WildML post has references to 2014 [paper by Kim Yoon](https://arxiv.org/abs/1408.5882) 

Layers used in the model: 
- Embedding layer: generate vector representations of individual words.
- Series of convolutions and filters: Each convolution follows a pattern: 
--convole the input data using valid padding. 
-- Apply a relu for potential non-linearity
-- Apply max pooling over the output of the relu
-- (optional) repeat with next Filter size
- Finally, apply dropout and calculate Mean X-entropy loss.

During the first attempt at running the model, was able to achieve 98.4% accuray on a validation data set. Next step is to test on a new set of data using this checkpointed model. Results from first run: 

![](misc/first_cnn.png?raw=true)

### TODO's
- Rework preparation step to use the TF.learn vocab preprocessing tool. 
- Prep step should produce many smaller files with languages in proportion to the original set. Currently just random. 
- visualization of the word embeddings
- Imvproved cross validation during training
- Evaluation step on outside data to see if I can achieve similar accuracy. 
- Hyperparameter tuning