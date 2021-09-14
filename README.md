# Injury Prognosis in NCAA Runners Using Wearable Accelerometer Data: Project Overview
Exploring wearable accelerometer data from NCAA runners to prognose musculokskeletal overuse injury. Part of my research efforts at the [Human Performance Lab](http://hpl.ucdavis.edu/) at University of California, Davis.

Highlights: 
* Used accelerometer data collected from UC Davis NCAA runners by the Human Performance Lab. Dataset contained triaxial accelerometer data collected at 50Hz. 
* Assessed signal quality using Fast Fourier Transform and filtered out noise using Butterworth filter with 10Hz cutoff. 
* Selected 1 training session to be categorized as "healthy" runner data, and 1 training session for "injured" data as the subject approached a permanent injury during data collection period.
* Prototyped Long Short-Term Memory (LSTM) model which classified between accelerometer signals from healthy and injured periods with average accuracy of 97%. 

# Code and Resources Used
**Python Version:** 3.7
**Packages:** pandas, numpy, scipy, scikit-learn, keras, matplotlib, tensorflow

# Data Collection and Subject Profile
* Data was collected from 10 NCAA runners at UC Davis using a wearable triaxial accelerometer mounted at the sacrum. 
* Sampling rate: 50Hz. 
* For this prototype, only data from Subject 1 was utilized to eliminate natural gait variations between subjects. 

**Important Note:** Subject 1 was permanently injured after the 29th training session. Thus, training session 29 is taken to be the subject's "injured" state, while training session 1 is the subject's "healthy" state. 

# Data Cleaning and Preprocessing 
The large magnitude and rawness of the dataset made preprocessing steps necessary. The first step I took was to plot the Fast Fourier Transform of the data to gauage signal quality. Below is a sample of a FFT plot from one of the 29 training sessions. 

**Insert Old Plot here** 

From the literature, we know that traditional running frequency is at 2-3Hz as well as some higher frequencies for the anterior-posterior and medial-lateral axes. Thus, I chose to filter out signal >10Hz as this was likely noise from electrical systems and the data collection environment. The resulting plot looked like this: 

**Insert New Plot Here** 

It is important to note that the nature of this model type makes it possible to be conservative with the cutoff frequency. As outlined in following steps, we will not explicitly be using the signal peaks or features to engineer features for classification. Therefore, it serves us well to keep as much of the signal as possible while eliminating as much noise as possible. 

Lastly, here are some additional processing steps that were taken: 
* Removed Resultant and Time columns from dataset. 
* Segmented data from both training sessions into 2s time intervals with 1s overlap. 
* Stacked all segmented data into a 3D data matrix. i.e., the triaxial data from both the "healthy" and "injured" training sessions were converged into one data matrix.

# Model Construction
A Long Short-Term Memory (LSTM) model type was utilized. LSTM models excel in Natural Language Processing, and thus, have the capability to 
