After training our model lets see how well our model work.
# Model accuracy

Model accuracy is a fairly common evaluation metric. _Accuracy_ is the fraction of predictions a model gets right.

Here's an example:

![Flowers](https://student.deepracer.com/static/media/flowers.4a259a4a910266882157.png)

Imagine that you build a model to identify a flower as one of two common species based on measurable details like petal length. You want to know how often your model predicts the correct species. To evaluate models we often use a statistical metrics like accuracy.
![[Pasted image 20240712093714.png|600]]

- Common one's are precision and F1 Score.

# An iterative process

![Iterative process](https://student.deepracer.com/static/media/stepsiter.65955c6d6e21c56486a4.png)

Every step we have gone through is highly iterative and can be changed or rescoped during the course of a project. At each step, you might find that you need to go back and reevaluate some assumptions you had in previous steps. Don't worry! This ambiguity is normal.

## Using Log Loss

![Jackets](https://student.deepracer.com/static/media/jackets.2b7b88774c6eed9e8bd5.png)

Let's say you're trying to predict how likely a customer is to buy either a jacket or t-shirt.

Log loss could be used to understand your model's uncertainty about a given prediction. In a single instance, your model could predict with 5% certainty that a customer is going to buy a t-shirt. In another instance, your model could predict with 80% certainty that a customer is going to buy a t-shirt. Log loss enables you to measure how strongly the model believes that its prediction is accurate.

In both cases, the model predicts that a customer will buy a t-shirt, but the model's certainty about that prediction can change.