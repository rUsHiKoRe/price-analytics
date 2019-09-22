import pandas as pd
shoes=pd.read_csv('E:\miniproject\sdl\shoesp.csv',low_memory=False)
#delete unnecessary columns
del shoes['features']
del shoes['prices.currency']
del shoes['prices.amountMax']
del shoes['prices.dateAdded']
shoes.head()

#rename
shoes=shoes.rename(columns={'dateAdded':'date/time','prices.amountMin':'prices($)'})
shoes['date/time']= pd.to_datetime(shoes['date/time'])
shoes.head()
#checking any null values
shoes.isnull().sum()

#remove null values
shoes['brand']=shoes['brand'].fillna(method="ffill")
shoes['prices($)']=shoes['prices($)'].fillna(method="ffill")
shoes.isnull().sum()

#sorting data by date/time
shoes=shoes.sort_values(by='date/time')
shoes.set_index('date/time',drop=True).head()
