
# Step 1: Defining the problem

Imagine you run a company that offers specialized on-site janitorial services. One client - an industrial chemical plant - requires a fast response for spills and other health hazards. You realize if you could _automatically_ detect spills using the plant's surveillance system, you could mobilize your janitorial team faster.  
  
Machine learning could be a valuable tool to solve this problem.

![spills](https://student.deepracer.com/static/media/spills.b9ee8efe365581a2dd2b.png)

### Choosing a model

As shown in the image above, your goal will be to predict if each image belongs to one of the following classes:

- Contains spill
- Does not contain spill

![superclass|400](https://student.deepracer.com/static/media/superclass.305479fcf7d8dcd31a71.png)

# Step 2: Building a dataset

### Collecting

- Using historical data, as well as safely staged spills, quickly build a collection of images that contain both spills and non-spills in multiple lighting conditions and environments.

### Exploring and cleaning

- Go through all of the photos to ensure that the spill is clearly in the shot. There are Python tools and other techniques available to improve image quality, which you can use later if you determine that you need to iterate.

### Data vectorization (converting to numbers)

- Many models require numerical data, so you must transform all of your image data needs to be transformed into a numerical format. Python tools can help you do this automatically.
- In the following image, you can see how each pixel in the image immediately below can be represented in the image beneath it using a number between 0 and 1, with 0 being completely black and 1 being completely white.

![black-spill](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAALMAAACPCAIAAAA+zn1yAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAALEoAACxKAXd6dE0AAASRSURBVHhe7dLRcqQwDETR/P9PZ2tTN1XJrmEwSBoL7nmcMchq+uNTGrEZd/OxjRPH2Iy7oQUjnDjGZtwEH/8s3vKDzeiND3sZr/vBZvTDx4zG27/ZjGb4jDmY8cVmLITv81Zc5TnNYO9JPByBNy6P6z6hGWx8Ga+bxMN9cO97N4Nd8zHvG7/2xA43bgaLahLx3bIZrKhTCPFmzWA5XUCUt2kGa+kyArUZ+geB3qMZ7KQIZGoz9A8y7dsM9lA08m3aDJZQAiK2GU9AapP6NYN1dQypzbMZt0VeZzVrBktrAzFF6NQMttcGYgrSphlsrw3EFMdm3AQxxenRDLbXNpKK06AZrK5tJBXKZtwBSYVavRmsrl2EFWrpZrC3tpFUApvRG0klWLcZrK5dhJXAZvRGWAkWbQZ76xXySmAzeiOvBCs2g6V1AJElWK4ZbKxjSC2BzeiN1BKs1QzW1WEEl8Bm9EZwCRZqBrtqBtklsBm9kV2CVZrBoppEfAmWaAZbah4JJrAZvZFggvc3gxV1CiEmeHMz2E9nkWOC9zSDtXQZgSZ4QzPYSRHINEF1M1hIQYg1gc3ojVgTlDaDbRSHZBPYjN5INkFdM1hFoQg3QVEz2EOhCDdHRTPYQ2eRY630qSynC4iyls1ogChr2YwGiLJW7lQ20zWkWctmNECatRKnspYuI9BaNqMBAq1lMxog0FpZU9lJEci0ls1ogExrpUxlIUUg03I2Y3VkWi5+MAspCLGWsxmrI9ZywYPZRnFItlzkYFZRKMItFzaYPRSNfMvFDGYJJSDicgGD2UA5SLnc1cFcX5nIupbNaICsa12aysWVjLhrnZ/KrZWPxGvZjAZIvNbJqVxZJQi91pmp3FeFiL6QzeiB6AtNj+SmKscHqDI3jzvqHfgGVWxGJ3yGEjajGb5EvolJXE3vxvdIZjO64qukOTqA62glfJscNqM3Pk+CQ6/mFvqNdL7xay1mJ3j9aq6gH4jmN/4rx/hoNmMaufyHv8sxPprNmEMoI5wox/hoNmMOoYxwohzjo9mMCSSygUPlGB/NZhxFHNs4V47x0WzGIWTxCqdrMTuazTiELI7hmSpMjWYzXiOIw3isClOjvXgvwx+MICbxcAlGRrMZe0jhLN6SjGHRbMYmIriGd2ViUrS99zL5kYjgMl6XiUnRbMYA+wfhpWkYE81m/MLmCRiQgAHRbAbYuQpTI/DGaDbjLxYux/hreFe0pzeDVdfAnSbxcLTnNoMl18P9DuOxaM9qBoutjbsexmPRHtQMtuqAGx/DM9Fsxrq49y6OJrAZ6+LeuziaYPPVTL4LtmqFq+/iaAKbsS6uvoujCWzGurj6Ns7lGLydsTfCYt1w+22cy2Ez1sXtN3AoTddmcNdbY9UNHEoT3wzektwwZtwaq45wIlNMM3jyN/5LwABlCmgGj/2Hv1/h9Bd+2sVRJbvUDB7YwKFdHP3Gr7s4qmQnm8HRaLx9G+eU70wzOJeAARs4pBJzzeCEHsCPrTGboTGboTGboTGboTGboTGboTGboTGboTGboTGboTGboTGboZHPzz/fAad5DYbKqAAAAABJRU5ErkJggg==)

![spill numbers|300](https://student.deepracer.com/static/media/spillnumbers.0b8e60a881ff5bc0ad27.png)

**Split the data**

- Split your image data into a training dataset and a test dataset.

# Step 3: Model Training

Traditionally, solving this problem would require hand-engineering features on top of the underlying pixels (for example, locations of prominent edges and corners in the image), and then training a model on these features.  
Today, deep neural networks are the most common tool used for solving this kind of problem. Many deep neural network models are structured to learn the features on top of the underlying pixels so you don’t have to learn them. You’ll have a chance to take a deeper look at this in the next lesson, so we’ll keep things high-level for now.

### CNN (convolutional neural network)

Neural networks are beyond the scope of this lesson, but you can think of them as a collection of very simple models connected together. These simple models are called _neurons_, and the connections between these models are trainable model parameters called _weights_.  
Convolutional neural networks are a special type of neural network that is particularly good at processing images.

# Step 4: Model evaluation

As you saw in the last example, there are many different statistical metrics that you can use to evaluate your model. As you gain more experience in machine learning, you will learn how to research which metrics can help you evaluate your model most effectively. Here's a list of common metrics:

- Accuracy
- Confusion matrix
- F1 score
- False positive rate
- False negative rate
- Log loss
- Negative predictive value
- Precession
- Recall
- ROC Curve
- Specificity

In cases such as this, accuracy might not be the best evaluation mechanism.  
  
**Why not?** The model will see the _does not contain spill'_ class almost all the time, so any model that just predicts _no spill_ most of the time will seem pretty accurate.

What you really care about is an evaluation tool that rarely misses a real spill.  
  
After doing some internet sleuthing, you realize this is a common problem and that _precision_ and _recall_ will be effective. Think of _precision_ as answering the question, "Of all predictions of a spill, how many were right?" and _recall_ as answering the question, "Of all actual spills, how many did we detect?"

Manual evaluation plays an important role. If you are unsure if your staged spills are sufficiently realistic compared to actual spills, you can get a better sense how well your model performs with actual spills by finding additional examples from historical records. This allows you to confirm that your model is performing satisfactorily.

# Step 5: Model inference

The model can be deployed on a system that enables you to run machine learning workloads such as AWS Panorama.  
  
Thankfully, most of the time, the results will be from the class _does not contain spill_.

![no spilled|400](https://student.deepracer.com/static/media/nospilled.746294f55fdcebac58b8.png)

But, when the class _contains spill'_ is detected, a simple paging system could alert the team to respond.

![spilled|400](https://student.deepracer.com/static/media/spilled.4486f1276e050ffb9797.png)


# Wrap-up

In this example, you saw how you can use machine learning to help detect spills in a work environment. This example also used a modern machine learning technique called a convolutional neural network (CNN).  
  
Here is summary of key moments from the lesson that you just finished.

**One**  
For some applications of machine learning, you need to use more complicated techniques to solve the problem. While modern neural networks are a powerful tool, don’t forget their cost in terms of being easily explained.  
  
**Two**  
High quality data once again was very important to the success of this application, to the point where even staging some fake data was required. Once again, the process of data vectorization was required so it was important to convert the images into numbers so that they could be used by the neural network.  
  
**Three**  
During model inference you continued to inspect the predictions for accuracy. It is especially important in this case because you created some fake data to use when training your model.

### Terminology

**Neural networks:** a collection of very simple models connected together.

- These simple models are called **neurons**.
- The connections between these models are trainable model parameters called **weights**.

**Convolutional neural networks(CNN)**: a special type of neural network particularly good at processing images.