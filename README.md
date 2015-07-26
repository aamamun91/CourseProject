# CourseProject
Step1: Set the directory 
setwd("C:/Users/aalmamun/Desktop/Datasciencecoursera/CourseProject")

Step 2: Read the url
fileurl<- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"

Step 3: Download the zipped file and unzip
course<- download.file(fileurl, destfile="C:/Users/aalmamun/Desktop/Datasciencecoursera/CourseProject/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip", mode="wb")
unzip("getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip")

Step 4: Preparing Test Dataset
##Reading Subject set from Test data set##
Stest<- read.table("C:/Users/aalmamun/Desktop/Datasciencecoursera/CourseProject/UCI HAR Dataset/test/sUbject_test.txt", header=FALSE, sep="", dec=".")
##Naming of the variable Subject in test dataset###
names(Stest)[1]<- "sub.test"
##Indexing the subject set in Test data##
Stest$x<- c(1:2947)
##Reading activity set from Test data##
Ytest<- read.table("C:/Users/aalmamun/Desktop/Philippines/Datasciencecoursera/CourseProject/UCI HAR Dataset/test/y_test.txt", header=FALSE, sep="", dec=".")
##Naming activity variable in test data##
names(Ytest)[1]<- "act.test"
##Indexing activity data##
Ytest$x<- c(1:2947)
##Merging Subject and Activity data##
test<- merge(Stest, Ytest, all=TRUE)
##Reading Test data that have measurements on 561 variables##
xtest<- read.table("C:/Users/aalmamun/Desktop/Datasciencecoursera/CourseProject/UCI HAR Dataset/test/X_test.txt", header=FALSE, sep="", dec=".")
##Indexing the Test data##
xtest$x<- c(1:2947)
##Merging Subject, Activity and the Variables related to measurements in Test Data##
test<- merge(test, xtest, all=TRUE)

Step 5: Preparing Training Dataset
###Preparing Training Data Set####
##Reading Subject set from train data set##
Strain<- read.table("C:/Users/aalmamun/Desktop/Datasciencecoursera/CourseProject/UCI HAR Dataset/train/sUbject_train.txt", header=FALSE, sep="", dec=".")
##Naming of the variable Subject in training dataset###
names(Strain)[1]<- "sub.train"
##Indexing the subject set in Training data##
Strain$y<- c(2948:10299)
##Reading activity set from training data##
Ytrain<- read.table("C:/Users/aalmamun/Desktop/Datasciencecoursera/CourseProject/UCI HAR Dataset/train/y_train.txt", header=FALSE, sep="", dec=".")
names(Ytrain)[1]<- "act.train"
##Indexing activity data##
Ytrain$y<- c(2948:10299)
##Merging Subject and Activity data##
train<- merge(Strain, Ytrain, all=TRUE)
##Reading Training data that have measurements on 561 variables##
xtrain<- read.table("C:/Users/aalmamun/Desktop/Datasciencecoursera/CourseProject/UCI HAR Dataset/train/X_train.txt", header=FALSE, sep="", dec=".")
##Indexing the Training data##
xtrain$y<- c(2948:10299)
train<- merge(train, xtrain, all=TRUE)

Step 6: Labeling the activities in the merged dataset
testrain$act <- factor(testrain$act, levels = c(1,2,3,4,5,6), labels = c("WALKING", "WALKING_UPSTAIRS", "WALKING_DOWNSTAIRS", "SITTING", "STANDING", "LAYING"))

Step 7: Merging Test and Training dataset
##Naming the ID Variables in both test and training data##
names(train)[1]<- "id"
names(test)[1]<- "id"
names(test)[2]<- "sub"
names(test)[3]<- "act"
names(train)[2]<- "sub"
names(train)[3]<- "act"
testrain<- merge(test, train, all=TRUE)

