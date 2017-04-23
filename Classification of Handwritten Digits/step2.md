## Download MNIST dataset

Now, open the notebook **ep7.ipynb** by simply clicking onto it. Here are the imports we have use, `matplotlib` to display images, and of course `TF.learn` to train the classifier. All of these are installed with the image. 

     import matplotlib.pyplot as plt
     %matplotlib inline
     import tensorflow as tf
     learn = tf.contrib.learn
     tf.logging.set_verbosity(tf.logging.ERROR)

Next, we'll download the MNIST dataset using,

     mnist = learn.datasets.load_dataset('mnist')
     
Th dataset contains thousand of labeled images of handwritten digits. The MNIST data is split into three parts: 55,000 data points of training data (mnist.train), 10,000 points of test data (mnist.test), and 5,000 points of validation data (mnist.validation). This split is very important: it's essential in machine learning that we have separate data which we don't learn from so that we can make sure that what we've learned actually generalizes! 
