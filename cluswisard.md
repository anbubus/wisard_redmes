# ClusWisard
## constructor:
```python
from wisardpkg import ClusWisard

addressSize = 3 
minScore = 0.1 
threshold = 10
discriminatorLimit = 5

clus = ClusWisard(
   addressSize,              # required
   minScore,                 # required
   threshold,                # required
   discriminatorLimit,       # required
   completeAddressing=True,  # optional
   ignoreZero=False,         # optional
   verbose=False,            # optional
   indexes=[],               # optional
   base=2,                   # optional
)
```
The default value for the optional parameters are showing in the example above.
- **addressSize: [int]** is the size of addressing RAM.
- **minScore: [float]** is the minimum score accept by cluswisard to choose to create a discriminator. Must be between 0 and 1.
- **threshold: [int]** is the limit of examples learned by a discriminator.
- **discriminatorLimit: [int]** is the limit of discriminator by cluster in supervised and semi-supervised learning, but in unsupervised learning this is the limit of classes that can be created.
- **ignoreZero: [boolean]** this enable or disable the wisard to read the address zero in each RAM.
- **completeAddressing: [boolean]** this enable or disable the automatic complete of addressing in the case when the size of entry is not divisible by address size, this create redundant information, but address all indexes of entry.
- **verbose: [boolean]** enable or disable prints of the progress of train() and classify()
- **indexes: [list(int)]** this is to use a specific addressing of entry to the discriminators, all discriminators wiil use this addressing.
- **base: [int]** this is the base of addressing, by default is binary addressing.

## methods:
### train
This method train with the data passed to it. In the case of labels, can be a list for supervised learning or a dictinary to semi-supervised learning.
```python

# load input data, just zeros and ones  
X = [
      [1,1,1,0,0,0,0,0],
      [1,1,1,1,0,0,0,0],
      [0,0,0,0,1,1,1,1],
      [0,0,0,0,0,1,1,1]
    ]

# load label data, which must be a string array
y = [
      "cold",
      "cold",
      "hot",
      "hot"
    ]

# load label data, which must be a dictionary with key integer and value string
y2 = {
       1: "cold",
       2: "hot
     }

ds = DataSet(X,y)

# to supervised learning
clus.train(ds)

ds2 = DataSet(X,y2)

# to unsupervised learning
clus.trainUnsupervised(ds2)

```
Keep in mind that when a dataset is passed to this method, first it will train with supervised piece and after it will train with unsupervised piece.
### trainUnsupervised
This method train with the data passed to it. This use the unsupervised learning.
```python

# load input data, just zeros and ones  
X = [
      [1,1,1,0,0,0,0,0],
      [1,1,1,1,0,0,0,0],
      [0,0,0,0,1,1,1,1],
      [0,0,0,0,0,1,1,1]
    ]

# to unsupervised learning
ds = DataSet(X)
clus.trainUnsupervised(ds)

```
### classify
This method classify the data passed to it, based on what it learn, for supervised and semi-supervised learning.
```python

# load input data, just zeros and ones  
X = [
      [1,1,1,0,0,0,0,0],
      [1,1,1,1,0,0,0,0],
      [0,0,0,0,1,1,1,1],
      [0,0,0,0,0,1,1,1]
    ]

# the output is a list of string, this represent the classes atributed to each input
ds = DataSet(X)
out = clus.classify(ds)

for oneout in out:
    print(oneout)

# if its just an single input
x = [1,1,1,0,0,0,0,0]

bin = BinInput(x)

# the output is a single string
out_ = clus.classify(bin)

print(out_)
```

### classifyUnsupervised
This method classify the data passed to it, based on what it learn, for unsupervised learning.
```python

# load input data, just zeros and ones  
X = [
      [1,1,1,0,0,0,0,0],
      [1,1,1,1,0,0,0,0],
      [0,0,0,0,1,1,1,1],
      [0,0,0,0,0,1,1,1]
    ]

# the output is a list of string, this represent the classes atributed to each input
ds = DataSet(X)
out = clus.classifyUnsupervised(X)

for oneout in out:
    print(oneout)

# if its just an single input
x = [1,1,1,0,0,0,0,0]

bin = BinInput(x)

# the output is a single string
out_ = clus.classify(bin)

print(out_)
```

### getMentalImages
This one show the pattern learned by the model, it return a dictionary where the key is of type string and it is the class and value is the list of list of integers representing the learned pattern for each discriminator in the cluster.
```python
patterns = clus.getMentalImages()

for key in patterns:
    cluster = patterns[key]
    for index,discriminator in enumerate(cluster)
        print(key, index, discriminator)

```
### json
This return the configuration and ram values as JSON format converted to string.
```python
print("ClusWisard: ", clus.json())
# or pass true as parameter to save ram data in files (this is useful for huge rams)
print("ClusWisard: ", clus.json("path/to/save/data"))

```
### getsizeof
This returns the model size.
```python
print(clus.getsizeof())

```
### rank
Returns a class rank based on the discriminators votes to an input or a list of inputs.
```python
X = [
      [1,1,1,0,0,0,0,0],
      [1,1,1,1,0,0,0,0],
      [0,0,0,0,1,1,1,1],
      [0,0,0,0,0,1,1,1]
]

ds = wp.DataSet(X)
clus.rank(ds)

```
### rankUnsupervised
Returns classification scores using the unsupervised cluster.
```python



```
### getAllScores
Retrieves scores for all classes for a given input.
```python
X = [
      [1,1,1,0,0,0,0,0],
      [1,1,1,1,0,0,0,0],
      [0,0,0,0,1,1,1,1],
      [0,0,0,0,0,1,1,1]
]

ds = wp.DataSet(X)
clus.getAllScores(ds)

```
### setMinScore, setThreshold, setDiscriminatorsLimit
Allow modifying the model parameters after initialization.
```python
clus.setMinScore(0.1)
clus.setThreshold(10)
clus.setMinScore(5)

```