Step 8: Extracting only the measurements on the mean and standard deviation for each measurement
##Reading the variable list from the source data##
varlist<- read.table("C:/Users/aalmamun/Desktop/Datasciencecoursera/CourseProject/UCI HAR Dataset/features.txt", header=FALSE, sep="", dec=".")
varlist
##Keeping the variables related to ID, mean and standard deviation##
myvar<- c("id","sub", "act", "V1", "V2", "V3",  "V4", "V5",	"V6",	"V41", "V42", "V43", "V44", "V45", 
          "V46", "V81", "V82", "V83", "V84", "V85", "V86", "V121", "V122", "V123", "V124", "V125", "V126", 
          "V161", "V162", "V163", "V164", "V165", "V166", "V201", "V202", "V214", "V215", "V227", "V228", "V240", "V241", "V253", "V254", 
          "V266", "V267", "V268", "V269", "V270", "V271", "V345", "V346", "V347", "V348", "V349", "V350", "V424", "V425", "V426", "V427", "V428", "V429", 
          "V503", "V504", "V516", "V517", "V529", "V530", "V542", "V543", "V556", "V557", "V558", "V559", "V560", "V561")
testrain<- testrain[myvar]

Step 9: Describing the variable names in the merged data
testrain$act <- factor(testrain$act, levels = c(1,2,3,4,5,6), labels = c("WALKING", "WALKING_UPSTAIRS", "WALKING_DOWNSTAIRS", "SITTING", "STANDING", "LAYING"))
names(testrain)[c(1:75)]<- c("ID", "Subject",  "Activity" , "tBodyAcc.mean.X",	"tBodyAcc.mean.Y", "tBodyAcc.mean.Z", "tBodyAcc.std.X",	"tBodyAcc.std.Y",	"tBodyAcc.std.Z", 
                             "tGravityAcc.mean.X" ,	"tGravityAcc.mean.Y" ,	"tGravityAcc.mean.Z",	"tGravityAcc.std.X",	"tGravityAcc.std.Y", "tGravityAcc.std.Z",	"tBodyAccJerk.mean.X",	"tBodyAccJerk.mean.Y",	
                             "tBodyAccJerk.mean.Z",	"tBodyAccJerk.std.X",	"tBodyAccJerk.std.Y",	"tBodyAccJerk.std.Z",	"tBodyGyro.mean.X",	"tBodyGyro.mean.Y",	"tBodyGyro.mean.Z",	"tBodyGyro.std.X",	
                             "tBodyGyro.std.Y",	"tBodyGyro.std.Z",	"tBodyGyroJerk.mean.X",	"tBodyGyroJerk.mean.Y",	"tBodyGyroJerk.mean.Z",	"tBodyGyroJerk.std.X",	"tBodyGyroJerk.std.Y",	"tBodyGyroJerk.std.Z",	
                             "tBodyAccMag.mean",	"tBodyAccMag.std",	"tGravityAccMag.mean",	"tGravityAccMag.std",	"tBodyAccJerkMag.mean",	"tBodyAccJerkMag.std",	"tBodyGyroMag.mean",	
                             "tBodyGyroMag.std",	"tBodyGyroJerkMag.mean",	"tBodyGyroJerkMag.std",	"fBodyAcc.mean.X",	"fBodyAcc.mean.Y",	"fBodyAcc.mean.Z",	"fBodyAcc.std.X",	"fBodyAcc.std.Y",	"fBodyAcc.std.Z",	
                             "fBodyAccJerk.mean.X",	"fBodyAccJerk.mean.Y",	"fBodyAccJerk.mean.Z",	"fBodyAccJerk.std.X",	"fBodyAccJerk.std.Y",	"fBodyAccJerk.std.Z",	"fBodyGyro.mean.X",	"fBodyGyro.mean.Y",	"fBodyGyro.mean.Z",	
                             "fBodyGyro.std.X",	"fBodyGyro.std.Y" ,	"fBodyGyro.std.Z",	"fBodyAccMag.mean",	"fBodyAccMag.std",	"fBodAccJerkMag.mean",	"fBodAccJerkMag.std",	"fBodGyroMag.mean",	"fBodGyroMag.std",	"fBodGyroJerkMag.mean",	
                             "fBodGyroJerkMag.std",	"ang.tBodyAccJerk.gravMean",	"ang.tBodGyro.gravMean",	"ang.tBodGyroJerk.gravMean",	"ang.X.gravityMean" ,	"ang.Y.gravMean" ,	"ang.Z.gravMean")

