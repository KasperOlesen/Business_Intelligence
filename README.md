# Assignment 3

### 1) Geocode the the entire dataset
#### Setup

**Download som og unzip**

```python
%%bash
wget --directory-prefix=./data/ http://download.geofabrik.de/europe/denmark-latest.osm.bz2
bzip2 -d ./data/denmark-latest.osm.bz2
```

**Installation af osmread**

```python
%%bash
sudo pip install osmread
```

**Data fra csv fil (Kan findes i zip under Assigment_3 folder:**

```python
import pandas as pd
df = pd.read_csv('boliga_all.csv')
df.head()
```

**Data fra osm fil**

```python
from osmread import parse_file, Node
from collections import defaultdict

postcodes = defaultdict(lambda: defaultdict(dict))

def decode_node_to_csv():
    for entry in parse_file('./data/denmark-latest.osm'):
        if (isinstance(entry, Node) and 
            'addr:street' in entry.tags and 
            'addr:postcode' in entry.tags and 
            'addr:housenumber' in entry.tags):
                yield entry


for idx, decoded_node in enumerate(decode_node_to_csv()):
    postcodes[decoded_node.tags['addr:postcode']][decoded_node.tags['addr:street']][decoded_node.tags['addr:housenumber']] = decoded_node.lon, decoded_node.lat
            
```

**Result:**
<br>
Bla bla bla


### 2) Convert all sales dates in the dataset into proper datetime
```python
df["sell_date"] = pd.to_datetime(df["sell_date"], dayfirst=True, errors='coerce')
```

### 3) Compute the average price per square meter for the years 1992 and 2016
```python
import pandas as pd
df = pd.read_csv('boliga_all.csv')

df.index = df['sell_date']
del df['sell_date']

def to_csv(data, name):
    try:
        data.to_csv(name + '.csv', sep='\t')
    except:
        print('Error')
    
to_csv( df[df['zip_code'] == '1050 København K']['1992'],'1050')   
to_csv( df[df['zip_code'] == '5000 Odense C']['1992'],'5000')   
to_csv( df[df['zip_code'] == '8000 Aarhus C']['1992'],'8000')   
to_csv( df[df['zip_code'] == '9000 Aalborg']['1992'],'9000')    
```


### 4) Create, four new CSV files containing the sales data of, Copenhagen, Odense, Aarhus, and Aalborg.
**Result:**
<br>
Bla bla bla

### 5) Create a 2-dimensional scatter plot
**Result:**
<br>
Bla bla bla

### 6) Use the following function, which computes the Haversine Distance
**Result:**
<br>
Bla bla bla

