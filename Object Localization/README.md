# Object Localization

* Object localization can be regarded as upgraded version of image classification task. The convolutional models are expected not only to categorize target object, 
but also to determine where it is located on the image. The essential point where object localization and image classification get together is that they cope with 
only one object per image; different kinds of objects are allowed to show up at the same time under the scope of object detection task.


* Convolutional architectures designed for image classification takes an image of particular object as input, and give as output a vector of its class probabilities
to specify the amount of chance of belonging to each category. When localization task is also included in this process, the models are also supposed to predict the
coordinates of a bounding box, which encloses the object in the scene. Although it is changeable and completely up to the approach that the developers follow, a 
typical bounding box is generally represented by (x, y) center coordinates and measurement of length (height, width). 


* What is controversial in this point is how regression and classification are combined on one architecture. In fact, this can be realized by building a model with two different heads. The model starts with a set of stacked convolutional layers to extract necessary pieces of information from input image. Then, feature vector coming from the output of convolution block is fed to two disjoint groups of fully-connected (FC) layers dedicated to class and box prediction respectively. This results in two different branches in computation graph of the model, each of which is optimized by separate loss function. While classification branch gets into the responsibility of Negative-Log Likelihood (NLL) loss, regressor side is managed by Mean-Squared Error (MSE) loss. The point where both loss functions have a right to say something during parameter optimization is actually convolutional block. To update feature extractor in consistency, backpropagated gradients coming from both branches have to be in same value scale. To accomplish this, the value of location and length measurements of bounding boxes are scaled to 0-1 range just like the probability values.
