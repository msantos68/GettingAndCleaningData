###Code Book for Coursera Course Getting and Cleaning Data Course Project
##3/21/2015

##Study Design:
You can find details about the Study at this website: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

This study looked at using the data from a Samsung Galaxy S II phone with it's built in GPS accelerometer and gyroscope to understand the movement of Subject
with Different Activity Levels.
The study used 30 different subjects and 6 different activities (Walking, Walking Upstairs, Walking Downstairs, Sitting, Standing, and Laying).
The data was partitioned into 2 groups (test and train) with 70% of subjects in train and 30% in test.

A video of how this was conducted can be viewed from the website provided above.

##Raw Data Information:
The Raw Data used for this analysis comes from the study above and is already processed for us.  Here we will be using the following files as the Raw Data:
- X_test.txt
- X_train.txt
Both of which are found under the zipped folder: http://archive.ics.uci.edu/ml/machine-learning-databases/00240/
The following information about the features can be found under features_info.txt in the same zipped folder above:

Feature Selection 
=================

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

tBodyAcc-XYZ
tGravityAcc-XYZ
tBodyAccJerk-XYZ
tBodyGyro-XYZ
tBodyGyroJerk-XYZ
tBodyAccMag
tGravityAccMag
tBodyAccJerkMag
tBodyGyroMag
tBodyGyroJerkMag
fBodyAcc-XYZ
fBodyAccJerk-XYZ
fBodyGyro-XYZ
fBodyAccMag
fBodyAccJerkMag
fBodyGyroMag
fBodyGyroJerkMag

The set of variables that were estimated from these signals are: 

mean(): Mean value
std(): Standard deviation
mad(): Median absolute deviation 
max(): Largest value in array
min(): Smallest value in array
sma(): Signal magnitude area
energy(): Energy measure. Sum of the squares divided by the number of values. 
iqr(): Interquartile range 
entropy(): Signal entropy
arCoeff(): Autorregresion coefficients with Burg order equal to 4
correlation(): correlation coefficient between two signals
maxInds(): index of the frequency component with largest magnitude
meanFreq(): Weighted average of the frequency components to obtain a mean frequency
skewness(): skewness of the frequency domain signal 
kurtosis(): kurtosis of the frequency domain signal 
bandsEnergy(): Energy of a frequency interval within the 64 bins of the FFT of each window.
angle(): Angle between to vectors.

Additional vectors obtained by averaging the signals in a signal window sample. These are used on the angle() variable:

gravityMean
tBodyAccMean
tBodyAccJerkMean
tBodyGyroMean
tBodyGyroJerkMean

The complete list of variables of each feature vector is available in 'features.txt'

##Processing Data
For this analysis, we were only concerned with the mean and std measurements from X_test.txt and X_train.txt

Our first task was to read in all the data and process.  We used the features.txt file to create a vector of names to use as the column names for a more
descriptive naming convention. 
We removed the "()-" from all the names and replaced with "."
Then we replaced the "()" with "."
Lastly we converted the "mean" and "std" to all UPCASE so that they are easier to understand.
The vector created is called feature_names.

Second we processed the X_test data
Read in the X_Test data and set the names to that from the feature_names vector processed above.
We selected only the columns with mean or std in the name and created a column called file = "test".  This way if we every want to go back to exactly which 
subset the row came from we could.

Next for the second step we used the Activity_Label to be able determine which activity the subject was doing.  THis was done by merging the Activity_Label data with teh y__test data.
THe merge was done by Activity_Num (The activity ID that was given to each row of the data).
We read in the subject_test file which contains the SubjectID for each row in the X_test file.
The SubjectID is the Subject # for the volunteer whose data is on the row.
We then CBIND the subject_test data with y_test and x_test.

The new dataset contains the following columns:
All columns, except SubjectID, Activity_Label, and file can be found in the features_info.txt referenced above.
Since these columns have been normalized for us, there is no units.
SubjectID = Subject # for the volunteer whose data is on the row.
Activity_Label = Activity for which the subject was doing on the row.
File = Test which references which original file the data came from.

 [1] "SubjectID"                            "Activity_Label"                      
 [3] "tBodyAcc.MEAN..X"                     "tBodyAcc.MEAN..Y"                    
 [5] "tBodyAcc.MEAN..Z"                     "tGravityAcc.MEAN..X"                 
 [7] "tGravityAcc.MEAN..Y"                  "tGravityAcc.MEAN..Z"                 
 [9] "tBodyAccJerk.MEAN..X"                 "tBodyAccJerk.MEAN..Y"                
