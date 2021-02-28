# Keras-MNIST
Description about PNN CW5 Type1:

Data Preprocessing:
import mnist from keras library datasets module, and use load_data() method to extract training and testing images and their corresponding labels;
format the data: covert the data type to float32 by using astype() method; value normalisation: CNN converges faster on [0, 1] data than on [0, 255];
import to_categorical function from keras library utils module; One Hot encoding: there are 10 digits: 0-9, e.g., 2 digit: (0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0). In this case, 1 represents presence, and 0 represents absence;

Backbone:
Keras Sequential API, add one layer at a time;
Convolutional layer: 32 filters, each filter transforms a part of the image defined by the kernel size. The kernel filter matrix is applied to the whole image; Rectified Linear Unit activation function: relu(x) = max(x, 0)
Add BatchNormalisation layer to reduce overfitting and improve generalisation
Add pooling layer: this layer acts as a downsampling filter. It looks at the 2 neighboring pixels and picks the maximal value. These are used to decrease the computational cost and reduce overfitting to some extent. More the pooling size is large, more the downsampling is important;
CNN is able to combine local features and learn more global features of the image by combining convolutional and pooling layer;
Add the flatten layer: convert the final feature maps (transformed images) into one single 1D vector. These flattening step is needed before using fully connected layer. It combines all the found local features of the previous convolutional layers
Dropout: one of the regularization methods, where a proportion of neurons in this layer are randomly ignored (setting their weights to zero) for each training sample. This technique also improves generalisation and reduces overfitting
In the end, two fully connected (Dense) layers which are artificial neural network classifiers. In the last layer, the network outputs distribution of probability of each class.

Choosing the loss function and optimizer to compile the network:
there are 10 classes (> 2 classes), 0-9, so we use categorical_crossentropy loss function. Otherwise (just 2 classes), we use binary_crossentropy function. The most important function is the optimizer. It will iteratively improve parameters, such as filters' kernel values, weights and bias of neurons, in order to minimise the loss.

Data Augmentation:
to produce many additional images for each original image by shifting, rotating, changing scale, flipping, shearing and cropping etc. while keeping the label the same. By applying some transformations to our training data, we can easily double or triple the number of training samples and create a very robust model. In this case, randomly rotate some training images by 8 degrees (0-180 degrees); randomly zoom by 8% some training images; randomly shift images horizontally by 8%; randomly shift images vertically by 8% ...


Description about PNN CW5 Type2:

The first four cells: Data Preprocessing

Backbone:
strides: step size along the width and height direction;
padding: "same": output's size is the same as input's. "valid": return just non-padding parts;

Training:
import LearningRateScheduler from keras library callbacks module;
details: https://keras.io/zh/callbacks/#learningratescheduler
import ModelCheckpoint class to record each model of each epoch from keras.callbacks;
details: https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/ModelCheckpoint?hl=zh-cn
