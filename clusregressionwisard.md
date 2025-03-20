# ClusRegressionWisard
## constructor:
```python
from wisardpkg import RegressionWisard

crew = ClusRegressionWisard(
addressSize=3            # required
minScore,                # optional
threshold,               # optional
discriminatorsLimit,     # optional
completeAddressing=True  # optional
orderedMapping=False     # optional
mean=Mean                # optional
minZero=0                # optional
minOne=0                 # optional
steps=0                  # optional
numberOfTrainings=0      # optional
)
```
The default value for the optional parameters are showing in the example above.
- **addressSize: [int]** is the size of addressing RAM.
- **minScore: [float]** is the minimum score accept by clusregressionwisard to choose to create a rew. Must be between 0 and 1.
- **threshold: [int]** is the limit of examples learned by a rew.
- **limit: [int]** is the limit of rews by cluster in supervised and semi-supervised learning.
- **completeAddressing: [boolean]** this enable or disable the automatic complete of addressing in the case when the size of entry is not divisible by address size, this create redundant information, but address all indexes of entry.
- **orderedMapping: [boolean]** Indicates whether the RAM mapping should be used.
- **minOne: [int]** Minimun number of ones bits allowed in an address.
- **minZero: [int]** Minimun number of zeros bits allowed in an address.
- **steps: [int]** Number of additional training steps for fine-tuning predictions.
- **numberOfTrainings: [int]** Keeps track of the number of training iterations.
- **mean: [Mean Object]** A helper object used to compute the final prediction from RAM outputs.

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

# load the y data
y = [
      1.3,
      2.0,
      3.0,
      1.1
    ]
# create a DataSet object
ds = DataSet(X, y)
crew.train(ds)
```
### predict
Predicts the outputs for a dataset.
```python
# load input data, just zeros and ones  
X = [
      [1,1,1,0,0,0,0,0],
      [1,1,1,1,0,0,0,0],
      [0,0,0,0,1,1,1,1],
      [0,0,0,0,0,1,1,1]
    ]

ds = DataSet(X)

# the output is a list of predicted y values
predicted = crew.predict(ds)
```
### getsizeof
This returns the model size.
```python
print(crew.getsizeof())
```
### json
This return the configuration and ram values as JSON format converted to string.
This return the configuration and ram values as JSON format converted to string.
```python
print("ClusRegressionWisard: ", crew.json())
# or pass true as parameter to save ram data in files (this is useful for huge rams)
print("ClusRegressionWisard: ", crew.json("path/to/save/data"))
```
### setMeanFunc
Updates the mean computation method used in predictions.
