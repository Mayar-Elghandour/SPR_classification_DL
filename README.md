# SPR_classification_DL
##classification of breathing sounds on event level using deep learning models (ResNet 18, VGG16) from the dataset SPR Sound:  SJTU Paediatric Respiratory Sound Database 
The main reason behind such classification model is to turn the diagnosis from a subjective prespective to an objective one 

this dataset is special due to having the age range between 0 and 16.2 years compared to other open source data set that ranges from pediatrics to old age 


The data set consists of audio signal (.wav format ) and labels in (.json )
Each signal is called *record*
Each record contain multiple *events*
In the .json file you will find the record and the event annotation 
The record annotation could be normal ,poor quality ,CAS, DAS, CAS&DAS which describe the whole signal label 
the event annotation contain the start and end time of the event in record and the type of event which could be normal,Fine Crackle,Wheeze,Coarse-Crackle,Rhonchi,Wheeze+Crackle,Stridor

In case of poor quality the event annotation are empty

**In data analysis notebook**
we read the json file and get the data in it and place it in the dataframe for easier manipulation
We find the ratio of the data  normal to abnormal to poor quality 

**In data perparation** 
We split the signal records into events and apply a band pass filter and balancing the data by removing the files with exteremly large time (outlier) and then randomly remove from the normal events to make it reach the same size of abnormal data

**In the classification notebooks** they contain the same code but the difference in the spectrogram used in the class ***mydataset*** and the log spectrogram with vgg16 produced the highest area under the ROC curve

I have uploaded the dataset on kaggle:
for the data analysis and data perparation it has the full dataset and contain the papers [kaggle dataset](https://www.kaggle.com/datasets/mayarelghandour/sprsound-nosplit/data)
for the classification notbooks for both log, stft  [kaggle dataset](https://www.kaggle.com/datasets/mayarelghandour/spr-splitevents/data)
