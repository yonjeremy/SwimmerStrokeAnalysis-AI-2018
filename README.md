
# Object Tracking Project

This is the README for the Object Tracking project. The program enables the user to track swimmers and storing stroke counts.


## Description

The purpose of this project is to explore the use of Google's [Tensorflow](https://github.com/tensorflow/tensorflow) machine learning framework, as well as [OpenCV](https://opencv.org/), to combine machine learning and image recognition in order to explore its use in real-world applications. The proposed project is to track swimmers by either sending in a video file or live feed to the program, which then recognizes swimmers based on a dataset, and track the swimmer's movements and number of strokes taken per lap.


## Progress Report
|Week|  Progress |
|--|--|
| 1| Installing Python with tensorflow and opencv and testing it |
| 2| Live video tracking using webcam, using the COCO model |
| 3| Testing out VOTT (video object tagging tool) and testing out swimmer detection |
| 4| Creating custom models and training AI to recognize swimmers |
| 5| TBC |

*See below for detailed breakdown of each week.*

## Development Environment
 - The current set up is a  6 core VM run on [Google Cloud](https://cloud.google.com/).
 - This VM was used for convenience and as a collaboration space
 - Ubuntu 16.04 runs on the VM
	 - A GUI was needed for viewing of images and testing.
	 - Ubuntu desktop was installed to facilitate this.
	 - To view the GUI, [VNC Server](https://www.realvnc.com/en/) along with port forwarding was used. 
 ### Modifications
 - A number of modifications were made to the [Tensorflow](https://github.com/tensorflow/tensorflow) scripts for our use case
 - .JPG file extension in the train.py script had to be changed to .jpg lowercase 
- Pipeling.config file changed for relative files
## Issues Encountered
- Ensuring all dependencies were met suring installtion of software
- .JPG file extension in the train.py script had to be changed to .jpg lowercase 
- Using wrong configuration file for the Pascal VOC data set
	- Issues correctly matching model, configuration file and data set, (Pascal VOC format  & fastercnn model)
- Initially had the wrong output format when exporting the annotated images from VOTT
	- Pascal VOC is the format in use
## Setup
- **Model**
	- [Faster R-CNN](https://arxiv.org/abs/1506.01497) with Resnet-101 (v1), configured for Pascal VOC Dataset. Created with this script.  
	- Model was not trained from scratch
		- To do so would take days/weeks with given setup
-  **Transfer Learning for efficiency** 
	- The model was trained by taking a fully-trained model and thne retraining from the existing weights for the new swimmer classes.
## Tools
- [Microsoft  VOTT](https://github.com/Microsoft/VoTT) for data set creation
	- Uses CAMSHIFT algorithm (suggestions based on colour detection), which helps speed up image labelling process.
	- Generates XML from the images with labelled classes
	- Can output to various formats, this case being a tensorflow Record (TFRecord)
## Progress Breakdown
  **Week 1**
 -  Set up the VM & development environment
 -  General research on how machine learning works
 - Installed Tensorflow, Python, OpenCV & dependencies 
 
 **Resources**:
1. https://pythonprogramming.net
2. https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/#0
3. https://opensource.com/article/17/11/intro-tensorflow

**Week 2**
 - Tested and learnt basics of how to use Tensorflow
 - Followed tutorials to use a basic image classifier
 - Adapted Tensorflow scripts to classify from live video feed using OpenCV 
 
 **Resources**:
1. https://www.youtube.com/watch?v=2FmcHiLCwTU&t=77s
2. https://pythonprogramming.net/introduction-use-tensorflow-object-detection-api-tutorial
3. https://medium.com/@WuStangDan/step-by-step-tensorflow-object-detection-api-tutorial-part-1-selecting-a-model-a02b6aabe39e

**Week 3**
- Researched different annotations tools
- Learnt to use VOTT 
	- Also learnt about the various export formats (e. gCNTK , Tensorflow (PascalVOC) or YOLO)
- Labelled roughly 100 images with a Swimmer class

**Resources**:
1. https://github.com/Microsoft/VoTT/blob/master/README.md
2. https://pjreddie.com/darknet/yolo
3. http://host.robots.ox.ac.uk/pascal/VOC

**Week 4**
- Exported swimmer data from VOTT to Pascal VOC format
- Converted  Pascal XML to CSV
- Successfully implemented Transfer learning
	- Trained the Faster-CNN model with the swimmer data set
- Test case showing preliminary signs of success: 
![swimmerdetection](https://media.giphy.com/media/4NnPGpnhHSblZMq8Su/giphy.gif)
