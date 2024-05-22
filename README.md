# SPR_classification_DL
## Table of Contents
1. [Introduction](#intro)
2. [Dataset](#dataset)
     1. [Data source](#source)
     2. [Data structure](#structure)
     3. [Data proportions](#ratio)
3. [Implementation](#imp)
     1. [data preparation](#dataperp)
     2. [classification](#class)
4. [Results](#result)
   1. [ResNet 18 using STFT spectrogram](#1)
   2. [ResNet 18 using LOG STFT spectrogram](#2)
   3. [VGG 16 using STFT spectrogram](#3)
   4. [VGG 16 using LOG STFT spectrogram](#4)
5. [Instructions](#instruction)
6. [References](#ref)
7. [Kaggle Datasets](#kdataset)
8. [Kaggle Notebooks](#knote)



<a name="intro"></a>
## Introduction
This project focuses on the classification of breathing sounds at the event level using deep learning models (ResNet 18, VGG16). 

The main objective is to turn the diagnosis from a subjective perspective to an objective one. 

<a name="dataset"></a>
## Dataset
This dataset is unique as it has an age range between 0 and 16.2 years, unlike other open-source datasets that range from pediatrics to old age.

it was taken from 140 female and 152 male.

the method of acquisation was through a digital stethoscope (Yunting model II Stethoscope, Yunting II).
<a name="source"></a>
### Data source 
The dataset used is the [SPR Sound:  SJTU Paediatric Respiratory Sound Database](https://github.com/SJTU-YONGFU-RESEARCH-GRP/SPRSound)

 
<a name="structure"></a>
### Data structure
The data set consists of audio signal (.wav ) and labels in (.json )

Each signal is called ***record*** &
Each record contain multiple ***events***

In the .json file you will find the record and the event annotation.

The record annotation which describe the label of the whole signal could be :

- normal
- poor quality
- CAS
- DAS
- CAS&DAS 

The event annotation contains: 

- the start and end time of the event in record
- the type of event which could be:
  - normal
  -  Fine Crackle
  - Wheeze
  - Coarse-Crackle
  - Rhonchi
  - Wheeze+Crackle
  - Stridor


In case of poor quality the event annotation are empty
<a name="ratio"></a>
### Data proportions
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/dataratio.jpg">
</div>
This plots the data on event level

- 0 is normal
- 1 is abnormal (includes Fine Crackle,Wheeze,Coarse-Crackle,Rhonchi,Wheeze+Crackle,Stridor)
- 2 is poor quality
<a name="imp"></a>
## Implementation
<a name="dataperp"></a>
### Data perparation
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/data perparation.png">
</div>

*this flow chart explain the process that happen in the data preparation notebook*


which starts with a process for handling data from a JSON file. It involves extracting and encoding data 

     - 0 normal
     - 1 abnormal
     - 2 poor quality
then removed poor quality entries and outliers ( the outliers are the events with very long time compared to the rest)
then balancing the dataset by removing the extra normal events to make the no. of normal events equal to the abnormal, then
applying a sound filter (bandpass filter )
,also splitting the data into events, and saving these events into a dataframe called event processed then saving this file as csv 
can be found in kaggle 2 dataset in the [kaggle dataset section](#kdataset)



<a name="class"></a>
### classification

<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/mydataset class.png">
</div>

*flowchart of the mydataset class*

***the function of this class:***

Instead of converting all audio files into spectrograms (which uses alot of  time and memory)and then creating a dataframe, I’ve went for a more efficient approach. I’ve developed a class that accepts an audio file and its corresponding label as inputs. This class is responsible for transforming the audio file into the desired type of spectrogram. Once the spectrogram is generated, it’s saved as a .png image, which is then resized to meet the model’s input requirements of 224x224 pixels. The image is subsequently converted into a tensor. The class returns this tensor along with its label, thereby constructing a dataset ready for use whenever the model requests it.

##### Note that : this is the major difference in code between the two classification notebook as one has stft spectrogram transformation inside the class & the other has log stft


<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/models.png">
</div>

*this flow chart explain the process that happen in the classfication notebook*

to train the model we first split the dataframe (event processed) into train, test & validation (the train test split was 90%,10% respectively) then we feed that dataframe into [the mydatasetclass](#class) explained above , then through the data loader into the model and when the validation accuracy is seen decreasing we stop training then we test and plot as seen below in the [results](#result) .

#### other functions in the notebook

- ##### in the calculate_accuracy function:
  it keeps count of how many times the model gets the correct prediction then divides it by the total number of predictions
- ##### in the plot_metrics function:
  the plotting of the confusion metrics , the ROC and the classification report is placed in a function to make it easier to use and call

### hyper parameters 
`DPI=100`

`figuresize=(2.24,2.24)`

`img_size=(224,224)`

`Batch_size=10`

`learn_rate=0.001`

`Momentum=0.9`

`patience=3 this is for early stopping`

`train_test split was 90% ,10%`
`validation was 10% of the train`

<a name="result"></a>

## Results
<a name="1"></a>
#### This is the output of the **Resnet18** using *stft* spect
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/resnetstftconfusionmatrix.jpg">
</div>
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/resnetstftROC.jpg">
</div>
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/resnetstft.jpg">
</div>

<a name="2"></a>

#### This is the output of the **Resnet18** using *log stft* spect
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/resnetlogconfusionmatrix.jpg">
</div>
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/resnetlogROC.jpg">
</div>
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/resnetlog.jpg">
</div>

<a name="3"></a>

#### This is the output of the **vgg 16** using *stft* spect
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/vggstftconfusionmatrix.jpg">
</div>
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/vggstftROC.jpg">
</div>
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/vggstft.jpg">
</div>
<a name="4"></a>

#### This is the output of the **vgg 16** using *log stft* spect
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/vgglogconfusionmatrix.jpg">
</div>
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/vgglogROC.jpg">
</div>
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/vgglog.jpg">
</div>

**Note that** in the dataset (kaggle 2 dataset ), I will provide below, have the final models saved for each type of spectrogram (with the best wiegths)
<a name="instruction"></a>
## Instructions
to properly use the code

1. run the data preparation notebook , keep in mind downloding the dataset for each notebook or work directly in kaggle using the datasets that I will provide in the [kaggle dataset section](kdataset).
2. run the model either the classification using the stft spectrogram or the classification using the log stft spectrogram

##### Note that in the dataset (kaggle 2 dataset), provided in [kaggle dataset section](kdataset), have the final models for both the VGG 16 & ResNet 18 saved for each type of spectrogram

<a name="ref"></a>
## References
- Zhang, Q., Zhang, J., Yuan, J., Huang, H., Zhang, Y., Zhang, B., Lv, G., Lin, S., Wang, N., Liu, X., Tang, M., Wang, Y., Ma, H., Liu, L., Yuan, S., Zhou, H., Zhao, J., Li, Y., Yin, Y., … Lian, Y. (2022). SPRSound: Open-source SJTU Paediatric Respiratory Sound Database. IEEE Transactions on Biomedical Circuits and Systems, 16(5), 867–881. https://doi.org/10.1109/tbcas.2022.3204910
- Dataset link:   https://github.com/SJTU-YONGFU-RESEARCH-GRP/SPRSound
<a name="kdataset"></a>
## Kaggle Datasets
- For the data analysis and data preparation, the full dataset and related papers can be found here.[kaggle 1 dataset](https://www.kaggle.com/datasets/mayarelghandour/sprsound-nosplit/data)
- For the classification notebooks for both log and STFT, refer to this dataset. [kaggle 2 dataset](https://www.kaggle.com/datasets/mayarelghandour/spr-splitevents/data)
<a name="knote"></a>
## kaggle notebooks for further insight
1. [data analysis](https://www.kaggle.com/code/mayarelghandour/spr-data-analysis)
2. [signal data perparation](https://www.kaggle.com/code/mayarelghandour/signal-data-preparation)
3. [model notebooks](https://www.kaggle.com/code/mayarelghandour/final-models) **version 12** contain the ***log stft*** classification & **version 11** contain the ***stft*** classification
