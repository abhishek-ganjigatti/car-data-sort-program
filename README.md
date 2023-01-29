# car-data-sort-program
to sort and change data type to provide a graph data (DS)

[CAR DETAILS FROM CAR DEKHO.csv](https://github.com/abhishek-ganjigatti/car-data-sort-program/files/10529132/CAR.DETAILS.FROM.CAR.DEKHO.csv)
import pandas as pd
df=pd.read_csv("E:\OneDrive\Pictures\Desktop\data sets for py\CAR DETAILS FROM CAR DEKHO.csv")
 #provides information about datatype of the column


#to change owner to simple terms (Test Drive Car =0)(First Owner =1)(Second Owner = 1)
# (Third Owner=3) & (Fourth & Above Owner=4)
df.replace('First Owner','1',inplace=True)
df.replace('Fourth & Above Owner','4',inplace=True)
df.replace('Test Drive Car','0',inplace=True)
df.replace('Second Owner','2',inplace=True)
df.replace('Third Owner','3',inplace=True)

# deleting 'seller_type' column
df=df.drop('seller_type',axis=1)

##
#convert_dict={'owner':int}  #convert datatype of a column
#df=df.astype(convert_dict)
#convert_dict={'owner':int}  #convert datatype of a column
#df=df.astype(convert_dict)
##

#to change km driven to simple terms (>50k = 2)(>100k = 5)&(<100k = 8)
i=0
while i <= 4339:
    if df.loc[i,'km_driven']<=50000:
        df.loc[i, 'km_driven']=2
    elif 100000>df.loc[i,'km_driven']>50000:
        df.loc[i, 'km_driven']=5
    else :
        df.loc[i, 'km_driven']=8
    i=i+1

 # to convert buying 'year' to age
df['age']=2022-df['year']
df.drop('year',axis=1,inplace=True)

#to change fuel to simple terms (Petrol = 1)(Diesel = 2)(CNG = 3)(LPG = 4)&(Electric = 5)
df.replace('Petrol','1',inplace=True)
df.replace('Diesel','2',inplace=True)
df.replace('CNG','3',inplace=True)
df.replace('LPG','4',inplace=True)
df.replace('Electric','5',inplace=True)


# to  change transmission to simple terms (transmission = 1)(Automatic = 2)
df.replace('Manual','1',inplace=True)
df.replace('Automatic','2',inplace=True)

#to simplify price(x*10000)
df.rename(columns = {'selling_price':'price*10k'}, inplace = True)
df = df.astype({'price*10k':'float'})
i=0
while i <= 4339:
    x=df.loc[i, 'price*10k']/10000
    df.loc[i, 'price*10k']=x
    i=i+1
df = df.astype({'transmission':'int'})
df = df.astype({'owner':'int'})
df = df.astype({'fuel':'int'})

#df=pd.get_dummies(df,drop_first=True)

df3=df
print(df.head())
