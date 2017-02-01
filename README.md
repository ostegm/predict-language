# Predicting Language From Text
This repo is contains the scripts and notebooks used to train a convolutional neural network (+LSTM) on a corpus of text and predict the language of that text with 99% accuracy. 

### Training
Initially, I based the neural network on a [WildMl.org blog post](https://github.com/dennybritz/cnn-text-classification-tf) that aims to predict sentiment from movie reviews. The WildML post has references to 2014 [paper by Kim Yoon](https://arxiv.org/abs/1408.5882). I found this to only achieve ~98% acc, so I chose to try out other architectures. The final architecture I settled on was a combination of CNN + LSTM, which achieved 99.7% accuracy on a [held out set of 21k records](https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/language-detection/europarl-test.zip) provided by [Startup.ml](https://startup.ml/challenge)

Layers used in training the model: 
- Embedding layer: generate vector representations of individual words. (+ dropout)
- A single 1D convolutional layer
-- convole the input data using a 5x64 filter with valid padding. 
-- Apply a relu for potential non-linearity
-- Apply max pooling over the output of the relu (stride of 4)
- An LSTM layer
- Finally, a fully connected layer with sigmoid activation. 

The Normalized Confusion Matrix from the CNN + LSTM Architecture
  
![](misc/conf_matrix.png?raw=true)

Demonstrating the plateauing training results from the first Achitecture: 

![](misc/first_cnn.png?raw=true)


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

Prior to running the CNN against any labeled data (for testing or training), we need to do some cleaning steps. The "exploratory work" notebook is the notebook used to perform these steps. 

- Strip XML from the raw data since many lines in the raw data weren't meant to be used in training. 
- Split each sentence at 70 words. Pad any sentences shorter than 70 words with the special <PAD> token to all other sentences to make them 70 words. Padding sentences to the same length is useful because it allows us to efficiently batch our data since each example in a batch must be of the same length.
- Build a vocabulary index and map each word to an integer between 0 and N (the vocabulary size).
- Convert each sentence into a vector of integers.



### Links to Files to Reproduce (too large to host here)
- [Training Data cleaned and prepped](https://s3.amazonaws.com/predict-lang/mapped_data_0.zip) - A random sample of 600k records from the original corups, mapped to integer word represenations. 
- [Tensorflow Vocab Processor](https://s3.amazonaws.com/predict-lang/20160113.vocab) - for mapping between integer word index and actual word from the raw text
- [Startup.ml Test Set Converted to Integers](https://s3.amazonaws.com/predict-lang/startup_test_set.pkl)

