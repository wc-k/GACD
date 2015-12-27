
Getting and Cleaning Data Course Project

Assignment:
You should create one R script called run_analysis.R that does the following.

1.	Merges the training and the test sets to create one data set.
2.	Extracts only the measurements on the mean and standard deviation for each measurement.
3.	Uses descriptive activity names to name the activities in the data set
4.	Appropriately labels the data set with descriptive variable names.
5.	From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

Files:

1.  README.md 
2.  run_analysis.R that does the merging and transformations
3.  CodeBook.md describes the variables, the data, the transformations, and the work that is performed to clean up the data

Assumptions:

1.	The Samsung data is available in the working directory and/or the user is connected to the Internet. The script checks:
    a.	If an unzipped folder named "UCI HAR Dataset" with the directory structure underneath that left intact from the original zip file          (e.g., there are subdirectories called "test" and "train" in "UCI HAR Dataset") is available. If so, the script continues.
    b.	If the "UCI HAR Dataset" folder is not available, the script checks whether the original zip file is available. If so, it is               unzipped and the script continues.
    c.	If the original zip file is not available, the script downloads the file from the Internet, unzips it, and continues the script.
2.	The user has either previously installed the plyr, dplyr, and reshape2 packages or is connected to the Internet so the script can          install them.
3.	"Extracts only the measurements on the mean and standard deviation" is assumed to mean all variables from the original data set with       the strings "Mean," "mean," or "std" in their names.

Process:

The run_analysis.R performs the following steps:

1.	Check whether the UCI HAR Dataset is available in the working directory. If not, the script checks for the zip file, unzips it, and        continues. If that is also unavailable, the script downloads the zip file, unzips it, and continues.

2.	Merge the training and the test sets to create one data set (requirement #1)

    a.	Load the "plyr," "dplyr," and "reshape2" packages as they are necessary for the data manipulation that follows. If they have not           been previously installed, the script installs them.

    b.	Read the "Activity Labels" and "Features" data into data frames, labeling the columns and changing the Feature data to character           type.
    
    c.	Read the separate parts of the training data set (training activities, "y_train.txt;" training data, "X_train.txt;" and training           subject, "subject_train.txt") and combine them into a single data frame using cbind.
    
    d.	Read the separate parts of the test data set (test activities, "y_test.txt;" test data, "X_test.txt;" and test subject,                    "subject_test.txt") and combine them into a single data frame using cbind.
    
    e.	Merge the training and test data sets into a single data frame using rbind.
    
    f.	Add activity labels from the "Activity Labels" data frame (Uses descriptive activity names to name the activities in the data set          (requirement #3))
    
    g.	Name the columns based on the "Features" data (Appropriately labels the data set with descriptive variable names (requirement #4))

3.	Extract only the measurements on the mean and standard deviation for each measurement (requirement #2)

    a.	Subset the merged data frame to the columns representing mean and standard deviation
    
    b.	To do this, search for all variable names containing the strings "Mean," "mean," and "std."
    

4.	Create a second, independent tidy data set with the average of each variable for each activity and each subject (requirement #5)
    a.	Make all column names legal for R by removing all parentheses and dashes.
    b.	Change variable names to Camel Case (i.e., capitalize "Mean" and "Std" regardless of where in the column name they appear) to              increase readability.
    c.	Change the names of the misnamed variables in the original data set (i.e., change "BodyBody" to "Body").
    d.	Change the "Subject" column to a factor for easier manipulation.
    e.	Sort the merged data frame by "Subject" and "Activity"
    f.	Calculate the average (mean) of each numeric column and return a data frame ("merged_summary" in the script) with the average for          each subject/activity combination.
    g.	Write this data frame to a text file called "samsung_summary.txt" using "row.names = FALSE."

