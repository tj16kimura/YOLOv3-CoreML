# YOLO with Core ML

This repo was forked and modified from [hollance/YOLO-CoreML-MPSNNGraph](https://github.com/hollance/YOLO-CoreML-MPSNNGraph). Some changes I made:

1. Add YOLOv3 model.
2. Only keep Keras converter.

TODO:
1. This version only used 13x13x(3x(80+4+1)) output, YOLOv3 has 3 scale outputs. Should fix output calculation use k-means clustering to determine bounding box priors.
>We just sort of chose 9 clusters and 3 scales arbitrarily and then divide up the clusters evenly across scales. On the COCO dataset the 9 clusters were: (10×13),(16×30),(33×23),(30×61),(62×45),(59×119),(116 × 90),(156 × 198),(373 × 326).


## About YOLO object detection

YOLO is an object detection network. It can detect multiple objects in an image and puts bounding boxes around these objects. [Read hollance's blog post about YOLO](http://machinethink.net/blog/object-detection-with-yolo/) to learn more about how it works.

![YOLO in action](YOLO.jpg)

In this repo you'll find:

- **YOLOv3-CoreML:** A demo app that runs the YOLOv3 neural network on Core ML.
- **Converter:** The scripts needed to convert the original Keras YOLOv3 model to Core ML.

To run the app:

1. Extract YOLOv3 CoreML model in YOLOv3 CoreML model folder and copy to YOLOv3-CoreML/YOLOv3-CoreML folder.
2. Open the **xcodeproj** file in Xcode 9 and run it on a device with iOS 11 or better installed.

The reported "elapsed" time is how long it takes the YOLO neural net to process a single image. The FPS is the actual throughput achieved by the app.

> **NOTE:** Running these kinds of neural networks eats up a lot of battery power. The app can put a limit on the number of times per second it runs the neural net. You can change this in `setUpCamera()` by changing the line `videoCapture.fps = 50` to a smaller number.

## Converting the models

> **NOTE:** You don't need to convert the models yourself. Everything you need to run the demo apps is included in the Xcode projects already. 

The model is converted from Keras h5 model, follow the Quick Start guide [keras-yolo3](https://github.com/qqwweee/keras-yolo3) to get YOLOv3 Keras h5 model, then use coreml.py to convert h5 model to CoreML model.

