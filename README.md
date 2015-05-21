
README file
=============
This repo was created as part of the project in "Getting and Cleaning Data" course in Coursera.org.

There are three files in the repo:

1. A README file (**_README.md_**), explaining all details for the repo
2. A script (**_run_analysis.R_**)
3. A code book file (**_CodeBook.md_**)

##run_analysis.R
#### *General Info*
This script prepares tidy data that can be used for later analysis. It uses data collected from the accelerometers from the Samsung Galaxy S smartphone, in a study carried out to develop the most advanced algorithms to attract new users in weareble computing. A full description of the original data is available at the study website: [Human Activity Recognition Using Smartphones Data Set](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones).

The source for the data used in this specific project was downloaded from https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip.

#### *Prerequisites*
In order for **_run_analysis.R_** to work properly, the following must be true:
* You must download the zipped file from [here](https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip), and unzip it in your current R (or RStudio) working directory;
* You must have package 'dplyr' installed;
* You must have package 'data.table' installed;

The packages mentioned before will be loaded automatically by **_run_analysis.R_**, so as long as they are installed there is no need to source them before executing this script.

#### *Script steps*
The script does the following:

1. Merges the training and the test sets to create one data set
2. Extracts only the measurements on the mean and standard deviation for each measurement
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject

The script contains comments that describe in a simple manner what is the result for each part of the code. The order in which the steps are presented above and the order in which they are executed in the script are somewhat different, but the results are the same.

Some details for each step are presented below.

#### *Merging of the training and the test sets into one data set:*
This is done in four steps:
* Files containing subject information for the test and training sets are merged (files **_subject_test.txt_**, **_subject_train.txt_**). **_subject_** is applied as a variable name for this information.
* Files containing activity information for the test and training sets are merged (files **_y_test.txt_**, **_y_train.txt_**). **_activity_** is applied as variable name for this information.
* Files containing variables information for the test and training sets are merged (561 variables - files **_X_test.txt_**, **_X_train.txt_**).
* All data from the merges above are merged into one single data frame (**_subject_** data, **_activity_** data, variables data [561 features of the study]). This results in a data frame with 10.299 rows and 563 columns.

#### *Extraction of the measurements on the mean and standard deviation for each measurement:*
From the whole data set generated by the merge step before, the script selects only measurements representing means [*mean()*] and standard deviations [*std()*].
It is important to note that the original data set contains some features called *MeanFreq()*, but these were not considered to rearrange this data set (note that in the **_features.txt_** in the original data set, the measure for *mean* and for *meanFreq* are presented as different calculations of the original measured variables. Therefore, it was my interpretation that the Coursera project asked only for mean and standard deviation as defined by *mean()* and *std()* in the original features names).

Instructions for the project do not specify in detail if *MeanFreq* should be considered, so it is also my opinion that both solutions could be considered correct.

The resulting data frame has 10.299 rows and 68 columns.

#### *Applying descriptive activity names to name the activities in the data set:*
For variable **_activity_**, replaces the coded number (1:6) by their descriptive correspondent ('WALKING',...). It uses the file **_activity_labels.txt_** as the source for the codification, as follows:

1. WALKING
2. WALKING_UPSTAIRS
3. WALKING_DOWNSTAIRS
4. SITTING
5. STANDING
6. LAYING


#### *Labeling the data set with descriptive variable names:*
For this step, each variable (originally called 'feature') is assigned to the name provided with the original data set (available in **_features.txt_** from that original data set). This was chosen because the names in the original data set were considered sufficiently descriptive. It is important to note that there are typos in the original names (some variables present a "BodyBody" part). In this step these typos are corrected, and replaced by "Body".

A detailed description for the meaning of variable names is given in the code book file (**_CodeBook.md_**).

#### *Creating (from the data set in step 4) an independent tidy data set with the average of each variable for each activity and each subject:*
As asked, data were grouped by subject (30 subjects) and activity (6 types of activities), so there is a total 180 combinations of these variables. Each column represent the average of an original variable mean or the average of an original variable standard deviation (for a given subject and activity).

The resulting tidy data is presented as a data frame with 180 rows and 68 columns.

The data can be considered tidy because it complies with the following principles:
* Each variable measured is in one column
* Each different observation of that variable is in a different row

#### run_analysis.R results
After **_run_analysis.R_** is executed, the user will have a variable in his Environment called **_tidy_data_**. This variable contain the data frame with the tidy data as described above.

Furthermore, a **_tidy_data.txt_** file is automatically saved in his working directory. If one tries to to open it in notepad or Excel, it might look odd (this is because it was generated by the fuction 'write.table()', as indicated by project's orientations). As a consequence, if one would like to see the data in a nice formatted way, it should be loaded in R (or RStudio) using the following commands:

```
data <- read.table("tidy_data.txt", header = TRUE)
View(data)
```

##CodeBook.md
The code book cotains information that explains all variables in the tidy data exported by **_run_analysis.R_**.
