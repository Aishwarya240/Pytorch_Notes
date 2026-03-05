- Now we know how to create tensor in PyTorch.
-  Next we will be loading datasets and converting those raw data into PyTorch tensors.
- We will be using datasets from Scikit-Learn and Kaggle datasets.
---
#  Loading and using Scikit-Learn toy datasets

- We will be loading Scikit-Learn iris dataset and convert those numpy array data into tensors
>[!Important]
>The PyTorch models only works with the dataset which are in tensor data type format. Sp this is the reason we cant use raw datasets.

---
# Loading and using Scikit-Learn toy datasets

- We will be loading Scikit- Learn iris dataset and convert those numpy array data into tensors.
-  First lets load our iris toy dataset
```python
from sklearn.datasets import load_iris

data = load_iris()

print(data)
```
- Here iris data is a dictionary where dataset components are stored in key and value pair.
- We can see the key values using this code
```python
data.keys()

# Output
# dict_keys(['data', 'target', 'frame', 'target_names', 'DESCR', 'feature_names', 'filename', 'data_module'])
```

- About dataset
	- The data for our model which is also known as input features are stored in `data` key and the values are in array format.
	- The target which is also known as output features are stored in the `target` key and it is also in array format.
	- Further more we will be storing these `data` and `target` in two variables known as `X` and `y` variables, where `X` is input features for out model and `y` is the output features of our model.
- Now lets create these two variables.	
```python
X = data["data"]
y = data["target"]
```

- Lets see the shape, size, and data type of the `X` and `y` variables.
```python
X.shape, X.size, X.dtype, type(X)
```

```python
y.shape, y.size, y.dtype, type(y)
```
- We can see these are numpy array data type.
-  Now lets convert these to PyTorch tensors.
```python
X = torch.tensor(X, dtype=torch.float16, device=torch.device("cpu")
y = torch.tensor(y, dtype=torch.float16, device=torch.device("cpu"))
```

>[!Note]
> - Here we used `dtype` parameter to set the data type for this tensor as `float16` as we know `float16` data type will take less space compared to other float values.
> - Further we set `device` as `cpu`, so these tensors will be created on CPU. You can change the device type as GPU by setting device as `cuda` or `mps`

- Lets print the data types of updated input features which is `X` and updated output features which is `y`.
```python
type(X), type(y), X.dtype, y.dtype
```
- This will print data type as tensors.
----
#  Train test split our data 
- After converting these raw data to tensor we can now split our data into two sub categories which are known to be training data and testing data .
- Scikit- Learn already provides a method `train_test_split` which splits our `X` and `y` data.
>[!Note]
>- We will be splitting our training and testing data as 80, 20 ration where 80% data will be fro training and 20% will be used for testing most commonly for evaluation process of model.
>- You can change this ratio based on your needs.

- Lets load `train_test_split` method from Scikit-Learn
```python
from sklearn.model_selection import train_test_split
```
- Now create four variables, `X_train`, `X_test`, `y_train`, and `y_test` which will be storing our train test split data for our `X` and `y` variables.
```python 
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

>[!Note]
>- Here `test_size=0.2` means 20% for testing purpose and rest remaining 80% will be used as training data for our model.

- Lets check the shape of our created train test split variables.
```python
X_train.shape, X_test.shape, y_train.shape, y_test.shape
```
- We can now give this data to the model.
---

#  Working with the Kaggle dataset

- In this section we will be working with a real dataset provided by kaggle.
- [kaggle](https://www.kaggle.com/)is one of the leading open-source dataset provide. Here you can download and use free datasets contributed by other fellows. It also proved you executable python code notebooks similar to jupyter notebook, where every thing is managed by kaggle. You can use CPU and GPU based on your requirements.
- Lets load one of the classification dataset. The dataset we will be using is [Heart Failure Prediction Dataset](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction)
- Lets download a csv file for this dataset.
- Now lets load this dataset using pandas.
```python
import pandas AS PD

data = pd.read_csv("<path-to-your-dataset>/heart.csv")

data.head() # checks first 5 data points
```
- To get more information about this loaded data we use `.info()` method provided by pandas.
```python
data.info()
```

```Text
<class 'pandas.DataFrame'>
RangeIndex: 918 entries, 0 to 917
Data columns (total 11 columns):
 #   Column          Non-Null Count  Dtype  
---  ------          --------------  -----  
 0   Age             918 non-null    int64  
 1   Sex             918 non-null    int64  
 2   ChestPainType   918 non-null    int64  
 3   RestingBP       918 non-null    int64  
 4   Cholesterol     918 non-null    int64  
 5   FastingBS       918 non-null    int64  
 6   RestingECG      918 non-null    int64  
 7   MaxHR           918 non-null    int64  
 8   ExerciseAngina  918 non-null    int64  
 9   Oldpeak         918 non-null    float64
 10  ST_Slope        918 non-null    int64  
dtypes: float64(1), int64(10)
memory usage: 79.0 KB
```
- Now we can convert our `X` input data and `y` output data into PyTorch tensors.
```Python
# pandas DataFrame (numpy_arrays) to torch tensors  
X_tensors = torch.from_numpy(X.values).to(device="mps", dtype=torch.float16)  
type(X_tensors)
```
```Python
y_tensors = torch.tensor(y).to(device="mps", dtype=torch.float16)  
type(y_tensors)
```
- We have successfully converted our data into tensor format. Now we can split our data into training and testing data.
```Python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X_tensors, y_tensors, test_size=0.2, random_state=42) # test data is 20% and train data is 80%

X_train.shape, X_test.shape, y_train.shape, y_test.shape
```
---

