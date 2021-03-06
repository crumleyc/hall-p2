# hall-p2

## Ciliary Motion Extraction : Cilia Segmentation

Cilia is a hair-like object protruding out of cell-bodies. Our task is to segment them and identify regions with Cilia. This problem is particularly hard and lack of data makes it even harder. We only had 214 video instance to train.  
The core aim of a learning algorithim in Cilia segmentation should be to learn texture of Cilia and how it moves in a video. 

This repository takes small video clips of cilla and returns segmetations of the frames to identify the location of the cillia. This project was created for CSCI 8360 Data Science Practicum at the University of Georgia. 

### Approach
This project took different approaches to identify the cilia with fluctuation variance, optical flow, and unets. 
  * [Fluctuation Variance](https://github.com/dsp-uga/hall-p2/wiki/Variance)
    * We compute the variance across frames. This will tell us how much each pixel has changed compared to the mean, but also will help us identify regions that could be Cillia. 
  * [Optical Flow](https://github.com/dsp-uga/hall-p2/wiki/Optical-Flow)
    * This approach looks at two frames at a time to find movement of objects between them. It creates a 2D vector that shows the displacement of each pixel from frame to frame. 
     
  * [Unet](https://github.com/dsp-uga/hall-p2/wiki/Unet)
    * UNets have proved to be highly efficient and effective in biomedical imaging domain. They don't require as much data as other CNN architectures such as FCNs. 
    * We implement Unets from [this github repository](https://github.com/zhixuhao/unet). It is based on the model built by researchers who invented Unets. 

### Getting Started
These next two sections will help you run this project on your local machine to attempt at replicating our results. 

#### Prerequisites
This project uses different Python packages listed below:
  * [Python](https://docs.anaconda.com/anaconda/install/windows/): Install python using Anaconda to create your own environments to run unets later on. 
  * [Keras](https://keras.io/): A deep learning package that is used to build the UNets that really makes the code easy to follow.
  * [OpenCv](https://opencv.org/): The library that contains different methods to processes images and implements the Optical Flow functions
  * [Skimage](https://scikit-image.org/): Another image processing library that we used for different prepressing [filters](http://scikit-image.org/docs/dev/api/skimage.filters.html). We used these 4 filters: roberts, sobel, scharr, and prewitt. 
 * [Tensorflow](https://www.tensorflow.org/)  
 * [GPU setup](https://medium.com/@raza.shahzad/setting-up-tensorflow-gpu-keras-in-conda-on-windows-10-75d4fd498198). We used this link to setup GPU to train unets using Keras and tensorflow backend. 
#### Installing Dependencies
[Conda](https://conda.io/en/latest/) will easily mange the enviornment and install all dependencies for these libraries that we used. 

### How to run
This project could be downloaded and run using the main script. It will automatically download the data and 
implement various techniques on the data.
Please refer the link [Wiki](https://github.com/dsp-uga/hall-p2/wiki/How-to-run) for details on how to run this project.

### Data 
Data could be downloaded using the scritps in the script folder of this repo, or running the main script downloads the data automatically on the local system.

### Results 

#### [Unet](https://github.com/dsp-uga/hall-p2/wiki/Unet)

|Unet Type   | Variance weight  | optical weight  |   | IOU Accuracy  |
|---|---|---|---|---|
| Multi  |  0 | 0  |   | 9.3  |
| Binary  | 0  | 0  |   | 15.5  |
|  Binary |  0.2 |  0.2|   |  5. |
|  Binary |  0.2 | 0|   |  17.2|
|  Binary |  1.0 | 0|   |  8.4|

#### [Optical Flow](https://github.com/dsp-uga/hall-p2/wiki/Optical-Flow)

|Method of Image | IOU Accuracy  |
|---|---|
| Merge 100 frames into 1 image| 11.6  |
| First 2 frames |  12.4  |
|  Step-wise |    13.0 |
|  All 100 frames |  21.2|
| Sobel Operator with all 100 frames | 0.8  |

#### [Fluctuation Variance](https://github.com/dsp-uga/hall-p2/wiki/Variance) 

|  scale | hop  | threshold  |   | IOU Accuracy |
|---|---|---|---|---|
|  2 |4   |10   |   |17.1  |
|  3 | 4  | 10  |   |18   |
|  3 | 1  |  5 |   | 18.2  |
|  2 | 8  | 10  |   | 16.6  |
|  2 | 8  | Mean+ 1 S.D(Standard Deviation) |   | 19.5 (Approach 2)  |


## References

1. [Unet Paper](https://arxiv.org/abs/1505.04597)
2. [Unet Repo, third party](https://github.com/zhixuhao/unet)
3. [Setting up Tensorflow GPU](https://medium.com/@raza.shahzad/setting-up-tensorflow-gpu-keras-in-conda-on-windows-10-75d4fd498198)
4. [Optical Flow](https://en.wikipedia.org/wiki/Optical_flow)
5. https://www.kdnuggets.com/2016/11/intuitive-explanation-convolutional-neural-networks.html
6. https://elitedatascience.com/keras-tutorial-deep-learning-in-python
7. https://course.fast.ai/videos/?lesson=3
 
The list of authors and their contributions are listed here -- [Contributors](CONTRIBUTORS.md)
### License
This project is licensed under the MIT Liscense -- [License](LICENSE)
