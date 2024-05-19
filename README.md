# ADHD-EEG-signal-classification
Our project is Binary EEG signal classification using 1D CNN deep learning model\
We are classifying our signal into control and ADHD\
## Table of content
### - Dataset
### - Data conversion
### - Data preprocessing
### - Data preparation and 1D CNN model
### - Confusion matrix
### - Metrics
### - ROC curve

### First: Dataset
- the dataset was aquired from [IEEEDataPort EEG data for ADHD / control children](https://ieee-dataport.org/open-access/eeg-data-adhd-control-children) \
- Participants were 61 children with ADHD and 60 healthy controls (boys and girls, ages 7-12).
- The ADHD children were diagnosed by an experienced psychiatrist to DSM-IV criteria, and have taken Ritalin for up to 6 months.
- None of the children in the control group had a history of psychiatric disorders, epilepsy, or any report of high-risk behaviors.
- EEG recording was performed based on 10-20 standard by 19 channels (Fz, Cz, Pz, C3, T3, C4, T4, Fp1, Fp2, F3, F4, F7, F8, P3, P4, T5, T6, O1, O2) at 128 Hz sampling frequency.
- Since one of the deficits in ADHD children is visual attention, the EEG recording protocol was based on visual attention tasks.







## Second: Data conversion
### Converting files
- The data files was in .mat format, we converted it to .fif to help us deal with it and saved it

## Third: Data preprocessing
- We used **MNE library** for reading, diplaying and preprocessing files
- We applied **high-pass** filter at frequency = 0.5 Hz
- Then, We applied **notch filter** at frequency = 50 Hz to remove power line frequency
- After that, We applied **zero padding** to all the files to avoid the loss of the data at the begining and end of record
- Then, We applied **moving average filter** with window = 5, the aim of it is to smooth out the signal a bit
- Then, We applied **common average reference filter** to remove artifacts related to noise present during the record
- At the end, We saved the filtered data in the files

## Fourth: Data preparation and 1D CNN model
### Data preparation
- we read the paths of the filtered data first
- we took 50 ADHD files and 60 control files to make the data balanced in both classes as the time of ADHD files were longer so it'll produce more epoches
- we created a function called read_data:
   - first it reads the files from the new directory
   - then, it divides single record into multiple equal epochs, epoch duration = 10 seconds with 75% overlap
   - then, it converts each epoch to numpy array using **epoch.get_data()**
- after applying this function to all the files in our directory, we put all the arrays in one big array
- then we created an array for labels
- the shape of data fed to the model was **1280x19**
### 1D CNN model
#### Model building:
- our CNN model consists of **15 layers**
- the model consisted:
   - 6 convolution 1D layers
   - 6 pooling layers(2 max pooling and 4 average pooling)
   - 7 LeakyReLU layers
   - 2 dropout layers
   - 3 dense layers
   - The output layer is a Dense layer with a single unit and sigmoid activation for binary classification
- **Optimizer used**: Adam optimizer
## Fifth: Confusion matrix
![Github logo](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)
