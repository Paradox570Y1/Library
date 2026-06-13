## Step 1: Define the problem

_Is it possible to find clusters of similar books based on the presence of common words in the book descriptions?_

![Books](https://student.deepracer.com/static/media/books.41b6c9f2c9b8bbc79953.png)

You do editorial work for a book recommendation company, and you want to write an article on the largest book trends of the year. You believe that a trend called "micro-genres" exists, and you have confidence that you can use the book description text to identify these micro-genres.  
  
By using an unsupervised machine learning technique called _clustering_, you can test your hypothesis that the book description text can be used to identify these "hidden" micro-genres.

### Identify the machine learning task you could use
By using an unsupervised machine learning technique called clustering, you can test your hypothesis that the book description text can be used to identify these "hidden" micro-genres.  
  
Earlier in this lesson, you were introduced to the idea of unsupervised learning. This machine learning task is especially useful when your data is not labeled.

![Unsupervised cluster|300](https://student.deepracer.com/static/media/unsuperclust.c6b5e1c6c880842f477f.png)


## Step 2: Build your dataset

To test the hypothesis, you gather book description text for 800 romance books published in the current year. You plan to use this text as your dataset.

### Data exploration, cleaning, and preprocessing
In the lesson about building your dataset, you learned about how sometimes it is necessary to change the format of the data that you want to use. In this case study, we need use a process called _vectorization_. __Vectorization is a process whereby words are converted into numbers.__

**Data cleaning and exploration**  
For this project, you believe capitalization and verb tense will not matter, and therefore you remove capitals and convert all verbs to the same tense using a Python library built for processing human language. You also remove punctuation and words you don’t think have useful meaning, like _'a'_ and _'the'_. The machine learning community refers to these words as __stop words__.  
  
**Data preprocessing**  
Before you can train the model, you need to do a type of data preprocessing called _data vectorization_, which is used to convert text into numbers.  
As shown in the following image, you transform this book description text into what is called a _bag of words representation_, so that it is understandable by machine learning models.  
  
How the _bag of words representation_ works is beyond the scope of this lesson. If you are interested in learning more, see the **What's next** section at the end of this chapter.

![Bag of words|300](https://student.deepracer.com/static/media/bagOfWords.b044011a6f457c2e1c37.png)


## Step 3: Train the model

Now you are ready to train your model.  
  
You pick a common cluster-finding model called _k-means_. In this model, you can change a model parameter, _k_, to be equal to how many clusters the model will try to find in your dataset.  
  
Your data is unlabeled and you don't how many micro-genres might exist. So, you train your model multiple times using different values for _k_ each time.  
  
What does this even mean? In the following graphs, you can see examples of when _k=2_ and when _k=3_.

![k2b|200](https://student.deepracer.com/static/media/k2b.7f5a0f0cc4ad7b7c877d.png)

During the model evaluation phase, you plan on using a metric to find which value for **k** is the most appropriate.

## Step 4: Model evaluation

In machine learning, numerous statistical metrics or methods are available to evaluate a model. In this use case, the _silhouette coefficient_ is a good choice. This metric describes how well your data was clustered by the model. To find the optimal number of clusters, you plot the silhouette coefficient as shown in the following image below. You find the optimal value is when _k=19._

![k19b](https://student.deepracer.com/static/media/k19b.5c2dead3303db3a07c0d.png)

Often, machine learning practitioners do a manual evaluation of the model's findings.  
  
You find one cluster that contains a large collection of books that you can categorize as "paranormal teen romance." This trend is known in your industry, and therefore you feel somewhat confident in your machine learning approach. You don’t know if every cluster is going to be as cohesive as this, but you decide to use this model to see if you can find anything interesting about which to write an article.

![[Pasted image 20240712101601.png|400]]
## Step 5: Model inference

As you inspect the different clusters found when _k=19_, you find a surprisingly large cluster of books. Here's an example from fictionalized cluster #7.

![silhouette coefficient|400](https://student.deepracer.com/static/media/silhou.a8ac69affee20de38bd5.png)

As you inspect the preceding table, you can see that most of these text snippets indicate that the characters are in some kind of long-distance relationship. You see a few other self-consistent clusters and feel you now have enough useful data to begin writing an article on unexpected modern romance micro-genres.

In this example, you saw how you can use machine learning to help find micro-genres in books by using the text found on the back of the book. Here is summary of key moments from the lesson you just finished.  
  
**One**  
For some applications of machine learning, you need to not only clean and preprocess the data but also convert the data into a format that is machine readable. In this example, the words were converted into numbers through a process called data vectorization.  
  
**Two**  
Solving problems in machine learning requires iteration. In this example you saw how it was necessary to train the model multiples times for different values of k. After training your model over multiple iterations you saw how the silhouette coefficient could be use to determine the optimal value for **k**.  
  
**Three**  
During model inference you continued to inspect the clusters for accuracy to ensure that your model was generative useful predictions.  
  
**Terminology**

- **Bag of words**: A technique used to extract features from text. It counts how many times a word appears in a document (corpus), and then transforms that information into a dataset.
- **Data vectorization**: A process that converts non-numeric data into a numerical format so that it can be used by a machine learning model.
- **Silhouette coefficients**: A score from -1 to 1 describing the clusters found during modeling. 
	- A score near zero indicates overlapping clusters.
	- Scores less than zero indicate data points assigned to incorrect clusters. 
	- A score approaching 1 indicates successful identification of discrete non-overlapping clusters.
- **Stop words**: A list of words removed by natural language processing tools when building your dataset. There is no single universal list of stop words used by all-natural language processing tools.