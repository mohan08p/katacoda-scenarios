As [Docker](https://www.docker.com/) is already installed and configured, we are good to go directly downloading and running the **tensorflow** image.

Before moving further, we'll simply understand the problem is **"classifying the handwritten digits from the `MNIST` dataset** and writing a simple classifier for this is often considered as writing a *Hello World* of computer vision. MNIST is a multi-class classification problem. Given an image of a digit, our job is to predict which one it is. We have written an ipython Notebook(official tutorial from tensorflow community) for this tutorial and to make it easier to configure your environment, we'll start with quick screencast with installing TensorFlow using Docker.

Here are the steps to do it,
**1) Installation**
**2) Download Data set**
**3) Visualize Images**
**4) Train a Classifier**
**5) Evaluate**
**6) Visualize Weights**

## Installation of TensorFlow using Docker
You can find the installation instruction for **TensorFlow** using [docker installation](https://www.tensorflow.org/versions/r0.10/get_started/os_setup#docker_installation) on the homepage under the getting stated. 

Next we will launch a docker container with a [tensorflow image](https://hub.docker.com/r/tensorflow/tensorflow/). The image is hosted on *docker hub*, simply click on the tensorflow image in previous sentence. The image contains tensorflow with all of its dependencies properly configured. Everything is configured with in this image, as docker is configured on this platform. Here, is the command to run this image, with the version you want, as I have choose the latest release, `1.1.0-rc2`

`docker run -it -p 8888:8888 tensorflow/tensorflow:1.1.0-rc2`{{execute}}

If it's a first time you've run the image, it'll be downloaded automatically. And, on subsequent runs it will be cached locally. The image starts automatically and by default, it runs a notebook server. Just note down the `token` in the link as I shown below from your terminal window.

     Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://localhost:8888/?token=061f975ebc5cc069a4974fbc869b0bcef6cf4d23132b355c

Now, you can go to the browser and point it to the IP on port 8888. In this case, simply click on + option besides Terminal and select **View HTTP Port 80 on Host 1** and finally enter the port as **8888** in **Display a different port** It will prompt to the Login into the **Jupyter** and the above token you can copied into the password and then we'll have an **ipython Notebook dashboard** that we can experiment in the browser served by the container. Now you can upload the notebook [**ep7.ipynb**](https://github.com/random-forests/tutorials/blob/master/ep7.ipynb) through the UI. 
