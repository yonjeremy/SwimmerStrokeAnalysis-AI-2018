

  
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
| 5| Issue of multi-class classification vs multi-labelling classification |
| 6| Labelling more videos for data set creation
| 7| Training classifier with new data set
| 8| Testing classifier with new data |
| 9| Creating project presentation & compiling research


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


----------


- .JPG file extension in the train.py script had to be changed to .jpg lowercase 


----------


- Using wrong configuration file for the Pascal VOC data set
	- Issues correctly matching model, configuration file and data set, (Pascal VOC format  & fastercnn model)


----------


- Initially had the wrong output format when exporting the annotated images from VOTT
	- Pascal VOC is the format in use


----------


- Error trying to push repo to github
> `error: RPC failed; result=22, HTTP code = 413`  
`fatal: The remote end hung up unexpectedly`  
`fatal: The remote end hung up unexpectedly`
> 
 
Could be that local repo is too large, upload buffer is not large enough
*Source : https://stackoverflow.com/questions/7489813/github-push-error-rpc-failed-result-22-http-code-413*


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

![01_test](/media/01_test_case.gif)

**Week 5**
- Researching and addressing the issue of multiclass vs multi-labelling 
	- Currently using binary classification, i.e swimmer or not swimmer
	- Want to differentiate swimmer above water/swimmer below water for stroke count using a sub class of swimmer

 Multi-class classification
 - The classes are mutually exclusive 

Multi-label classification
 - Predicting properties of a data-point that are not mutually exclusive

> For example, in the famous leptograspus crabs  [dataset](http://www.stats.ox.ac.uk/pub/PRNN/)  there are examples of males and females of two colour forms of crab. You could approach this as a multi-class problem with four classes (male-blue, female-blue, male-orange, female-orange). As a multi-label problem,  one label would be male/female and the other blue/orange. Essentially in multi-label problems a pattern can belong to more than one class.
>
> *Source : https://stats.stackexchange.com/questions/11859/what-is-the-difference-between-multiclass-and-multilabel-problem*

	- VOTT unable to multi-label object for multilabel classification
	- Posted issue on VOTT github
	- https://github.com/Microsoft/VoTT/issues/166
 - Researched [LabelImg](https://github.com/Labelbox/Labelbox#labelbox-pluggable-interface-architecture) as an alternative tool for labelling. Multi-labels may be [supported](https://github.com/Labelbox/Labelbox/issues/25).
 - Researched problems associated with multilabelling and multiclass object classification
 - Re-annotating swimming images sample with multiclass classification 
	- swimmer_above_water vs swimmer_below_water

 **Resources**:
 - http://scikit-learn.org/stable/modules/multiclass.html
 - https://www.coursera.org/learn/machine-learning/lecture/68Pol/multiclass-classification-one-vs-all

**Week 6**

 - Added to dataset using more video footage provided by Swimming Ireland
 - Labelling done using two tools, VOTT and LabelImg
 - SSH keys set up allowing for both developers to access VM used for training
 
 **Resources**:
 - https://www.youtube.com/watch?v=nw1GexJzbCI
 - https://cloud.google.com/compute/docs/instances/connecting-to-instance
 - https://gist.github.com/feczo/7282a6e00181fde4281b


**Week 7/8**

 - Training model with newly created data set
 - VOTT github developers have added multilabel classification as [feature to implement in next release](https://github.com/Microsoft/VoTT/issues/166) 
 - Clip from output with improved trained model
![model with above/below classification](https://media.giphy.com/media/2eKfegKPDWTgRiV6zt/giphy.gif)
 - Trying to resolve issue with pushing local git repo on VM to github 
 - Began research & implementation of object tracking using open CV
	 - Predict swimmer using motion tracking
	 - Change example scripts to work with swimmer video feed
	 *- Resource: [Object Tracking Using OpenCV](https://www.google.ie/search?q=open+cv+motion+tracking&rlz=1C1AVNE_enGB701GB706&oq=open+cv+motion+&aqs=chrome.0.69i59j69i57j0l4.2564j0j1&sourceid=chrome&ie=UTF-8)*

**Week 9**
 - Creating Presentation for project
	 - Create video overview
 - Compiling research & outcomes
 - Processing output data from classification script
	 - Ignore bounding boxes outside of range of primary swimmer 
	 - Involves editing [visualization_utils.py](https://github.com/tensorflow/models/blob/master/research/object_detection/utils/visualization_utils.py), script responsible for drawing boxes on output images
 	 - Output data to CSV format
	 - Graph Data
