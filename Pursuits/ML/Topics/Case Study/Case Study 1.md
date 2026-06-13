__House Price Prediction__

House price prediction is one of the most common examples used to introduce machine learning.  
  
Traditionally, real estate appraisers use many quantifiable details about a home (such as number of rooms, lot size, and year of construction) to help them estimate the value of a house.  
  
You detect this relationship and believe that you could use machine learning to predict home prices.

![House value|400](https://student.deepracer.com/static/media/houseValue.f062a034bc399762b51a.png)

## Step 1: Define the problem

**Problem**  
_Can we estimate the price of a house based on lot size or the number of bedrooms?_

You access the sale prices for recently sold homes or have them appraised. Since you have this data, this is a supervised learning task. You want to predict a continuous numeric value, so this task is also a regression task.

![Labeled data|400](https://student.deepracer.com/static/media/labeledData.19ee4ede4e6f623008a9.png)


## Step 2: Build the dataset

For this project, you need data about home prices, so you do the following tasks:

- **Data collection**: You collect numerous examples of homes sold in your neighborhood within the past year, and pay a real estate appraiser to appraise the homes whose selling price is not known.
- **Data exploration**: You confirm that all of your data is numerical because most machine learning models operate on sequences of numbers. If there is textual data, you need to transform it into numbers. You'll see this in the next example.
- **Data cleaning**: Look for things such as missing information or outliers, such as the 10-room mansion. You can use several techniques to handle outliers, but you can also just remove them from your dataset.

![Data table|400](https://student.deepracer.com/static/media/datatable.34e7f293467d090db67e.png)

You also want to look for trends in your data, so you use **data visualization** to help you find them.  
  
You can plot home values against each of your input variables to look for trends in your data. In the following chart, you see that when lot size increases, house value increases.

![Lot size|200](https://student.deepracer.com/static/media/lotSize.b231d1f1e94072670780.png)


## Step 3: Model training

Prior to actually training your model, you need to split your data. The standard practice is to put 80% of your dataset into a training dataset and 20% into a test dataset.

### Linear model selection
As you see in the preceding chart, when lot size increases, home values increase too. This relationship is simple enough that a linear model can be used to represent this relationship.  
A linear model across a single input variable can be represented as a line. It becomes a plane for two variables, and then a hyperplane for more than two variables. The intuition, as a line with a constant slope, doesn't change.

### Using a Python library
[The Python _scikit-learn_ library](https://scikit-learn.org/stable)  has tools that can handle the implementation of the model training algorithm for you.


## Step 4: Model evaluation

One of the most common evaluation metrics in a regression scenario is called _root mean square_ or _RMS_. The math is beyond the scope of this lesson, but RMS can be thought of roughly as the __"average error"__ across your test dataset, so you want this value to be low.

![RMS](https://student.deepracer.com/static/media/rms.7b9e4450494798d38600.png)

In the following chart, you can see where the data points are in relation to the blue line. You want the data points to be as close to the "average" line as possible, which would mean less net error.  
  
You compute the root mean square between your model’s prediction for a data point in your test dataset and the true value from your data. This actual calculation is beyond the scope of this lesson, but it's good to understand the process at a high level.

![RMS chart|300](https://student.deepracer.com/static/media/rmsChart.dffe228182776a085463.png)


### Interpreting Results
In general, as your model improves, you see a better RMS result. You may still not be confident about whether the specific value you’ve computed is good or bad.  
  
Many machine learning engineers manually count how many predictions were off by a threshold (for example, $50,000 in this house pricing problem) to help determine and verify the model's accuracy.
## Step 5: Model inference
Now you are ready to put your model into action. As you can see in the following image, this means seeing how well it predicts with new data not seen during model training.

![inference 1](https://student.deepracer.com/static/media/inf1.3f8cb93f954f23c5e66b.png)

In this example, you saw how you can use machine learning to help predict home prices.  
  
**One**  
Solving problems using machine learning is an evolving and iterative process.  
**Two**  
To solve a problem successfully in machine learning, finding high quality data is essential.  
**Three**  
To evaluate models, you often use statistical metrics. The metrics you choose are tailored to a specific use case.  
  
**Terminology**

- **Regression:** A common task in supervised machine learning used to understand the relationship between multiple variables from a dataset.
- **Continuous:** Floating-point values with an infinite range of possible values. This is the opposite of categorical or discrete values, which take on a limited number of possible values.
- **Hyperplane:** A mathematical term for a surface that contains more than two planes
- **Plane:** A mathematical term for a flat surface (like a piece of paper) on which two points can be joined by drawing a straight line.