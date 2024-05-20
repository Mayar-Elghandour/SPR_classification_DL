# SPR_classification_DL
## Table of Contents
1. [Introduction](#intro)
2. [Dataset](#dataset)
     1. [Data source](#source)
     2. [Data structure](#structure)
     3. [Data ratio](#ratio)
3. [Results](#result)
   1. [ResNet 18 using STFT spectrogram](#1)
   2. [ResNet 18 using LOG STFT spectrogram](#2)
   3. [VGG 16 using STFT spectrogram](#3)
   4. [VGG 16 using LOG STFT spectrogram](#4)
4. [Instructions](#instruction)
5. [References](#ref)
6. [Kaggle Datasets](#kdataset)
7. [Kaggle Notebooks](#knote)


<a name="intro"></a>
## Introduction
This project focuses on the classification of breathing sounds at the event level using deep learning models (ResNet 18, VGG16). 

The main objective is to turn the diagnosis from a subjective perspective to an objective one. 

<a name="dataset"></a>
## Dataset
This dataset is unique as it has an age range between 0 and 16.2 years, unlike other open-source datasets that range from pediatrics to old age.
<a name="source"></a>
### Data source 
The dataset used is the[SPR Sound:  SJTU Paediatric Respiratory Sound Database](https://github.com/SJTU-YONGFU-RESEARCH-GRP/SPRSound)

 
<a name="structure"></a>
### Data structure
The data set consists of audio signal (.wav ) and labels in (.json )

Each signal is called ***record*** &
Each record contain multiple ***events***
In the .json file you will find the record and the event annotation.

The record annotation could be normal ,poor quality ,CAS, DAS, CAS&DAS which describe the label of the whole signal

The event annotation contain the start and end time of the event in record and the type of event which could be normal,Fine Crackle,Wheeze,Coarse-Crackle,Rhonchi,Wheeze+Crackle,Stridor

In case of poor quality the event annotation are empty
<a name="ratio"></a>
### The data ratio
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/images/dataratio.jpg">
</div>
This plots the data on event level

- 0 is normal
- 1 is abnormal (includes Fine Crackle,Wheeze,Coarse-Crackle,Rhonchi,Wheeze+Crackle,Stridor)
- 2 is poor quality
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

**Note that** in the dataset (kaggle 2 dadtaset ), I will provide below, have the final models saved for each type of spectrogram (with the best wiegths)
<a name="instruction"></a>
## Instructions
- the data analysis is only for gainig knowledge about the dataset
- to run the code first run the data preparation notebook , keep in mind downloding the dataset for each notebook or work directly in kaggle using the datasets i will provide in the kaggle dataset section,then run the model either the classification using the stft spectrogram or the classification using the log stft spectrogram

### Note that in the dataset (kaggle 2 dadtaset ), I will provide in refrences, have the final models saved for each type of spectrogram

<a name="ref"></a>
## References
Zhang, Q., Zhang, J., Yuan, J., Huang, H., Zhang, Y., Zhang, B., Lv, G., Lin, S., Wang, N., Liu, X., Tang, M., Wang, Y., Ma, H., Liu, L., Yuan, S., Zhou, H., Zhao, J., Li, Y., Yin, Y., … Lian, Y. (2022). SPRSound: Open-source SJTU Paediatric Respiratory Sound Database. IEEE Transactions on Biomedical Circuits and Systems, 16(5), 867–881. https://doi.org/10.1109/tbcas.2022.3204910  
<a name="kdataset"></a>
## Kaggle Datasets
- For the data analysis and data preparation, the full dataset and related papers can be found here.[kaggle 1 dataset](https://www.kaggle.com/datasets/mayarelghandour/sprsound-nosplit/data)
- For the classification notebooks for both log and STFT, refer to this dataset. [kaggle 2 dataset](https://www.kaggle.com/datasets/mayarelghandour/spr-splitevents/data)
<a name="knote"></a>
## kaggle notebooks for further insight
1. [data analysis](https://www.kaggle.com/code/mayarelghandour/spr-data-analysis)
2. [signal data perparation](https://www.kaggle.com/code/mayarelghandour/signal-data-preparation)
3. [model notebooks](https://www.kaggle.com/code/mayarelghandour/final-models) version 12 contain the log stft classification &version 11 contain the stft classification
