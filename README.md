# Robotics, Vision and Control Experiments
Juan-Pablo Ramirez, <jpiramirez@gmail.com>, <jpramirez@ufl.edu>

This package contains experimental code that may be incorporated into other projects at a later stage.

## ros_inception

This is a small ROS node that uses [Tensorflow](https://www.tensorflow.org) and Google InceptionV3 to classify images from a video stream,
on-the-fly. It is a fusion of the [cv_bridge tutorial code](http://wiki.ros.org/cv_bridge/Tutorials/ConvertingBetweenROSImagesAndOpenCVImagesPython) from ROS and the [classify_image.py script from Google](https://github.com/tensorflow/models/blob/master/tutorials/image/imagenet/classify_image.py).

### Prerequisites

* Tensorflow (properly configured and tested)
* ROS (tested on Kinetic)
* ROS node that publishes a BGR8 image topic (I use openni2_camera with an ASUS Xtion sensor)

### How to use
Use rosrun from within an environment that has access to Tensorflow. For example, if you followed the [Tensorflow installation
tutorials and used virtualenv](https://www.tensorflow.org/install/install_linux#InstallingVirtualenv), then you must first use `source tensorflow/bin/activate` and then call rosrun from the command line
prompt with the (tensorflow) prefix.

To launch the node use
`rosrun rvcexp ros_inception image:=/path/to/your/image_raw`

The node will take arguments similar to those in the original classify_image.py, as
`rosrun rvcexp ros_inception --model_dir dir_for_inception --num_top_predictions 10 image:=/your/topic`

I tested the node on a machine with the following specs
* Intel Xeon CPU E3-1246
* 32 GB of Ram
* GeForce GTX 1050 Ti

and the image classification ran at 10 FPS. [Video demonstration](https://youtu.be/cvaYFF3vgWA)

### Topics
* `/image` is the image topic to which the node subscribes.
* `/inception` is a std_msgs:String message with the classification tags.
