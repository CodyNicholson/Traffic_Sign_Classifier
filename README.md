# Traffic Sign Classifier Project

In this project I used a deep convolutional neural network to classify images of German traffic signs. The model architecture is inspired by the LeNet architecture created by Yann LeCun.

### 1. Preprocessing My Datasets

To preprocess my datasets I created a pipeline that first grayscales the images, then applies min-max scaling for normalization, and then finally standardizes the data. I grayscaled the images to eliminate the noise that is color. I applied min-max scaling for normalization to make sure the data in my dataset is all on the same scale so that it is easy to compare each data point to each other data point. Lastly, I standardize my data by making the mean equal to zero because I find it easier to plot data that has been standardized.

### 2. Model Architecture

Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model architecture, as seen below, is based off the LeNet architecture. I added dropout near the bottom of the architecture to help with the training of my model. Dropout will randomly select data from the training set to remove. This happens again and again in every epoch with different data points being removed. By training like this we can come closer to simulating how the model will interpret random new data, and better prepare our model for the real world.

| Layer              | Description        |
|:------------------ |:------------------ |
| Input              | 32x32x1 RGB Image  |
| Convolution 5x5    | 28x28x6 Image      |
| RELU               |                    |
| Max Pooling        | 14x14x6 RGB Image  |
| Convolution        | 10x10x16 Image     |
| RELU               |                    |
| Max Pooling        | 5x5x16 RGB Image   |
| Flatten            | 5x5x16 (400)       |
| Convolutional Full | 84                 |
| RELU               |                    |
| Convolutional Full | 10                 |
| Dropout 1          |                    |

### 3. How I Trained My Model

I trained over 100 EPOCHs, but I avoid overfitting the data by using dropout, and by shuffling my data before every sess.run(). In shuffling and using dropout in my training I can simulate randomness to a significant degree. Over 100 EPOCHs I will always get above 93% accuracy, sometimes even 94%.

I kept the learning rate low at 0.001 so that my algorithm learns slowly but with high consistency. I used a BATCH_SIZE of 128, primarily because it worked well for other image classifiers like LeNet.

### 4. My approach to finding the solution and getting the validation set accuracy to be at least 0.93

To find my solution I relied on a modified version of the LeNet architecture with the added ML technique dropout. As you can see in the results, it takes almost 20 EPOCHs to get into the 90% correct range. This is because I set my learning rate to the low value of 0.001, but as you can see after the first 20 EPOCHs there are almost no accuracy values lower then 90%. This consistency is good evidence that my model is working well. I think that the LeNet architecture was very suitable for this problem since this is also an image classifier.

***

## Testing the model on new images

### 1. The five images I chose for my model to classify

If you look at the five images I chose you will see that they all have different lighting as a result of the time of day or season. I was also interested in finding out how the model would perform if there was something covering the sign, so my first image has snow covering the bottom of the sign.

### 2. The model's predictions

Of the five predictions, only four are correct. The one prediction it gets wrong is the sign that is partially covered with snow. I am interested to learn how to augment the image more so that this problem is resolved. Surprisingly, the correct answer for this prediction isn't even in the top five predictions as you can see in the softmax probabilities data visualization below. Other than the sign with the snow on it, the model performed very well on these new images.

### 3. Model certainty

The model seems very certain of its predictions, as seen in the data visualization. For four of the five graphs, there is only one visible bar for the five possible values on the x-axis. Since my model is so certain of itself, it makes me think that it might be a little overfit.

The accuracy on the captured images is 80% while it averaged at about 93% on the testing set. However, the one captured image that gets labeled incorrectly is due to the snow on the sign in the picture. If the sign did not have snow on it, I am confident the model would label it correctly and have 100% accuracy. This leads me to believe that my model may be a bit overfit since it is so confident.
