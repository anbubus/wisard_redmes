# Wisard
## constructors:
### type 1
```python
addressSize=3

wsd = Wisard(
   addressSize,              # required
   verbose=False,            # optional
   balanced=False,           # optional
   ignoreZero=False,         # optional
   completeAddressing=True,  # optional
   indexes=[],               # optional
   base=2,                   # optional
 
)
```
The default value for the optional parameters are showing in the example above.
- **addressSize: [int]** is the size of addressing RAM.
- **verbose: [boolean]** enable or disable prints of the progress of train() and classify()
-**balanced:[boolean]** when enabled, this adjust how the classification is performed based on the number os training samples. For example, when False, if a class has more examples it can dominate the cassification since it has more stores patterns.
- **ignoreZero: [boolean]** this enable or disable the wisard to read the address zero in each RAM.
- **completeAddressing: [boolean]** this enable or disable the automatic complete of addressing in the case when the size of entry is not divisible by address size, this create redundant information, but address all indexes of entry.

- **indexes: [list(int)]** this is to use a specific addressing of entry to the discriminators, all discriminators wiil use this addressing.
- **base: [int]** this is the base of addressing, by default is binary addressing.


### type 2
```python
jsonConfig = wsd.json()
wsd2 = Wisard(jsonConfig)
```
The wisard can be saved with json or jsonConfig methods and reloaded later with this value.

## methods:

### train
This method train with the data passed to it.
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
# create a DataSet object
ds = DataSet(X, y)
wsd.train(ds)
```
### classify
This method classify the data passed to it, based on what it learn.
```python

# load input data, just zeros and ones  
X = [
      [1,1,1,0,0,0,0,0],
      [1,1,1,1,0,0,0,0],
      [0,0,0,0,1,1,1,1],
      [0,0,0,0,0,1,1,1]
    ]

ds = DataSet(X)

# the output is a list of string, this represent the classes attributed to each input
out = wsd.classify(ds)

for oneout in out:
    print(oneout)

# if its just an single input
x = [1,1,1,0,0,0,0,0]

bin = BinInput(x)

# the output is a single string
out_ = wsd.classify(bin)

print(out_)

```
- **X: [list(list(int))]** This is the list of inputs to be classified.

### getMentalImages
This one show the pattern learned by the model, it return a dictionary where the key is of type string and it is the class and value is the list of integer representing the learned pattern.
```python
patterns = wsd.getMentalImages()

for key in patterns:
    print(key, patterns[key])

```

### untrain
This will untrain an input trained before or a list of inputs trained before.
```python
x = BinInput([1,1,1,0,0,0,0,0])

ds = DataSet([x], ["cold"])
wsd.untrain(ds)

X = [
   [1,1,1,0,0,0,0,0],
   [0,0,0,0,1,1,1,1],
]
y = [
   "cold",
   "hot"
]

ds = DataSet(X,y)
wsd.untrain(ds)
```

### json
This return the configuration and ram values as JSON format converted to string.
```python
print("Wisard: ", wsd.json())
# or pass true as parameter to save ram data in files (this is useful for huge rams)
print("Wisard: ", wsd.json(True,"path/to/save/data"))
```
### rank
Returns a class rank based on the discriminators votes to an input or a list of inputs.

```python
x = [1,1,1,0,0,0,0,0]

bin = BinInput(x)

# the output is a list of strings with the discriminators votes ordered.
rank = wsd.rank(bin)

print(rank)

################
X = [
      [1,1,1,0,0,0,0,0],
      [1,1,1,1,0,0,0,0],
      [0,0,0,0,1,1,1,1],
      [0,0,0,0,0,1,1,1]
]

ds = DataSet(X)
out = wsd.rank(ds)


for r in ranks:
    print(r, ranks[r])

```
### getsizeof
This returns the model size.
```python
print("Model size: ", wsd.getsizeof())
```
### getTupleSizes
Returns the size of each discriminator.
```python
for r in wsd.getTupleSizes():
    print("Discriminator size", r)

```

