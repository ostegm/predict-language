# Predicting Language From Text
This repo is contains the scripts and notebooks used to train a convolutional neural network on a corpus of text and predict the language of that text

Basing the CNN work on the Blog post here: https://github.com/dennybritz/cnn-text-classification-tf

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
