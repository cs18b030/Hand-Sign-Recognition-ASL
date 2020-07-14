# Hand-Sign-Recognition-ASL
We applied hand sign classification for ASL and made a descent real time application for that purpose.   <br>
Here is a demo of our work: <br>
![Hello World Demo](https://github.com/cs18b030/Hand-Sign-Recognition-ASL/blob/master/Hello%20World.gif)
<br>
**Packages Used:**<br>
- Keras
- Tensorflow  
- OpenCV
<br><br>
**About The dataset:**<br>
We first used the data by MNIST for ASL hand sign classification [link](https://www.kaggle.com/datamunge/sign-language-mnist). The images were 28x28 in grayscale. The training model performed good on the data but in real time results were not satisfactory. So we decided to generate our own [data](https://drive.google.com/file/d/1zvWoFZvQIMIGhBhWD_xMLs6_99lIOn4s/view?usp=sharing). We created ~13000 RGB-images of 100x100x3 from laptop-webcam. On these images, standard pre processing steps were applied:<br>
- Histogram Equalisation  
- Denoising by Bilateral Filter  
- Edge detection by Canny filter  
<br>    
    
