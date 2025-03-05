# DynamicThermometer
## constructors:
```python
thermometerSizes = [,]
minimum = [,]
maximum = [,]

dy = DynamicThermometer(
   thermometerSizes,          # required
   minimum,                  # required
   maximum,                  # required
)
```
The default value for the optional parameters are showing in the example above.
- **thermometerSize: [int]** list of numbers of divisions for each thermometer scale.
- **minimum: [double]** list of minimum values for each interval.
- **maximum: [double]** list of maximum value for each interval.
All of them needs to be the same size.

## methods:
### getSize
This method returns the number of divisions the thermometer has.
```python
dy_size = dy.getSize()
```
### transform
This method binarizes each input data following the set of thermometers. It returns a BinInput object with all the encoded data together in a single array. 
```python
thermometerSizes = [4, 10]
minimum = [0.0, 10.0]
maximum = [10.0, 40.0]

di = DynamicThermometer(thermometerSizes=thermometerSizes, minimum=minimum, maximum=maximum)
# load input data, set of numbers in the interval [0, 10]. Same size of the thermometer array.
X = [
     4.0, 27.2 
    ]

X_bin = dy.transform(X)

# printing the BinInput
print(X_bin.list())
```
For this example, the output should look like this.
```python
[1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

# 4.0 -> [1, 1, 0, 0]
# 27.2 -> [1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```
