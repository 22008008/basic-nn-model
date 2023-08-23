# Developing a Neural Network Regression Model

## AIM

To develop a neural network regression model for the given dataset.

## THEORY

A neural network with multiple hidden layers and multiple nodes in each hidden layer is known as a deep learning system or a deep neural network. Here the basic neural network model has been created with one input layer, one hidden layer and one output layer.The number of neurons(UNITS) in each layer varies the 1st input layer has 16 units and hidden layer has 8 units and output layer has one unit.

In this basic NN Model, we have used "relu" activation function in input and hidden layer, relu(RECTIFIED LINEAR UNIT) Activation function is a piece-wise linear function that will output the input directly if it is positive and zero if it is negative.

## Neural Network 

 <img width="442" alt="nn (2)" src="https://github.com/22008008/basic-nn-model/assets/118343520/9c2433a0-a5f0-4f17-b71c-f10fe19d736f">

## DESIGN STEPS

### STEP 1:

Loading the dataset

### STEP 2:

Split the dataset into training and testing

### STEP 3:

Create MinMaxScalar objects ,fit the model and transform the data.

### STEP 4:

Build the Neural Network Model and compile the model.

### STEP 5:

Train the model with the training data.

### STEP 6:

Plot the performance plot

### STEP 7:

Evaluate the model with the testing data.

## PROGRAM

```
DEVELOPED BY: SRI RANJANI PRIYA.P
REF NO:212222220049
```

### Importing Required Packages :
```
from google.colab import auth
import gspread
from google.auth import default
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
```

### Authentication and Creating DataFrame From DataSheet :
```
auth.authenticate_user()
creds, _ = default()
gc = gspread.authorize(creds)
worksheet = gc.open('ex1').sheet1
rows = worksheet.get_all_values()
df = pd.DataFrame(rows[1:], columns=rows[0])
df = df.astype({'INPUT':'float'})
df = df.astype({'OUTPUT':'float'})
df
```

### Assigning X and Y values :
```
X = df[['INPUT']].values
Y = df[['OUTPUT']].values
```

### Normalizing the data :
```
X_train,X_test,y_train,y_test=train_test_split(X,y,test_size = 0.33,random_state=33)
Scaler = MinMaxScaler()
Scaler.fit(X_train)
X_train1 = Scaler.transform(X_train)
```

### Creating and Training the model :
```
model = Sequential([
    Dense(5,activation = 'relu'),
    Dense(10,activation = 'relu'),
    Dense(1)
])
model.compile(optimizer='rmsprop',loss = 'mse')
model.fit(X_train1,y_train,epochs=2200)
```

### Plot the loss :
```
loss_df = pd.DataFrame(model.history.history)
loss_df.plot()

### Evaluate the Model :
X_test1 = Scaler.transform(X_test)
model.evaluate(X_test1,y_test)
```

### Prediction for a value :
```
X_n1 = [[20]]
X_n1_1 value = Scaler.transform(X_n1)
model.predict(X_n1_1 value)
```


## Dataset Information

![image](https://github.com/22008008/basic-nn-model/assets/118343520/cebcd648-079b-4db2-b3b7-efdcb10b058e)



## OUTPUT

### Training Loss Vs Iteration Plot

![image](https://github.com/22008008/basic-nn-model/assets/118343520/1bd163bb-c7f6-4e20-9364-29afe5ea919f)



### Test Data Root Mean Squared Error

1/1 [==============================] - 0s 265ms/step - loss: 2116.7065

### New Sample Data Prediction
```
1/1 [==============================] - 0s 215ms/step
array([[158.81854]], dtype=float32)
```
## RESULT
```
Thus the neural network regression model for the given dataset is executed successfully.
```
