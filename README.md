import pandas as pd

# Load the dataset
df = pd.read_csv('data.csv')

# Display the first few rows of the dataframe
print("Original Data:")
print(df.head())

# Handling Missing Values
# Fill missing Age values with the mean age
df['Age'].fillna(df['Age'].mean(), inplace=True)

# Fill missing Salary values with the mean salary
df['Salary'].fillna(df['Salary'].mean(), inplace=True)

# Fill missing Joining Date values with a placeholder date
df['Joining Date'].fillna('2022-01-01', inplace=True)

# Drop rows where Gender is missing
df.dropna(subset=['Gender'], inplace=True)

# Convert data types
df['Age'] = df['Age'].astype(int)
df['Salary'] = df['Salary'].astype(float)
df['Joining Date'] = pd.to_datetime(df['Joining Date'])

# Display cleaned data
print("\nCleaned Data:")
print(df.head())

# Data Analysis
# Basic statistics
print("\nBasic Statistics:")
print(df.describe())

# Average Salary by Gender
avg_salary_by_gender = df.groupby('Gender')['Salary'].mean()
print("\nAverage Salary by Gender:")
print(avg_salary_by_gender)

# Number of employees who joined after 2020
joined_after_2020 = df[df['Joining Date'] > '2020-12-31'].shape[0]
print(f"\nNumber of employees who joined after 2020: {joined_after_2020}")

# Save the cleaned data to a new CSV file
df.to_csv('cleaned_data.csv', index=False)
