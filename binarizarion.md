# SimpleThermometer
## constructors:
```python
thermometerSize=4
minimum=0.0
maximum=10.0

ther = SimpleThermometer(
   thermometerSize,          # required
   minimum,                  # required
   maximum,                  # required
)
```
The default value for the optional parameters are showing in the example above.
- **thermometerSize: [int]** number of divisions for the thermometer scale.
- **minimum: [double]** minimum value for the interval.
- **maximum: [double]** maximum value for the interval.

## methods:
### getSize
This method returns the number of divisions the thermometer has.
```python
ther_size = ther.getSize()
```
### transform
This method binarizes the input data. It returns a BinInput object with all the encoded data together in a single array. 
```python

# load input data, set of numbers in the interval [0, 10] 
X = [
     1.0, 3.0, 4.5, 6.0, 7.2 
    ]

X_bin = ther.transform(X)

# printing the BinInput
print(X_bin.list())
```
For this example, the output should look like this.
```python
[1, 0, 0, 0, 1, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 1, 1, 0]
```
It's important to separate them if needed.
```python
# using the numpy library to reshape the array
# reshaping to [5, 4]

import numpy as np # importing the library

X_bin_list = np.array(X_bin.list()) # getting the array list
num = len(X)                        # number of inputs
ther_size = int(ther.getSize())     # divisions 4
X_reshaped = X_bin_list.reshape(num, ther_size) 
```
The output of X_reshaped:
```python
array([[1, 0, 0, 0],
       [1, 1, 0, 0],
       [1, 1, 0, 0],
       [1, 1, 1, 0],
       [1, 1, 1, 0]])
```
