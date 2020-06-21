# Hand-Sign-Recognition-ASL
First we try our model on static images of ASL alphabet dataset. Then we'll try and do the same for real time!   <br>
Dataset and current models in the limk: https://drive.google.com/drive/folders/12JUlYr5yRKBm3O9k_ooeJ5pmPhW1UVc5?usp=sharing  

Pre-processing steps:
  img[:,:,0] = cv2.equalizeHist(img[:,:,0])
  img_hist = cv2.cvtColor(img, cv2.COLOR_YUV2BGR)
  bilateral = cv2.bilateralFilter(img_hist, 7, 100, 100) 
  img_canny = cv2.Canny(img_hist,100,200)
  img_blur_canny = cv2.Canny(bilateral,100,200)