Step 10: Reshaping Data to create tidy dataset
install.packages("reshape2")
library(reshape2)
testrainMelt<- melt(testrain, id=c("ID", "Subject", "Activity"), measure.vars=c("tBodyAcc.mean.X",    "tBodyAcc.mean.Y", "tBodyAcc.mean.Z", "tBodyAcc.std.X",  "tBodyAcc.std.Y",	"tBodyAcc.std.Z", "tGravityAcc.mean.X" ,	
                      "tGravityAcc.mean.Y" ,	"tGravityAcc.mean.Z",	"tGravityAcc.std.X",	"tGravityAcc.std.Y", "tGravityAcc.std.Z",	"tBodyAccJerk.mean.X",	"tBodyAccJerk.mean.Y", "tBodyAccJerk.mean.Z",	"tBodyAccJerk.std.X",	
                      "tBodyAccJerk.std.Y",	"tBodyAccJerk.std.Z",	"tBodyGyro.mean.X",	"tBodyGyro.mean.Y",	"tBodyGyro.mean.Z",	"tBodyGyro.std.X", "tBodyGyro.std.Y",	"tBodyGyro.std.Z",	"tBodyGyroJerk.mean.X",	"tBodyGyroJerk.mean.Y",	
                      "tBodyGyroJerk.mean.Z",	"tBodyGyroJerk.std.X",	"tBodyGyroJerk.std.Y",	"tBodyGyroJerk.std.Z", "tBodyAccMag.mean",	"tBodyAccMag.std",	"tGravityAccMag.mean",	"tGravityAccMag.std",	"tBodyAccJerkMag.mean",	
                      "tBodyAccJerkMag.std",	"tBodyGyroMag.mean",	"tBodyGyroMag.std",	"tBodyGyroJerkMag.mean",	"tBodyGyroJerkMag.std",	"fBodyAcc.mean.X",	"fBodyAcc.mean.Y",	"fBodyAcc.mean.Z",	"fBodyAcc.std.X",	
                      "fBodyAcc.std.Y",	"fBodyAcc.std.Z",	"fBodyAccJerk.mean.X", "fBodyAccJerk.mean.Y",	"fBodyAccJerk.mean.Z",	"fBodyAccJerk.std.X",	"fBodyAccJerk.std.Y",	"fBodyAccJerk.std.Z",	"fBodyGyro.mean.X",	
                      "fBodyGyro.mean.Y",	"fBodyGyro.mean.Z",	"fBodyGyro.std.X", "fBodyGyro.std.Y" ,	"fBodyGyro.std.Z",	"fBodyAccMag.mean",	"fBodyAccMag.std",	"fBodAccJerkMag.mean",	"fBodAccJerkMag.std",	"fBodGyroMag.mean",	
                      "fBodGyroMag.std",	"fBodGyroJerkMag.mean",	"fBodGyroJerkMag.std",	"ang.tBodyAccJerk.gravMean",	"ang.tBodGyro.gravMean",	"ang.tBodGyroJerk.gravMean",	"ang.X.gravityMean" ,	"ang.Y.gravMean" ,	"ang.Z.gravMean"))

testrainCast<- dcast(testrainMelt, Subject+Activity~variable, mean)

Step 11: Saving tidy data in text file
testrainnn<- write.table(testrainnCast, file="testrain.txt", quote=TRUE, append=FALSE, eol="\n", sep=",", row.name=FALSE, col.names=TRUE, dec=".", qmethod = c("escape", "double"), fileEncoding="")

