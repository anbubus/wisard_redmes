# BinInput
The main purposeof this class is to store and manipulate **binary values** efficiently.  
## constructors:
```python
bin = BinInput()             # initializes as an empty bin object
bin1 = BinInput(size = 4)    # initializes as an empty bin object with a especifc size
bin2 = BinInput([1,0,0,1,1]) # initializes with a short vector of 0 and 1
```
## methods:
### get
Reads a single bit at the given **index**.
```python
bin_index = bin.get(index)
```
### list
This method returns all stored bits as a short vector.
```python
out = bin2.list()
print(out)
```
For this example, the output should look like this.
```python
[1,0,0,1,1]
```
### set
Modifies a specific bit at index, setting it to 1 or 0.
```python
bin2.set(2, 1)

out = bin2.list()
print(out)
```
The new bin value.
```python
[1,1,0,1,1]
```
### size
Returns the number of stored bits.
```python
bin2.size() # returns 5
```
### data
This method encodes the bits into a Base64 string.
### extend
Allows concatenating two **BinInput** objects, or when receiving a short vector it's appends the values to the current object.
### setConfig
Adjust the number of bytes required to store **size** bits.
