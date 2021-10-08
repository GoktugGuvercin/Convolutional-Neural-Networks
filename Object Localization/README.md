# Object Localization

* Object localization can be regarded as upgraded version of image classification task. The convolutional models are expected not only to categorize target object, 
but also to determine where it is located on the image. The essential point where object localization and image classification get together is that they cope with 
only one object per image; different kinds of objects are allowed to show up at the same time under the scope of object detection task.


* Convolutional architectures designed for image classification takes an image of particular object as input, and give as output a vector of its class probabilities
to specify the amount of chance of belonging to each category. When localization task is also included in this process, the models are also supposed to predict the
coordinates of a bounding box, which encloses the object in the scene. Although it is changeable and completely up to the approach that the developers follow, a 
typical bounding box is generally represented by (x, y) center coordinates and measurement of length (height, width). 
