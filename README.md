# SPR_classification_DL

## Introduction
This project focuses on the classification of breathing sounds at the event level using deep learning models (ResNet 18, VGG16). The main objective is to turn the diagnosis from a subjective perspective to an objective one. 

## Dataset
The dataset used is the[SPR Sound:  SJTU Paediatric Respiratory Sound Database](https://github.com/SJTU-YONGFU-RESEARCH-GRP/SPRSound) This dataset is unique as it has an age range between 0 and 16.2 years, unlike other open-source datasets that range from pediatrics to old age. 

The data set consists of audio signal (.wav format ) and labels in (.json )
Each signal is called *record*
Each record contain multiple *events*
In the .json file you will find the record and the event annotation 
The record annotation could be normal ,poor quality ,CAS, DAS, CAS&DAS which describe the whole signal label 
the event annotation contain the start and end time of the event in record and the type of event which could be normal,Fine Crackle,Wheeze,Coarse-Crackle,Rhonchi,Wheeze+Crackle,Stridor

In case of poor quality the event annotation are empty

## Results
this the output of the vgg 16 using log spect
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/confusion.png?raw=true">
</div>
<div>
  <img src="https://github.com/Mayar-Elghandour/SPR_classification_DL/blob/main/roc.png?raw=true">
</div>

## Instructions
the data analysis is only for knowledge about the dataset
to run the code first run the data preparation then run the model either classification using the stft spectrogram or classification using the log stft spectrogram
in the dataset (kaggle 1) I will provide in refrences have the final models saved for all types


## References
Zhang, Q., Zhang, J., Yuan, J., Huang, H., Zhang, Y., Zhang, B., Lv, G., Lin, S., Wang, N., Liu, X., Tang, M., Wang, Y., Ma, H., Liu, L., Yuan, S., Zhou, H., Zhao, J., Li, Y., Yin, Y., … Lian, Y. (2022). SPRSound: Open-source SJTU Paediatric Respiratory Sound Database. IEEE Transactions on Biomedical Circuits and Systems, 16(5), 867–881. https://doi.org/10.1109/tbcas.2022.3204910  

## Kaggle Datasets
- For the data analysis and data preparation, the full dataset and related papers can be found here.
- For the classification notebooks for both log and STFT, refer to this dataset.
