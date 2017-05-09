####################### Getting and Cleaning Data Course Project #########################

#The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. The goal is to prepare tidy data that can be used for later analysis. You will be graded by your peers on a series of yes/no questions related to the project. You will be required to submit: 1) a tidy data set as described below, 2) a link to a Github repository with your script for performing the analysis, and 3) a code book that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md. You should also include a README.md in the repo with your scripts. This repo explains how all of the scripts work and how they are connected.

#One of the most exciting areas in all of data science right now is wearable computing - see for example this article . Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained:
  
#  http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

#Here are the data for the project:
  
 # https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

# You should create one R script called run_analysis.R that does the following.

# 1-Merges the training and the test sets to create one data set.
# 2- Extracts only the measurements on the mean and standard deviation for each measurement.
# 3- Uses descriptive activity names to name the activities in the data set
# 4- Appropriately labels the data set with descriptive variable names.
# 5- From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

#-----------------------------------------------------------------------------------------------------------

rm(list = ls()) 


setwd("/home/madoro/Desktop/datascience/3.cleaning_data/course_project/")


library(data.table)  # allow fread function
library(dplyr)       # allow usefull tbl/dataframe functions
library(plyr)        #  allow revalue function

###### TEST DATA  ######################
# Reading files - test data
features_name<-fread("./UCI_HAR_Dataset/features.txt") # store the features names
features_name[[c(2)]]<-gsub("[^A-Za-z0-9]","", features_name[[c(2)]]) #supress all special characters for name columns

testx<-fread("./UCI_HAR_Dataset/test/X_test.txt", col.names = features_name[[c(2)]])  # store the data - features values with headers
testy<-fread("./UCI_HAR_Dataset/test/y_test.txt", col.names = "activity_code")
test_subj<-fread("./UCI_HAR_Dataset/test/subject_test.txt")



aux <- as.matrix(testy) # convert testy to a matrix to allow  convert each integer to character
aux <- as.character(aux) # turn into a vector of characters 

###### Assign descriptive names to activity codes
testy$activity <- revalue(aux,
                             c("1"="WALKING","2"="WALKING_UPSTAIRS", "3"="WALKING_DOWNSTAIRS", 
                               "4"="SITTING", "5"="STANDING","6"="LAYING"))


mean_std_col<-grep("[Mm]ean|MEAN|STD|[Ss]td",features_name[[c(2)]]) # identify all column headers with characters "mean" and "std"
testx<-(testx[, mean_std_col,with=FALSE]) # subset columns with characteres "mean" and "std" in the column header


ntestx<-cbind(test_subj,testy$activity,testx)  # joint volunteer and activity column to dataframe

colnames(ntestx)[1] <- "Volunteer"  #rename the column name with descriptive name
colnames(ntestx)[2] <- "Activity"   #rename the column name with descriptive name




############## TRAIN DATA  ######################
# Reading files - TRAINdata
features_name<-fread("./UCI_HAR_Dataset/features.txt") # store the features names
features_name[[c(2)]]<-gsub("[^A-Za-z0-9]","", features_name[[c(2)]]) #supress all special characters for name columns

trainx<-fread("./UCI_HAR_Dataset/train/X_train.txt", col.names = features_name[[c(2)]])  # store the data - features values with headers
trainy<-fread("./UCI_HAR_Dataset/train/y_train.txt", col.names = "activity_code")  # Store the correspondent activity
train_subj<-fread("./UCI_HAR_Dataset/train/subject_train.txt")  # record the volunteer nr

aux <- as.matrix(trainy) # convert testy to a matrix to allow  convert each integer to character
aux <- as.character(aux) # turn into a vector of characters 

###### Assign descriptive names to activity codes
trainy$activity <- revalue(aux,
                 c("1"="WALKING","2"="WALKING_UPSTAIRS", "3"="WALKING_DOWNSTAIRS", 
                   "4"="SITTING", "5"="STANDING","6"="LAYING"))


mean_std_col<-grep("[Mm]ean|MEAN|STD|[Ss]td",features_name[[c(2)]]) # identify all column headers with characters "mean" and "std"
trainx<-(trainx[, mean_std_col,with=FALSE]) # subset columns with characteres "mean" and "std" in the column header


ntrainx<-cbind(train_subj,trainy$activity,trainx)  # joint volunteer and activity column to data

colnames(ntrainx)[1] <- "Volunteer"  #rename the column name with descriptive name
colnames(ntrainx)[2] <- "Activity"   #rename the column name with descriptive name

##########################  MERGE TRAIN AND TEST DATA #####################

mydata<-rbind(ntrainx,ntestx)  # merge train and test data


###############################  NEW TIDY DATA ##########################################
#install.packages("detach_package")
pkg <- "package:plyr"
detach(pkg, character.only = TRUE)  # unload "plyr" due to conflicting packages issue with "dplyr"
# was having problems with dplyr functions

mydata<-tbl_df(mydata) # transform dataframe in a table dataframe

ntidy<-mydata %>% group_by(Volunteer, Activity) %>% summarise_each(funs(mean))
# summarize average of each variable for each activity and each subject (volunteer).

write.table(ntidy, file = "tidyswet.txt", col.names = FALSE)  # write the tidy data to a file.txt

