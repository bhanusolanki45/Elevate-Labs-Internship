import pandas as pd
df = pd.read_csv('C:\\Users\\bhanu\\Downloads\\archive\\netflix_titles.csv')
print(df.head())
print(df.info())

# Finding Missing Values

print(df.isnull().sum())

# Missing Values:
# Filled director (2,634 missing) with “Unknown”.
# Filled cast (825 missing) with “Unknown”.
# Filled country (831 missing) with “Unknown”.
# Fiiled 10 rows with missing date_added ( filled with mode)
# Filled rating (4 missing) with “Not Rated”
# Dropped 3 rows with missing duration (“Unknown”).

df['director'].fillna('Unknown', inplace=True)
df['cast'].fillna('Unknown',inplace=True)
df['country'].fillna('Unknown', inplace=True)
print(df['date_added'].mode()[0])
df['date_added'].fillna(df['date_added'].mode()[0],inplace=True)
df['rating'].fillna('Not Rated', inplace=True)
df['duration'].fillna('Unknown', inplace=True)

print(df.isnull().sum())


# Check Duplicate
print(df.duplicated(). sum())
print(df['show_id'].duplicated().sum())

# Since there is no any Duplicate Value in the DataSet


# Standardize Text value as all Column's text in a lower case and proper spacinng.
# Removed leading/trailing spaces
# Converted to lowercase

df['country'] = df['country'].str.strip()         
df['country'] = df['country'].str.lower()         
print(df['country'].unique())


df['type'] = df['type'].str.strip()        
df['type'] = df['type'].str.lower()        
print(df['type'].unique())

df['title'] = df['title'].str.strip()      
df['title'] = df['title'].str.lower()       
print(df['title'].unique())

df['director'] = df['director'].str.strip()         
df['director'] = df['director'].str.lower()        
print(df['director'].unique())

df['cast'] = df['cast'].str.strip()       
df['cast'] = df['cast'].str.lower()         
print(df['cast'].unique())

df['listed_in'] = df['listed_in'].str.strip()         
df['listed_in'] = df['listed_in'].str.lower()      
print(df['listed_in'].unique())


df['description'] = df['description'].str.strip()         
df['description'] = df['description'].str.lower()        
print(df['description'].unique())


#  Convert date formats to a consistent type (e.g., dd-mm-yyyy)

df['date_added']=pd.to_datetime(df['date_added'], errors = 'coerce')
df['date_added']= df['date_added'].dt.strftime('%d-%m-%Y')
print(df['date_added'].isnull().sum())


print(df['date_added'].mode()[0])
df['date_added'].fillna(df['date_added'].mode()[0],inplace=True)

print(df.isnull().sum())


# Rename column headers to be clean and uniform (e.g., lowercase, no spaces).

df.columns = df.columns.str.lower().str.replace(' ','-')
print(df.columns)


 # Check and fix data types (e.g., age should be int, date as datetime).

print(df.dtypes)
