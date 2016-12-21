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
