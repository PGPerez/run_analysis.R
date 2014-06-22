run_analysis.R
==============

Getting and Cleaning Data Course Project

## Course Project - Getting and Cleaning Data
##
## Reading Data into R
##
setwd("C:/Users/pgper_000/Desktop/Coursera R Class/Getting and Cleaning Data/UCI HAR Dataset/test")
Testdata <- read.table("X_test.txt")
Testlabels <-read.table("y_test.txt")
SubjectTest <- read.table("subject_test.txt")
setwd("C:/Users/pgper_000/Desktop/Coursera R Class/Getting and Cleaning Data/UCI HAR Dataset/train")
Traindata <- read.table("X_train.txt")
Trainlabels <-read.table("y_train.txt")
SubjectTrain <- read.table("subject_train.txt")
setwd("C:/Users/pgper_000/Desktop/Coursera R Class/Getting and Cleaning Data/UCI HAR Dataset")
featuresnames <- read.table("features.txt")
activitylabels <- read.table("activity_labels.txt")
##
## add feature label names to each data set (i.e. Testdata and Traindata)
##
names(Testdata) <- featuresnames[,2]
names(Traindata) <- featuresnames[,2]
##
## add "Subject_id" label to SubjectTest and SubjecTrain
##
names(SubjectTest) <- "Subject_id"
names(SubjectTrain) <-"Subject_id"
##
## add "Activity_id" label to Testlabels and Trainlabels and activity labels
##
names(Testlabels) <- "Activity_id"
names(Trainlabels) <- "Activity_id"
names(activitylabels) <-c("Activity_id","Activity")
##
## using the Cbind function ADD "Subject ID" and "Activity ID" COLUMNS to Testdata and Traindata
##
Testdata <- cbind(SubjectTest,Testlabels,Testdata)
Traindata <-cbind(SubjectTrain,Trainlabels,Traindata)
## 
## combine the training and test data sets
##
dataset <- rbind(Testdata,Traindata)
##
## merge activity levels
##
dataset <- merge(dataset,activitylabels, by.x="Activity_id",all=TRUE)
##
## Create "1st Tidy Data by "extract mean and standard deviation 
##
mean_std_index <-c(grep("mean()",names(dataset)),grep("std()",names(dataset)))
labels <- names(dataset)
mean_std_labels <- labels[mean_std_index]
mean_std_labels <- c("Subject_id","Activity_id","Activity",mean_std_labels)
Tidy_Data_1 <-dataset[,mean_std_labels]
##
## Examine Tidy Data 1 using head and str functions
##
head(Tidy_Data_1)
str(Tidy_Data_1)
## 
## Creating Tidy Data 2
##
mean_std_index <-c(grep("mean()",names(dataset)))
labels <- names(dataset)
mean_std_labels <- labels[mean_std_index]
mean_std_labels <- c("Subject_id","Activity_id","Activity",mean_std_labels)
Tidy_Data_2 <-dataset[,mean_std_labels]
##
## Examine Tidy Data 2 using head and str functions
##
head(Tidy_Data_2)
str(Tidy_Data_2)
## 
setwd("C:/Users/pgper_000/Desktop/Coursera R Class/Getting and Cleaning Data/UCI HAR Dataset")
write.csv(Tidy_Data_1, file="TidyData1.csv")
write.csv(Tidy_Data_2, file="TidyData2.csv")

