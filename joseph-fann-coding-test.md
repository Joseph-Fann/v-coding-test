```python
import json

import pandas as pd
```


```python
with open('interview-policies.json', 'r') as f:
    data = json.loads(f.read())
```


```python
df = pd.DataFrame(data['data'], columns=data['fields'])
```

####  Compute and output:

#### Total number of policies


```python
len(data['data'])
```




    100000



#### Count of policies that include a waiver of subrogation


```python
sum(df['Has Waiver of Subrogation'])
```




    49948



#### List of states by the sum of their Building Coverage Limit


```python
df.groupby('Location State')['Building Coverage Limit'].sum()
```




    Location State
    AK    1354404000
    AL    1277021000
    AR    1302033000
    AZ    1276073000
    CA    1301775000
    CO    1237416000
    CT    1345233000
    DE    1258751000
    FL    1275849000
    GA    1314357000
    HI    1268562000
    IA    1246920000
    ID    1275667000
    IL    1342401000
    IN    1325381000
    KS    1279724000
    KY    1302604000
    LA    1287238000
    MA    1354120000
    MD    1356508000
    ME    1348200000
    MI    1325393000
    MN    1249770000
    MO    1297153000
    MS    1253193000
    MT    1331916000
    NC    1281371000
    ND    1296444000
    NE    1307185000
    NH    1318368000
    NJ    1288503000
    NM    1254797000
    NV    1314614000
    NY    1264085000
    OH    1307763000
    OK    1302472000
    OR    1279898000
    PA    1266194000
    RI    1267241000
    SC    1292225000
    SD    1269965000
    TN    1244554000
    TX    1280149000
    UT    1270053000
    VA    1320433000
    VT    1298105000
    WA    1317469000
    WI    1329146000
    WV    1242091000
    WY    1343296000
    Name: Building Coverage Limit, dtype: int64



#### Convert the above JSON file (which is one large object) to a file of JSON rows where each row is a complete json object. The keys of the new rows should be the “fields” in the original file, and the values the corresponding value for each row.

#### Sort this new file by GL Aggregate Limit


```python
# Sorting by GL Aggregate Limit, when values are equal, Pandas default 
# to by index value in original json
gl_df = df.sort_values(by=['GL Aggregate Limit'], ascending=True).to_dict('records')
```


```python
with open('gl_output.json', 'w') as f:
    json.dump(gl_df, f)
```


```python

```
