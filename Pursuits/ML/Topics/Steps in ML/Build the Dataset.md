The next step in the machine learning process is to build a dataset that can be used to solve your machine learning-based problem. Understanding the data needed helps you select better models and algorithms so you can build more effective solutions.

> [[Forbes Survey of 2016]]

### Working With Data
Understanding the data we are working with ,really understanding it, helps us select better models and algorithms that ultimately enables us to have more effective Machine Learning solution.
- Good, high-quality data is essential for any kind of machine learning project.
#### Four Ways to break down the data portion of the ML Workflow
![[Pasted image 20240702102140.png|500]]

##### Data Collection
- First Step is to gather the data relevant to your problem.
  ![[Pasted image 20240702102308.png|400]]
Data collection can be as straightforward as running the appropriate SQL queries or as complicated as building custom web scraper applications to collect data for your project. You might even have to run a model over your data to generate needed labels. Here is the fundamental question:  
   - Does the data you've collected match the machine learning task and problem you have defined?

##### Data inspection
- Now that we have the data, it's essential to inspect the [[integrity]] of the data.
- Don't assume the any data you find is of high quality.
- The quality of data will ultimately have a massive impact on how well your model can perform.
- Explore your data outside the norms.
- Check if you're missing some data or has incomplete data
- Transform the data into the form the model requires.
  ![[Pasted image 20240702103515.png|400]]


##### Summary Statistics
- Models can make assumptions about how your data is structured.
- Now that you have some data in hand, it is a good best practice to check that your data is in line with the underlying assumptions of the machine learning model that you chose.
- Summary Statistics allows you to see trends in data , which can help you better understand what the data is communicating.
- There are many statistical tools that you can use to calculate things like mean, interquartile range(IQR) and standard deviation. 
- These tools can give you insight into the scope, scale and shape of the dataset.
- You might also detect [[outliers]] that you might have missed during other method.
  ![[Pasted image 20240702104436.png|400]]
  
##### Data visualization
- You can use data visualization to see outliers and trends in your data and to help stakeholders understand your data.
- Look at the following two graphs. In the first graph, some data seems to have clustered into different groups. In the graph immediately preceding it, some data points might be outliers.
  ![[Pasted image 20240702104551.png|400]]
![[Pasted image 20240702104746.png|600]]

  
