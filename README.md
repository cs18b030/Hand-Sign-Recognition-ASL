# Hand-Sign-Recognition-ASL
We applied hand sign classification for ASL and made a descent real time application for that purpose.   <br>
Here is a demo of our work: <br>
![Hello World Demo](https://github.com/cs18b030/Hand-Sign-Recognition-ASL/blob/master/Hello%20World.gif)
<br>
**Packages Used:**<br>
- Keras
- Tensorflow  
- OpenCV


**About The dataset:**<br>
We first used the data by MNIST for ASL hand sign classification [link](https://www.kaggle.com/datamunge/sign-language-mnist). The images were 28x28 in grayscale. The training model performed good on the data but in real time results were not satisfactory. So we decided to generate our own [data](https://drive.google.com/file/d/1zvWoFZvQIMIGhBhWD_xMLs6_99lIOn4s/view?usp=sharing). This data has 6 arrays - normal images, images with canny filter, images after denoising, images after histogram equalisation and truth values Y. We created ~13000 RGB-images of 100x100x3 from laptop-webcam. On these images, standard pre processing steps were applied:<br>
- Histogram Equalisation  
- Denoising by Bilateral Filter  
- Edge detection by Canny filter  
Performing these pre processing steps increased the accuracy by 2-3%.


**Data Augmentation**<br>
The data collected by the team members was localised and in a few specific back-grounds and lightings. Thus initially the results in real-time application of the models specified above was not very encouraging, although the data augmentation when done while training the model improved the in general performance in real-time conditions

**Model**<br>
The following models were implemented :  
- Resnet-50 : this was a standard resnet50 which was trained with input as 100x100x3
- CNN Model 1: this model has about a million parameters and is easy to train and predictions are fast, input is 100x100x3 RGB image.
- Multi Input pipeline : this model was implemented with two input pipelines one takes 
100x100x3 RGBimage as input and the other takes 100x100x1 grayscale image as input.
  
Observations and inference made on the basis of performance of above models:  
- Resnet50: The model has a large number of parameters (23 million). Although the large size of the pipeline does not affect the speed of real-time predictions to a noticeable extent. 
- CNN Model 1: The model has about a million parameters i.e. the pipeline is light and predictions are fast, fit for real-time predictions. The performance of this model is similar to resnet with the improvement of speed and model size.
- Multi-input pipeline model, this model was implemented in the hope to improve accuracy although it did not improve the performance. The model is slower than both the above models and hence not fit for real-time applications.



**Real Time Implementation**<br>
For real time, we created a fixed box, and placed our hand in the box. On pressing ‘p’, the model is prompted to generate a prediction for the given input image. The demo is in a way so that you can write a word on the screen by pressing ‘p’ again and again with different symbols. For the sole purpose of the demo, keypress = ‘e’ is used for backspace, ‘p’ is for prediction, ‘n’ for clearing the screen or ‘new’ word and spacebar for space.





**Skin Segmentation**<br>
- Method1:<br>
Skin Segmentation is done using Thresholding in the YCrCb Color space<br>
Step1: We have a BGR image captured by the webcam. <br>
Step2: Convert this image to YCrCb color space and apply the threshold. <br>
In simple terms take each pixel of an image, if that pixel is in the range of the “threshold values” then make it white if not make it black.
In our context, the threshold values will be YCrCb values denoting the range of “skin color”. The YCrCb ranges can be obtained by doing a bit of trial and error.

- Method2:<br> Skin Segmentation was done using Thresholding in the HSV Color space but better results were obtained by doing it in YCrCb sapce so we switched to YCrCb.

- Method3 :<br>
Extract skin colour from the colour of your hand and use it to set the thresholds while doing skin segmentation.<br>
Step1: Provide an image of your hand such that your hand covers most part of the frame.<br>
Step2: Dominant colour is extracted from this frame using K-means clustering.<br>
Step3: This colour is used to set the threshold while performing skin segmentation instead of hard-coding the colour.

- Method4 : <br>
In method 2 one still needs to take their hand in the frame specified and ensure that their hand covers most of the frame.
So, instead of doing this we used the skin colour from our face.<br>
Step1: The face is detected in the frame using a haar cascade classifier.<br>
Step2: After extracting the face from the frame the dominant colour is again found using K-means clustering<br>
Step3: This colour is used to set the threshold while performing skin segmentation instead of hard-coding the colour.
<br>
All the above methods are fast enough to be used in a real time implementation.
<br>

Variations in illumination can have significant effects on the apparent colour of skin, which can be damaging to the
efficiancy of any colour-based segmentation approach which we are using.

**Future Work:**
Given a set of detected faces (or, a set of regions believed to contain faces), we require methods that can reliably extract
the skin pixels that will be used to build our colour model. We have seen that the
detection regions tend to be quite large overestimations of actual face sizes, so we must firstly discard the significant
amounts of background information within them. Secondly, we must filter out the non-skin features of faces themselves.
<br> 
<br>
Fortunately, however, these non-skin features tend to share one common trait: extreme intensity.
Features such as facial hair, nostrils, pupils, and mouths will all usually tend towards black (low intensity), whereas those
such as eyes, teeth, and glasses glare usually tend towards white (high intensity). This allows for the filtration of these
features.
