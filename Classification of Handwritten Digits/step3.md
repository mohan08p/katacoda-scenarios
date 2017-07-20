## Visualize Images

Let's visualize the images. This code displays an image along with its label, and, you might notice we have reshaping the image

     def display(i):
         img = test_data[i]
         plt.title('Example %d. Label: %d' % (i, test_labels[i]))
         plt.imshow(img.reshape((28,28)), cmap=plt.cm.gray_r)    
         
The first image from the testing set is 7, and you can see the example as well as the label. Then, second image 2, now both of these are clearly drawn, but theres variety of different handwriting samples in this dataset. Then, the next image 5, that's harder to recognize. These images are low resolution, just 28 * 28 pixels in greyscale. Also, note that they are properly segmented. That means each image contains exactly one digit. 

Now let's talk about the feature we have used. When we work with images, we use the raw pixels as features. That's because extracting useful features from images, like textures and shapes, is hard. Now, a 28 * 28 has 784 pixels, so we have, 784 features. And here we're using the flattened representation of the image. To flatten an image means to convert it to 2D array to a 1D array by unstacking the rows and lining them up. That's why we had to reshape this array to display it earlier. 