# Hand-Sign-Recognition-ASL
We applied hand sign classification for ASL and made a descent real time application for that purpose.   <br>
Here is a demo of our work:
![Hello World Demo](https://github.com/cs18b030/Hand-Sign-Recognition-ASL/blob/master/Hello%20World.gif)


Dataset link: https://drive.google.com/file/d/1zvWoFZvQIMIGhBhWD_xMLs6_99lIOn4s/view?usp=sharing  

Pre-processing steps:
    img = cv2.cvtColor(crop_img ,cv2.COLOR_BGR2YUV)  
    img[:,:,0] = cv2.equalizeHist(img[:,:,0])  
    img_hist = cv2.cvtColor(img, cv2.COLOR_YUV2BGR)  
    denoised = cv2.bilateralFilter(img_hist, 7, 100, 100)   
    img_canny = cv2.Canny(img_hist,100,200)  
    img_blur_canny = cv2.Canny(denoised,100,200)   
    
