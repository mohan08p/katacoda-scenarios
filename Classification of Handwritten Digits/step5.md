## Evaluate Accuracy

Once we have a trained model, we can evaluate it. Using the evaluate method we see that it correctly classifies about 90% of the test set. We can also make prediction on individual images. Here's once (digit 7 image) that it correctly classifies, and here's one (digit 5 image) that it gets wrong. 

## Visualize Weights 

Now, we'll see how to visualize the weights the classifier learns. Here, positive weights drawn in red and negative weights drawn in blue. So, what do these weights tell us ? We'll understand that I'll show four image of once. 

![Different types of Drawing the same image Four once](../images/four1s.png)

They are all drawn slightly differently, but, take a look at the middle pixels , notice that it's filled in with every image. When the pixel is filled in, it's evidence that image we are looking at it is a one, so we'd expect a highway on that edge. 

![Four 0s image](../images/four0s.png)

Now, let's take a look at four zeros. Notice that a middle pixel is empty. Although, there is a lot of ways to draw zeros, if that middle pixel is filled in, it's evidence against the image being a zero so we expect the negative weight on the edge. And, looking at the images at the weights, we can almost see outlines of the digits drawn in red for each class. We were able to visualize these, because we started with 784 pixels and we learned 10 weights for each, one for each type of digit. We then reshape the weights into 2D array. 