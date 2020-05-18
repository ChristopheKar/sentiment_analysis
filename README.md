# Sentiment Classification

This repository serves a documentation for the work done on classyfing sentiments during the Spring 2019-2020 term. The models, datasets, and experiment outline are the result of Layal Al Khuja's work, and the implementation is coded by Christophe Karam.
The repository contains Jupyter notebooks containing the code necessary to run each bundle of experiments (along with the proper environment setup and data processing). The repository also contains the datasets used, and instructions on how to run everything.
The following are thoughts on the experimentation, the models, and the datasets, which can be used as a basis for future research.

First of all, the experiment plan proposed by Layal involved 11 different models and 3 different datasets, as outlined in the `expriment_plan.pdf` document. GitHub links were provided for all of the models except for 3 of them (so 8/11 available GitHub repositories). I debugged and ran the codes from the provided repositories for the experiments, except when the code was really messed up, in which case I searched for different repositories. In total, I was able to run 6 out of the 11 requested experiments (3 without any found/provided repositories and 2 that were not compatible with the datasets, explanation will follow).

1. The Decision-CNN and multichannel-CNN were tested on all datasets and they are suitable for the classification task we are trying to solve, They achieve good results based on the depth of the model and other optimizations. Nothing to say here.
2. I was asked to test Tree-LSTM on the SemEval and SentiHood datasets, because it was only tested on the Stanford TreeBank dataset (SST). I did not run this experiment because the Tree-LSTM model supposes the dataset is organized in a tree structure, like SST, and this is impossible to train on the other datasets because they are not labeled in this way. There are no ways around it.
3. The BiLSTM-CRF model's goal is to extract part-of-speech tags from sentences, and is not suitable for a sentiment classification task. This experiment was also not run.
4. The remaining models are either target-dependent or aspect-dependent or both, and so they cannot be trained on datasets which are not labeled in a way that respects this structure. The SST datasets contains no target information and no aspect information, for example. I had brought this concern to Layal and she suggested a way around this by feeding a null aspect or target vector to the model. The practical way around this was that I found was to duplicate the sentence and mark each word in it as the target, so a sort of unity aspect/target vector instead of a null one, since this was easier to implement in the already confusing mess of the codes. However, the models trained this way lead to bad results, and the training also defeats the purpose of the model, and does not allow for a fair comparison between models or datasets. At this point, we're better off training a simple LSTM for this purpose, without getting involved in the target or aspect dependency for datasets which are structured differently.

## Instructions

All Jupyter notebooks can be run in a Google Colab environment or any other environment.
In any environment, the files dataset.zip and utils.py should be placed in the same directory as the Jupyter notebooks.

For use in Google Colab:
- Upload the Jupyter notebook to you Google Drive folder.
- Right-click on the notebook and open with Google Colab.
- In Colab, specify the runtime acceleration as 'GPU' or 'TPU' (in Runtime --> Change Runtime Type)
- On the left-hand side panel, go to the files tab and upload the dataset.zip and utils.py files.
- Run the cells as instructed in the notebook.

Contact me for any questions:\
Christophe Karam\
cbk02@mail.aub.edu\
karam.christophe@gmail.com

## Results

### LSTMs

TD-LSTM on SST1 >>> test accuracy 23.9827\
TC-LSTM on SST1 >>> test accuracy 23.9827\
TD-LSTM on SST2 >>> test accuracy 50.3172\
TC-LSTM on SST2 >>> test accuracy 50.3172

-----------------------------------------

AT-LSTM on SST1 >>> test accuracy 32.4905\
AE-LSTM on SST1 >>> test accuracy \
AT-LSTM on SST2 >>> test accuracy 71.9846\
AE-LSTM on SST2 >>> test accuracy \
AT-LSTM on SentiHood >>> test accuracy \
AE-LSTM on SentiHood >>> test accuracy


## DCNN
DCNN on all Datasets

**SST-1**: 5 classes

Basic Dynamic CNN:
Training: 71.10%
Validation: 57.64%
Testing: 58.29%

Two-Conv Dynamic CNN:
Training: 63.66%
Validation: 59.93%
Testing: 57.64%

Two-Feature-Map Dynamic CNN:
Training: 65.18%
Validation: 53.69%
Testing: 56.48%


**SST-2**: 2 classes

Basic Dynamic CNN:
Training: 99.86%
Validation: 76.40%
Testing: 78.32%

Two-Conv Dynamic CNN:
Training: 99.71%
Validation: 76.06%
Testing: 77.06%

Two-Feature-Map Dynamic CNN:
Training: 99.81%
Validation: 78.01%
Testing: 77.66%

**SentiHood**: 2 classes

Basic Dynamic CNN:
Training: 76.94 %
Validation: 75.84 %
Testing: 73.78 %

Two-Conv Dynamic CNN:
Training: 75.9 %
Validation: 75.25 %
Testing: 72.98 %

Two-Feature-Map Dynamic CNN:
Training: 74.37 %
Validation: 74.65 %
Testing: 73.08 %

**SemEval**: 3 classes

Basic Dynamic CNN:
Training: 73.77 %
Validation: 60.43 %
Testing: 61.08 %

Two-Conv Dynamic CNN:
Training: 64.11 %
Validation: 58.62 %
Testing: 57.96 %

Two-Feature-Map Dynamic CNN:
Training: 62.82 %
Validation: 55.67 %
Testing: 56.81 %

### MultiChannelCNN

**SST-1**: 5 classes
Training: 39.31%
Validation: 36.30%
Testing: 37.22%

**SST-2**: 2 classes
Training: 74.45%
Validation: 72.16%
Testing: 72.39%

**SentiHood**: 2 classes
Training: 80.65%
Validation: 72.87%
Testing: 72.18%

**SemEval**: 3 classes
Training: 65.55%
Validation: 63.05%
Testing: 57.64


## Model Number of Parameters
Basic Dynamic CNN: 1,076,305\
Two Conv Dynamic CNN: 1,127,605\
Two Feature Map Dynamic CNN: 1,255,205\
MultiChannel CNN: 8,814 (5,860,800 non-trainable)\
AT-LSTM: 67,594,505\
TD-LSTM: 483,605\
TC-LSTM: 643,605
