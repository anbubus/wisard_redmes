# DataSet
This class was desingned to handle different types of datasets, including supervised, unsupervised, and semi-supervised data. 
## constructors:
```python
# for supervided learning
X = [
    [1, 0, 1, 1],
    [0, 0, 0, 1],
]
Y = ["hot", "cold"]

ds = DataSet(X, Y)

# for unsupervised
ds = DataSet(X)
```
## methods:
### add
Add individual or multiple samples (string, BinInput, short vector) with our without labels/Y values.
```python
ds.add([1, 0, 0, 1], "mid")
```
### get
Retrives a data entry.
```python
bin = ds.get(index) # returns a BinInput
```
### getLabel/getY
Retrieves corresponding label or Y value.
```python
ds.getLabel(0) # 'hot'
```
### getLabels/getYs
Returns all stodes labes or Y values.
```python
ds.getLabels() # {1: 'cold', 0: 'hot'}
```
### save
Saves the dataset to a file, encoding labels/Y values in Base64.
```python
f = ds.save("my_dataset") # my_dataset.wpkds
```
### set
Modifies a specific bit at index, setting it to 1 or 0 BinInputs objects.
```python
ds.set(0, BinInput([1,1,1,1]))
```
### size
Returns the number of data stored.
```python
bin2.set(2, 1)

out = bin2.list()
print(out) # [1,1,0,1,1]
```
