Here is an overview of some of my preliminary results (I used github as Notion is not working currently)

I used Radiation data for now, but will try the same evaluation using transmissivity in a next step

# 1) Fitting curve to Radiation data only:

### One-day evolution of radiation
I used NN and each input consists of the radiation evolution of one day (trying to capture the average shape of the curve)

![mlp_1dayevol](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/f7d38a67-62d7-4f57-8ab9-99e420b07ea1)

-> standard evolution over one day does not capture fluctuations -> no good fit

### Periodic spline interpolation on radiation evolution

![periodicSpline](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/43543510-09e8-4e72-b05c-965c20dce013)

## Conclusion:
- we need additional features to capture fluctuations
- Remark: cannot fit continuous fucntion due to split in data (no data between 5pm-6am)


# 2) Using standard NN - (Multi-layer-perceptron)

## Started with 10x10 cod images - MLP
I started by using the 10x10 cod input data. Then I added the time information (day and time) as a first step and in a second step the sun position (altitude and azimuth -> see 'Information'-page) as input features.
I used hyperparametertuning to find the best MLP architecture up to 3 layers (!!! no improvement with further increase of layers)

Mean squared error are:
10 x 10 (hyperparameter tuning)	
- 0.474963 cod and sun postion,
- 0.571241	 cod and time index
- 0.887235 cod only


Random Hyperparametertuning - variation of the following parameters:
- 'max_iter': [500, 1000], 
- "hidden_layer_sizes" : [(20,),(50,), (100,),(20,20,), (50,50,), (100,100,), (20,20,20,),  (50,50,50,), (100,100,100,)],
- 'learning_rate_init' : [0.01, 0.005, 0.001, 0.0005, 0.0001],
- 'activation' : ['identity', 'logistic', 'tanh', 'relu'],
- 'solver' : ['sgd', 'adam']

The results show the MSE on the test data.
![Results_MLP_10_cod](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/ecebfd18-f57a-4c8e-b866-0a9dbae77fb1)
![Results_MLP_10_timeind](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/1082743c-8504-450f-9e80-eeb370967cd3)
![Results_MLP_10_sunpos](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/21d223ff-1031-4dc4-944d-f0118986cad8)

(Training with Sklearn)



###  MLP with 1 layer & 1 hidden feature for the 64x64 data

I used the 64x64 cod input data. Then I added the time information (day and time) as a first step and in a second step the sun position (altitude and azimuth -> see 'Information'-page) as input features.
Each model is trained with 1 hidden layer consisting of 1 hidden feature and a ReLu activation function.

Mean squared error are:
(64x64 1 layer with 1 hidden node)	
- 0.443 cod and sun postion,
- 0.785	 cod and time index
- 0.824 cod only



Results show MSE on the test data:

![mlp_64_codonly_1layer](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/75b88c99-4985-4004-9ad0-287ac1e87e6a)
![mlp_64_time_1layer](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/9b843897-2dea-4cf5-8743-9240aaf1e9cb)
![mlp_64_sun_1layer](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/992e8940-c6f0-4908-a357-117ec43f575b)


### MLP tuning on 64x64 data with sun position as additional input

I used the 64x64 cod and sun position (altitude and azimuth -> see 'Information'-page) as input features.


Manual evaluation of hyperparameters shows: 



![mlp_64_cod_50](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/ca5f6597-3988-4d36-9e3e-38fcebffaebd)
![mlp_64_cod_100](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/74dede5f-3528-476d-a491-d1984d4ddf7f)
![mlp_64_cod_50,50](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/5d964457-ebf1-4376-8ac7-193aced97f4c)

![mlp_64_cod_10,10,10](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/fbe8ce53-3d29-4759-801f-8f72c7130a84)


##### -> As training fails to converge and jumps around minima, I decreased the learning rate (from 0.001 to 0.0001) to get smoother curve:

![mlp_64_cod_50,50,50](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/3ef8ef2e-e3d9-4127-b152-a0b5019b5e24)

![mlp_64_cod_100,100,100](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/9e7caee7-2409-4dce-9bf7-f267b584e69d)

##### -> Using tanh-activation function did not lead to an improvement:

![mlp_64_cod_100,100,100_tanh](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/83dcee2d-6ee7-4f42-8e8d-3b8796555477)


##### -> Using a MLP with 3 layers, each 100 hidden features -> seem to work better, but still bad fit:

![mlp_64_sun_100-100-100](https://github.com/SimoneMarlenHorstmann/HypProject/assets/160620548/ead6708e-46c7-417c-ba27-dcdf051f9347)

## Conclusion:
- using 64x64 data seems to work better
- including sun position seems to improve prediction
- MLP does not capture data

# 3) Using Convolutional neural network (CNN)
-- in progess: so far no comparable results (mse way higher than for NN) --
