# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

import pandas as pd
            df=pd.read_csv("/content/SAMPLEIDS.csv")
            df
            ![image](https://github.com/user-attachments/assets/be847b6e-be19-4fc0-9458-960851fc8620)
            
df.shape         
 ![image](https://github.com/user-attachments/assets/342fad44-0e45-4322-83c3-b1ed57e9657b)
 df.describe()
 ![image](https://github.com/user-attachments/assets/48003e00-50bf-4903-b285-6a1671d87748)
    df.info()
 ![image](https://github.com/user-attachments/assets/c4ae6f4b-6b1d-4336-8f96-5a28080c4e24)
df.head(4)
            df.tail(4)
            ![image](https://github.com/user-attachments/assets/497db152-eeb9-4daf-85fd-846c4a2f52b5)
            
            
 df.isnull().sum()
            ![image](https://github.com/user-attachments/assets/395484a8-8aaf-4875-95db-f1d93ae87b7d)
            
            
 df.dropna(how='any').shape
            df.shape
            ![image](https://github.com/user-attachments/assets/84d5d03f-6a30-4055-a3ad-be470595602a)
            
            
 x=df.dropna(how='any')
            x
            ![image](https://github.com/user-attachments/assets/bc4b1bd3-573c-489f-8f3b-f942b0358ac0)
            
            
 x2=df.dropna(how='all').shape
            mn=df.TOTAL.mean()
            mn
            df.isnull().sum()
            ![image](https://github.com/user-attachments/assets/a23bf1ca-64bc-4ecd-b7f1-f3d08e1fb7e5)
            
            
  df.TOTAL.fillna(mn,inplace=True)
            df
            ![image](https://github.com/user-attachments/assets/b16e127d-cdbc-490b-8bc2-379a391e6aba)
            
            
df['M1']
            ![image](https://github.com/user-attachments/assets/49324a1f-48c1-4a15-865f-2b19ce96be41)
            
            
 df['M1'].fillna(method='ffill',inplace=True)
            ![image](https://github.com/user-attachments/assets/53d0b80c-1828-42d9-93ee-f91be82b1b72)
            
            
 df.duplicated()
            ![image](https://github.com/user-attachments/assets/d79a665c-f168-4a0b-958b-3225a6ad0900)
            
            
 l=df.M1.interpolate()
            l
            ![image](https://github.com/user-attachments/assets/f5ed36d3-e3a5-4c16-aa27-4355a293b402)
            
            
  df['DOB']
            ![image](https://github.com/user-attachments/assets/7aa00ac2-fd35-4c8a-a037-95ace32e5941)
            
            
 x
            ![image](https://github.com/user-attachments/assets/4f71f276-ed21-4097-92d6-13a85f32fe76)
            
import seaborn as sns
            sns.heatmap(df.isnull(),yticklabels=False,annot=True)
            ![image](https://github.com/user-attachments/assets/31326d4f-3aa8-4cfc-a1fc-050fe687e7f4)
            
            
 df.dropna(inplace=True)
            sns.heatmap(df.isnull(),yticklabels=False,annot=True)
            ![image](https://github.com/user-attachments/assets/b8fac803-bfae-4657-832c-36c63b2f7ec9)
            
            
import numpy as np
            age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
            af=pd.DataFrame(age)
            af
            ![image](https://github.com/user-attachments/assets/62882e03-72b6-4b44-b837-b76c26754b90)
            
            
 sns.boxplot(data=af)
            ![image](https://github.com/user-attachments/assets/afd3116c-8e97-4c83-930f-a7b9651a8fa3)
            
            
 sns.scatterplot(data=af)
            ![image](https://github.com/user-attachments/assets/8514b3a3-4d42-4715-9c27-a0402140b1cf)
            
            
 q1=af.quantile(0.25)
            q2=af.quantile(0.5)
            q3=af.quantile(0.75)
            iqr=q3-q1
            iqr
            ![image](https://github.com/user-attachments/assets/03a9cb62-a632-436d-82ed-eb19dcfba7a8)
            
            
Q1=np.percentile(af,25)
            Q3=np.percentile(af,75)
            IQR=Q3-Q1
            IQR
            ![image](https://github.com/user-attachments/assets/7186986f-3859-41af-b49f-d67446809e5e)
            
            
  lower_bound=Q1-1.5*IQR
            upper_bound=Q3+1.5*IQR
            
            
 lower_bound
            upper_bound
            ![image](https://github.com/user-attachments/assets/c7355647-ff86-4203-859e-fd4168c0f1fe)
            
            
 outliers=[x for x in age if x<lower_bound or x>upper_bound]
            print("Q1:", Q1)
            print("Q3:", Q3)
            print("IQR:", IQR)
            print("Lower bound:", lower_bound)
            print("Upper bound:", upper_bound)
            print("Outliers:", outliers)
            ![image](https://github.com/user-attachments/assets/98fe00c9-0fca-44cf-998b-2737e82481b2)
            
            
 af=af[((af>=lower_bound)&(af<=upper_bound))]
            af
            ![image](https://github.com/user-attachments/assets/e4666ad5-333f-4ec4-9ded-51441b56ec33)
            
            
af.dropna()
            ![image](https://github.com/user-attachments/assets/1721220d-02c6-4f82-8f95-9ae6755316b3)
            
            
 sns.boxplot(data=af)
            ![image](https://github.com/user-attachments/assets/8b964a58-c90d-4cc8-b605-0653c7712015)
            
            
  data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
            mean=np.mean(data)
            std=np.std(data)
            print("Mean of the Dataset is", mean)
            print("Std. Deviation is", std)
            
            
 threshold=3
            outlier=[]
            for i in data:
              z=(i-mean)/std
              if z>threshold:
                outlier.append(i)
            print('outlier in dataset is',outlier)
            image
            
 from scipy import stats
            data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                            66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
            df=pd.DataFrame(data)
            df
            ![image](https://github.com/user-attachments/assets/eb3a3c20-f9cb-4131-844a-00e4342242c5)
            
            
 z=np.abs(stats.zscore(df))
            print(df[z['weight']>3])
            ![image](https://github.com/user-attachments/assets/37ff6fbe-1e67-454b-8d35-8a4fcd8c5be1)
            
            
 val=[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]
            
  out=[]
            def d_o(val):
              ts=3
              m=np.mean(val)
              sd=np.std(val)
              for i in val:
                z=(i-m)/sd
                if np.abs(z)>ts:
                  out.append(i)
              return out
            
op=d_o(val)
            
 op
            ![image](https://github.com/user-attachments/assets/8059e283-c262-4508-a798-b662041b13dd) 


            
            
            
# Result
          Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
