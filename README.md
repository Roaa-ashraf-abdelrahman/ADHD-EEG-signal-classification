# ADHD-EEG-signal-classification
Our project is Binary EEG signal classification using 1-D CNN deep learning model\
We are classifying our signal into control and ADHD\
the dataset was aquired from [IEEEDataPort EEG data for ADHD / control children](https://ieee-dataport.org/open-access/eeg-data-adhd-control-children) \

## First: converting and preprocessing
### Converting files
- The data files was in .mat format, we converted it to .fif to help us deal with it and saved it
### Preprocessing
- We used MNE library for reading, diplaying and preprocessing files
- We applied high-pass filter at frequency = 0.5 Hz
- Then, We applied notch filter at frequency = 50 Hz to remove power line frequency
- After that, We applied zero padding to all the files to avoid the loss of the data at the begining and end of record
- Then, We applied moving average filter with window = 5, the aim of it is to smooth out the signal a bit
- Then, We applied common average reference filter to remove artifacts related to noise present during the record
- At the end, We saved the filtered data in the files
## Second: Data preparation and 1-D CNN model
### Data preparation
- we read the paths of the filtered data first
- we created a function called read_data:
   - first it reads the files from the new directory
   - then, it divides single record into multiple equal epochs, epoch duration = 10 seconds with 75% overlap
   - then, it converts each epoch to numpy array using epoch.get_data()
