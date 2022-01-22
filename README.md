# Time-Series-

import pandas as pd

parser = lambda x: pd.datetime.strptime(x,'%Y-%m-%d %I-%p')
df = pd.read_csv('ETH.csv',parse_dates=['Date'],date_parser = parser)
df['Date'] = pd.to_datetime(df['Date'], format = '%Y-%m-%d %I-%p')



df['Date'] = pd.to_datetime(df['Date'], format = '%Y-%m-%d %I-%p')


df['Date'].dt.date.max()

#Filtering dates (condition in string format)
filt = (df['Date'] >= '2019') & (df['Date'] < '2020')
filt1 = (df['Date'] >= pd.to_datetime('2019-01-01')) & (df['Date'] < pd.to_datetime('2020-01-01'))
df.loc[filt1]


#Filtering by index
df.reset_index()
df.set_index('Date',inplace=True)
df['2019']
df['2020-01-01':'2020-02-31']


df['2020-01-01']['High'].max()

#Find the daily high price by resampling
highs = df['High'].resample('D').max()

%matplotlib inline

highs.plot()



#Return aggregation functions for several columns
df.resample('W').agg({'Close':'mean','High':'max','Low':'min','Volume':'sum'})
