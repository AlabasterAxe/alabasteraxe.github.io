---
id: 19
timestamp: 1541350838
author: "Matt Keller"
title: "Machine Learning: Chapter 1 - Introduction"
excerpt "Dipping a toe into machine learning starting from basic math."
---

This is the first in a series of blog posts, the aim of which is to introduce the reader to various ML concepts.

## Who should read this?

First things first, this series of blog posts is written under the assumption that you are at least somewhat familiar with basic programming and mathematical concepts. If you’re comfortable with the following ideas, you should be alright:

-   Functions
-   Summations (𝚺)
-   Vectors or Arrays

The goal is for these blog posts to be practical guides which have real examples you can try out (using python and TensorFlow) but if you’re just interested in learning the concepts you should still find these posts useful.

## What is ML?

Ultimately, the goal of ML is to create a function. It’s not dissimilar to ones you’ve probably written many times before. You have some input and you want some expected output.

The key difference is how we create this function. Whereas with your typical function, you just spin up your favorite text editor and write it out, in machine learning, you show your function (many!) examples of input and output that demonstrate the desired behavior and over time, it approximates the desired behavior.

You might be asking yourself: “If it’s just a function why don’t we just write it out instead of faffing about with this whole ML business?” That’s the right question to be asking! In some cases the right thing to do is manually construct these functions as opposed to resorting to ML. In other cases, though, it is tedious and error-prone for humans to write such functions by hand (e.g. write a function to accept a 28x28 grid of pixels and return which number is in the picture. You probably **could** write such a function by hand, but you’ll probably want to claw your eyeballs out by the time you’re done.)

By way of example, let’s say we want to create a tool to tell us whether food is healthy or not. Obviously, this is a complicated question which varies from person to person but let’s assume, for the sake of this blog post, that it’s possible to create such a function. We can set it up so that it takes in the information on a Nutrition Facts label. In this situation, the inputs to the function are things like Calories, amount of fat, amount of vitamin A etc…

Using machine learning terminology, we might say these are our **_dimensions_**, or our **_predictors_** for this machine learning task.

So, when we have our model, we would pass in all of these dimensions, and it outputs a designation HEALTHY or UNHEALTHY.

![Figure 1:  Does this look healthy to you?](https://images.squarespace-cdn.com/content/v1/5bc3ae2ca56827a279bf229b/1541757216872-1VG8SGX6KU8VXMP2NR4L/Peach_NutritionLabel.png?format=500w)

**Figure 1:** Does this look healthy to you?

Okay so now we have a sense for what a machine learning task looks like, in terms of what the inputs and outputs are. How are we supposed to actually learn this relationship though?

## How do we learn this function?

Before we can talk about the different techniques for using these examples to learn the relationship, we need to discuss the idea of “Loss” which is fundamental to many machine learning tasks.

### LOSS

Loss represents the quality of your function or model. The ML model gives you answers; loss tells you how wrong those answers are. The goal of a supervised machine learning task is to pick a model such that the output of the loss function is minimized. One way to think about loss is that your model is a student (we are trying to get the model to learn after all!) We’re giving our student a test and the loss is our student’s score on the test.

Going back to our example from above, let’s say we created a V1 of our function and we want to see how it’s doing.

![Table 1:  Our student’s test answers vs the answer key](https://images.squarespace-cdn.com/content/v1/5bc3ae2ca56827a279bf229b/1541757773356-7VWDAGJF3VP7YD84GFXQ/Screenshot+from+2018-11-09+10-02-29.png?format=1000w)

**Table 1:** Our student’s test answers vs the answer key

So from Table 1 we can see that we asked our model about the four foods above and it said HEALTHY every single time. Clearly not the behavior we were looking for! One simple way to calculate the loss in this situation would be to calculate the ratio of incorrect answers to all answers. In this case, loss would be 2/4 or 0.5.

There are many different ways to construct the loss function. Which one is best is highly dependent on your problem.

### TRAINING

Now that we understand the notion of loss, we can get back to the original question which was, “how do we learn this function?” The answer is through a process called “training”. Using the process we described above to calculate loss, the process of training is:

-   Give the model some examples with known values
    
-   Calculate the loss of the model
    
-   Look at the examples that the model got wrong and got right
    
-   For the ones it got wrong, we want to nudge it in the right direction  
      
    

As with most things in life, the devil of training an ML model is in the details. Getting into the weeds for training is outside the scope of this post but this should give you an understanding of what the process looks like in the abstract. In future posts, we’ll be able to add some color to this process by talking about the specifics of a real learning task you can work through yourself.

---

So this was obviously just the very beginning of learning about ML. The main things I’d want you to take away from this article are:

-   ML “models” are just functions, with inputs and desired outputs
    
-   Loss is a single number that represents our model’s quality. The lower the loss the better the model.
    
-   Training takes the output of the loss function and uses it to nudge the model in the right direction.
    

Hopefully, this article was able to demystify some of the aspects of ML and show that there’s really nothing magical going on here.

In the [[2018-11-24-machine-learning-2|next article]], we’ll see how to create a basic machine learning model to solve an example problem.