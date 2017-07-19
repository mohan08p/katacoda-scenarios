## Initialize the Classifier

Now we'll initialize the classifier and here, we'll use the linear classifier. We will provide two parameters. The first indicate, how many classes we have, and there are 10, one for each type of digit. The second informs the classifier about the features we'll use.

We'll see the quick diagram of liner classifier to give you a high level preview of how it works under the hood. You can think of the classifier as adding up the evidence that the image is each type of digit. The input nodes are on the top, represented Xes, and the output nodes are on the bottom represented by Ys. We have one input node for each feature or pixel in the image and one output node in the each digit the image could represent. Here, we have 784 inputs and 10 outputs. I have just drawn a few of them, so everything fits on the screen. Now, the inputs and outputs are fully connected, and each of these edges has a weight.

![Linear Classifier](/mohan08p/scenarios/classification%20of%20handwritten%20digits/assets/Linear_classifier.png)

When we classify an image, you can think of each pixel are going on a journey. First, its flow into its input nodes. and, next it travels along the edges. Along the way, it'd multiplied by the weight on the edge, and the output nodes gather evidence that the image we are classifying represents each type of digit. The more evidence we gather, say on the eight output, the more likely the image is an eight. And, to calculate how much evidence we have, we sum the value of pixel intensities multiplied by the weights.

     evidence  yi = Sum Wi,jXj

Then we can predict that the image belongs to the output node with the most evidence. The important part is weights, and by setting them properly we can get accurate classifications. We begin with random weights, then gradually adjust them towards better values. And, this happens inside the `fit` method.