[11] "tBodyAccJerk.MEAN..Z"                 "tBodyGyro.MEAN..X"                   
[13] "tBodyGyro.MEAN..Y"                    "tBodyGyro.MEAN..Z"                   
[15] "tBodyGyroJerk.MEAN..X"                "tBodyGyroJerk.MEAN..Y"               
[17] "tBodyGyroJerk.MEAN..Z"                "tBodyAccMag.MEAN."                   
[19] "tGravityAccMag.MEAN."                 "tBodyAccJerkMag.MEAN."               
[21] "tBodyGyroMag.MEAN."                   "tBodyGyroJerkMag.MEAN."              
[23] "fBodyAcc.MEAN..X"                     "fBodyAcc.MEAN..Y"                    
[25] "fBodyAcc.MEAN..Z"                     "fBodyAcc.MEANFreq..X"                
[27] "fBodyAcc.MEANFreq..Y"                 "fBodyAcc.MEANFreq..Z"                
[29] "fBodyAccJerk.MEAN..X"                 "fBodyAccJerk.MEAN..Y"                
[31] "fBodyAccJerk.MEAN..Z"                 "fBodyAccJerk.MEANFreq..X"            
[33] "fBodyAccJerk.MEANFreq..Y"             "fBodyAccJerk.MEANFreq..Z"            
[35] "fBodyGyro.MEAN..X"                    "fBodyGyro.MEAN..Y"                   
[37] "fBodyGyro.MEAN..Z"                    "fBodyGyro.MEANFreq..X"               
[39] "fBodyGyro.MEANFreq..Y"                "fBodyGyro.MEANFreq..Z"               
[41] "fBodyAccMag.MEAN."                    "fBodyAccMag.MEANFreq."               
[43] "fBodyBodyAccJerkMag.MEAN."            "fBodyBodyAccJerkMag.MEANFreq."       
[45] "fBodyBodyGyroMag.MEAN."               "fBodyBodyGyroMag.MEANFreq."          
[47] "fBodyBodyGyroJerkMag.MEAN."           "fBodyBodyGyroJerkMag.MEANFreq."      
[49] "angle.tBodyAccMEAN.gravity."          "angle.tBodyAccJerkMEAN.gravityMEAN." 
[51] "angle.tBodyGyroMEAN.gravityMEAN."     "angle.tBodyGyroJerkMEAN.gravityMEAN."
[53] "angle.X.gravityMEAN."                 "angle.Y.gravityMEAN."                
[55] "angle.Z.gravityMEAN."                 "tBodyAcc.STD..X"                     
[57] "tBodyAcc.STD..Y"                      "tBodyAcc.STD..Z"                     
[59] "tGravityAcc.STD..X"                   "tGravityAcc.STD..Y"                  
[61] "tGravityAcc.STD..Z"                   "tBodyAccJerk.STD..X"                 
[63] "tBodyAccJerk.STD..Y"                  "tBodyAccJerk.STD..Z"                 
[65] "tBodyGyro.STD..X"                     "tBodyGyro.STD..Y"                    
[67] "tBodyGyro.STD..Z"                     "tBodyGyroJerk.STD..X"                
[69] "tBodyGyroJerk.STD..Y"                 "tBodyGyroJerk.STD..Z"                
[71] "tBodyAccMag.STD."                     "tGravityAccMag.STD."                 
[73] "tBodyAccJerkMag.STD."                 "tBodyGyroMag.STD."                   
[75] "tBodyGyroJerkMag.STD."                "fBodyAcc.STD..X"                     
[77] "fBodyAcc.STD..Y"                      "fBodyAcc.STD..Z"                     
[79] "fBodyAccJerk.STD..X"                  "fBodyAccJerk.STD..Y"                 
[81] "fBodyAccJerk.STD..Z"                  "fBodyGyro.STD..X"                    
[83] "fBodyGyro.STD..Y"                     "fBodyGyro.STD..Z"                    
[85] "fBodyAccMag.STD."                     "fBodyBodyAccJerkMag.STD."            
[87] "fBodyBodyGyroMag.STD."                "fBodyBodyGyroJerkMag.STD."           
[89] "file"

Third step was to repeat Step 2 for the Train data.
The train data has the same columns as the test data above.
The only exception is that file = Train instead of file = Test since this is the Train data.

Fourth Step was to merge the Test and Train data together
This step used RBIND since both files contained the same columns and was just need to be combined together.

The final result of this data is called: master_data

Fifth Step - create a tidy data which has the average mean and std values over the SubjectID and Activity_Label
It should be noted that the column names are the same as in the master_data.
However, columns now represent the AVERAGE value for the column over the SubjectID and Activity_Label.
This part was completed by using melt function to create ID and Measurement variables
Then using the dcast function created the mean of all the Measurement variables by SubjectID and Activity_Label
The final dataset is called: tidy_avg

And output of this data to txt flat file is done to your working directory: Final_Tidy_Data.txt