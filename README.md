# Social-Data-Science-Group-8
# Home assignment
Answer 3.1.3

#Answer 3.1.3

l1 = ['r ', 'Is', '>', ' < ', 'g ', '?']


''.join([l1[1], ' ', l1[0].strip(), l1[2], l1[-2].strip(), str(l1[-1])])


'Is r>g?'

# Answer 3.1.4

words = {}
values = []
keys = ['animal', 'coffee', 'python', 'unit', 'knowledge', 'tread', 'arise']
vowels = ['a', 'e', 'i', 'o', 'u', 'y']

​

for key in keys:
    if key[0] in vowels : 
        values.append(True)
    else :
        values.append(False)
print(values)
​
keys_values = list(zip(keys, values))
words = dict(keys_values)
dict(words)
[True, False, False, True, False, False, True]
{'animal': True,
 'coffee': False,
 'python': False,
 'unit': True,
 'knowledge': False,
 'tread': False,
 'arise': True}

# Answer 3.3.2

#Creating function that can generate correct URL
import requests 
def construct_link(table_id, variables):
    base = 'https://api.statbank.dk/v1/data/{id}/JSONSTAT?lang=en'.format(id = table_id)
    
    for var in variables:
        base += '&{v}'.format(v = var)
​
    return base 
construct_link('FOD', ['Tid=*', 'BARNKON=P'])
'https://api.statbank.dk/v1/data/FOD/JSONSTAT?lang=en&Tid=*&BARNKON=P'

#Wrapping a function around saving a file, pulled from a URL
def function2(x):
    ladies = requests.get(x)
    ladies.json()
    
    with open ('ladies1.json', 'w') as f:
        resp_json_str = json.dumps(ladies.json()) #dette får det tilbage til dets originale form
        f.write(resp_json_str)
    return ladies
function2('https://api.statbank.dk/v1/data/FOD/JSONSTAT?lang=en&Tid=*&BARNKON=P') 
#the URL you've generated from the other link, could be any link with data attachewd

# Answer 4.1.1

import pandas as pd
url = 'https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/by_year/1864.csv.gz'
df = pd.read_csv(url, header=None, compression='gzip')
print(df.head())
             0         1     2    3    4    5  6   7
0  ITE00100550  18640101  TMAX   10  NaN  NaN  E NaN
1  ITE00100550  18640101  TMIN  -23  NaN  NaN  E NaN
2  ITE00100550  18640101  PRCP   25  NaN  NaN  E NaN
3  ASN00079028  18640101  PRCP    0  NaN  NaN  a NaN
4  USC00064757  18640101  PRCP  119  NaN  NaN  F NaN

# Answer 4.1.2

df=df.iloc[:,0:4]
column_name = ['station', 'data', 'type', 'value']
df.columns=column_name
print(df.head())
       station      data  type  value
0  ITE00100550  18640101  TMAX     10
1  ITE00100550  18640101  TMIN    -23
2  ITE00100550  18640101  PRCP     25
3  ASN00079028  18640101  PRCP      0
4  USC00064757  18640101  PRCP    119

# Answer 4.1.3

df_copy = df[(df.station == 'ITE00100550') & (df.type == 'TMAX')].copy()
print(df_copy.head())
         station      data  type  value
0    ITE00100550  18640101  TMAX     10
75   ITE00100550  18640102  TMAX      8
152  ITE00100550  18640103  TMAX    -28
227  ITE00100550  18640104  TMAX      0
305  ITE00100550  18640105  TMAX    -19

# Answer 4.1.4

df_copy['TMAX_F'] = df_copy.value * 1.8 + 32
print(df_copy.head())
         station      data  type  value  TMAX_F
0    ITE00100550  18640101  TMAX     10    50.0
75   ITE00100550  18640102  TMAX      8    46.4
152  ITE00100550  18640103  TMAX    -28   -18.4
227  ITE00100550  18640104  TMAX      0    32.0
305  ITE00100550  18640105  TMAX    -19    -2.2
