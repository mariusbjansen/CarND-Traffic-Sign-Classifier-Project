# **Build a Traffic Sign Recognition Classifier** 

## Reflection
In this project the goal was to create a pipieline for the classifcation of traffic signs.

Example image

<img src="00000_00005.jpg" width="300">

Example result

Classified by label (some number) with the meaning limit 80kph

### 1. Processing chain

The following items describe the steps of processing.

#### 1 Loading the data
The data is was stored in pickled format and consist of a training set, a validation set and a test set

#### 2 Dataset Summary & Exploration
The data given was imbalanced. For example the ratio of the class with the most samples to the class with the least samples is 11!
The data given was a colored image (three channels)

I created histograms for a visual representation of the representation of the samples (train and validation) and also one sample image in color color with dimensions 32x32.

#### 3 Design and Test a Model Architecture
##### Dealing with the data set
First point is to deal with the shortcomings of the data set. I artifically created additional samples by sampling from the given data and applying
salt and pepper noise (randomly set pixels of the image to either white (255 255 255) or black (0 0 0) ). I also rotated the images by some degrees.

##### Dealing with the data set
Next important step is preprocessing the data.

I applied a reduction (mean of all channels) color to grayscale. My experiments have shown that color does not hold as much information as I believed in the beginning. Since some of the signs hold a specific color like blue or red. But maybe I did not apply the right technique to make use of color :-)
Finally I decided for grayscale in order to increase computing performance.

Also I applied a histogram equalization since some picture are very dark.

Next I normalized so the images have zero mean.

Also the images need to be shuffled to prevent the net to "learn in one direction".

##### Model
The model is exactly LeNet from Yann LeCun with the modification that I increased the dimensions of layer 3 to 300.

I run the net locally on my graphics card. Btw. it took me some time to find out why Jupyter Notebook is not finding the CUDA shared object libraries...
-> You need to pass the environment variables to the jupyter notebook of course.

My other hyper parameters are 

Processing:
EPOCHS = 25
BATCH_SIZE = 512

Weights:
Mean mu = 0
Standard deviation sigma = 0.1

Learning rate = 0.005 = 5e-3

My performance around 85% on a balanced dataset with artificial disturbances. (Notice that on the imbalanced data the performance is even higher. The reason for that is that the validation data
is imbalanced like the training data). Why is that: The classifier implicitly learns the a priori probability. Because label 3's probability is more than 11 times higher than label 0's probability.

Anyway it is important and good for the generalization to balance the dataset. This can also be seen in the Softmax Probabilities later.


#### 4 Test a Model on New Images

I did not download the raw images (as suggested in the notebook) from the web, since I think test dataset was meant to be used)

When I apply the CNN to six new images from the test set the performance is mostly 100%.
Softmax Probabilities for the candidates after the winner are most of the time several orders of magnitude away from the winner, which is an indicator for 
robustness of the net.

#### 5 (Optional): Visualize the Neural Network's State with Test Images

Not yet done


### 2. Shortcomings

#### A Handling imbalanced data

#### B Preprocessing

#### C LeNet's Model

#### D Learning rate


### 3. Suggest possible improvements to your pipeline

#### A One could invest more time for dealing with the imbalanced data. I only applied salt and pepper and rotation. Different filters (blur or sharpen) could be (additionaly) applied.

#### B Preprocessing could be also enhanced by applying suitable filters (blur, sharpen, edge detection) and/or extracting a ROI.

#### C I think spending time on experimenting with layer sizes can also lead to significantly better results since LeNet was possibly optimized for the ten classes of digits.

#### D Introducing a reduction of the learning rate over time while learning can also improve the classification results.

