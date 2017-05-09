
# COURSE PROJECT   
# Instructions

# The purpose of this project is to collect, work with, and clean a data set described on Readme.md

The following are done in the script:

1-Merges the training and the test sets to create one data set.
2- Extracts only the measurements on the mean and standard deviation for each measurement.
3- Uses descriptive activity names to name the activities in the data set
4- Appropriately labels the data set with descriptive variable names.
5- From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

To do so, the two data set, Train and Test are treated separetely. For "Test" data is done the following, 
Import the data set to the variables: 
  testx - is the data with 561 variables and thousands of observations. 
  testy - is a vector with de associates activity code for each observation.
  test_subj - store the subject or volunteer associated to each observation

Next, it is matched descriptive names to activity codes. 
The variable "testx" is redefined by removing all columns without characteres "mean" and "std" in the column header. 
The 03 variables are merged together to make a unique dataframe "ntestx"

This process is replicated to "Train" data and a dataframe "ntrainx" is also obtained. 

This two tidy data are joined and a dataframe "mydata". 

Finally, "mydata" is summarized in an independent and more tidy dataframe "ntidy". This last dataframe  shows the average of each variable grouped for each activity and each subject (volunteer).





