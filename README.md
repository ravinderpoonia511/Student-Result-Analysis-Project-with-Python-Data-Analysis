**Student Exam Scores Analysis**
This project analyzes student exam scores based on various factors like parent education, parental marital status, gender, and ethnic group. The dataset used in this project is downloaded from Kaggle.

**Required Libraries:**
Ensure all required libraries are installed by including them in your requirements.txt file.

Important: The os module is built into Python and does not need to be installed separately.

**Project Setup**
1. Clone the repository.
2. 
3. Install dependencies:
pip install -r requirements.txt

5. Download Dataset
Using KaggleHub to download the latest version of the dataset:

6. Load the dataset into a pandas DataFrame


**Key Insights:**
Gender Distribution: The number of female students is higher than male students in the dataset.

Parent Education Impact: Higher parental education correlates with better student performance in all subjects.

Parental Marital Status: Parental marital status does not significantly impact student scores.

Outliers in Math Scores: Box plot analysis shows that there may be some outliers in Math scores.

Ethnic Group Distribution: The dataset has a balanced distribution of students from various ethnic groups.


**Python Code**
'''sql
import kagglehub
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import os

# Download latest dataset from Kaggle
path = kagglehub.dataset_download("desalegngeb/students-exam-scores")

# List the files in the dataset directory
files = os.listdir(path)
print("Path to dataset files:", path)
print(files)

# Load the dataset into a pandas DataFrame
df = pd.read_csv(f'{path}\\Expanded_data_with_more_features.csv')
df.head()

# Summary statistics of the dataset
df.describe()

# Information about the dataset, including data types and null values
df.info()

# Checking for missing values
df.isnull().sum()

# Unique values in the 'LunchType' and 'EthnicGroup' columns
df.LunchType.unique()
df.EthnicGroup.unique()

# Remove 'Unnamed: 0' column from the DataFrame
df = df.drop('Unnamed: 0', axis=1)
df.head()

# Plot the distribution of students based on Gender
plt.figure(figsize=(4,5))
ax = sns.countplot(data=df, x='Gender')
ax.bar_label(ax.containers[0])
plt.title('Gender Distribution')
plt.show()

# Calculate the mean scores for Math, Reading, and Writing based on parent education
gb = df.groupby('ParentEduc').agg({'MathScore': 'mean', 'ReadingScore': 'mean', 'WritingScore': 'mean'})
print(gb)

# Heatmap to visualize the impact of parent education on scores
sns.heatmap(data=gb, annot=True)
plt.title("Parent Education Impact on Student's Scores")
plt.show()

# Calculate the mean scores for Math, Reading, and Writing based on parental marital status
ms = df.groupby('ParentMaritalStatus').agg({'MathScore': 'mean', 'ReadingScore': 'mean', 'WritingScore': 'mean'}).round(2)
print(ms)

# Heatmap to visualize the impact of parental marital status on scores
sns.heatmap(data=ms, annot=True)
plt.title("Parental Marital Status Impact on Student's Scores")
plt.show()

# Box plot to check for outliers in Math scores
sns.boxplot(data=df, x='MathScore')
plt.title('Math Score Distribution and Outliers')
plt.show()

# Count the number of students belonging to each ethnic group
groupA = df.loc[df['EthnicGroup'] == 'group A', 'EthnicGroup'].count()
groupB = df.loc[df['EthnicGroup'] == 'group B', 'EthnicGroup'].count()
groupC = df.loc[df['EthnicGroup'] == 'group C', 'EthnicGroup'].count()
groupD = df.loc[df['EthnicGroup'] == 'group D', 'EthnicGroup'].count()
groupE = df.loc[df['EthnicGroup'] == 'group E', 'EthnicGroup'].count()

# Plotting a pie chart for the distribution of ethnic groups
l = ['group A', 'group B', 'group C', 'group D', 'group E']
mlist = [groupA, groupB, groupC, groupD, groupE]
plt.pie(mlist, labels=l, autopct="%1.2f%%")
plt.title('Distribution of Ethnic Groups')
plt.show()

'''
