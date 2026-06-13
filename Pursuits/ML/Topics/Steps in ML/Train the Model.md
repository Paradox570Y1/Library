### Splitting the Dataset
- You need to randomly split the dataset to keep some of the data hidden from training. This enables you later evaluate your model with the data before it is put into production.
- Majority will be held in _training dataset_. Training dataset is the data that will be used when your model is training. General rule of thumb is around 80% of your data.
- Then we have _test dataset_ which is the data that model hasn't seen during training. It's used during the model evaluation state. It helps you see how well your model will generalize to new data.

### Model Training
- The model training algorithm iteratively updates [[model parameters]] to minimize some loss function.
- Nearly all models are trained by a slowly changing model parameters to move the model closer and closer to achieving some goal.
- A **loss function** is used to codify the model’s distance from a goal. For example, if you were trying to predict the number of snow cone sales based on the day’s weather, you would care about making predictions that are as accurate as possible. So you might define a loss function to be “the average distance between your model’s predicted number of snow cone sales and the correct number.” You can see in the snow cone example; this is the difference between the two purple dots.
#### More Details about Training a Model
- Unless you are developing brand new models or algorithm, you will likely use one of many machine learning frameworks, which already have these implemented for you. Determining which model to use ,a process known as model selection is not a perfect science. 
- The list of established model is constantly growing and even seasoned machine learning practitioners will try many different types of models while solving problem with ML.
- _Hyperparameters_ are settings on the model that are not changed during model training. These settings can affect how quickly or how reliably the model trains, such as the number of clusters the model should identify.
- Be prepared to iterate
- Pragmatic problem-solving with ML is really an exact science.
##### Putting it all together
The end-to-end training process is:

- Feed the training data into the model.
- Compute the loss function on the results.
- Update the model parameters in a direction that reduces loss.
![[Pasted image 20240710095632.png|600]]
#### [[More about Models]]