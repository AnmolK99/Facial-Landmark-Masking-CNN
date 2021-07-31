# Facial-Landmark-Masking-CNN
Masking Lips and Eyes of Images by a CNN to detect Facial Landmarks

**Dataset used**,
Cleaned Muct Dataset
http://www.milbo.org/muct/  
https://github.com/StephenMilborrow/muct (Uncleaned raw ones)  
https://drive.google.com/drive/folders/1mSDsY3gIC2_etcvk-WTWJcIxSApnORZB?usp=sharing (Cleaned ones here)  
List of training 7049 images. Row containing (x,y) coordinates for 15 keypoints, and image data as row-ordered list of pixels.
List of 1783 test images. Row containing ImageId and image data as row-ordered list of pixels.

**SUMMARY**  
Facial Landmark masking is an old techniques been used in social media and phone camera filters  
Here we have used Neural Nets to detect facial 15 landmarks  
![Landmark Depicted over James Madison jr.'s face](https://github.com/AnmolK99/Facial-Landmark-Masking-CNN-/blob/main/images/15_landmark_pts.png?raw=true)  

above image depicts the landmarks we are targeting our NN to detect.

Masking the image with relevant color Blob is not so difficult task when you have the points  
surrounding the targetted area  
this task can be done using OpenCVs FillPoly function  
_cv2.fillPoly(img2, mask_points, choice, lineType=cv2.LINE_AA)_  

Post-Prediction the image, Predicted Landmark Positions and Mask looks like below  
![original_image](https://github.com/AnmolK99/Facial-Landmark-Masking-CNN-/blob/main/images/index4.png)
![Predicted landmark on image](https://github.com/AnmolK99/Facial-Landmark-Masking-CNN-/blob/main/images/index5.png)
![Masking of landmarks predicted](https://github.com/AnmolK99/Facial-Landmark-Masking-CNN-/blob/main/images/index6.png)  
![original_image](https://github.com/AnmolK99/Facial-Landmark-Masking-CNN-/blob/main/images/index7.png)
![Predicted landmark on image](https://github.com/AnmolK99/Facial-Landmark-Masking-CNN-/blob/main/images/index8.png)
![Masking of landmarks predicted](https://github.com/AnmolK99/Facial-Landmark-Masking-CNN-/blob/main/images/index9.png)  
(Please check for other testimages as well and test the model for accuracy)
(the images seems uplifted and towards left a little which can easily be solved by increasing the x and y coordinate values of checkpoints) 

(**Please Check the Model and Outcome on your Machine yourself, This Method is running prefectly for Human Face Images**)


**Data Extraction**   
Data is of Image files which are created by 2D structuring of 1D row ordered list of Pixels.  
**_img = ['0' if x ==" " else x for x in img]_**  
above line is converting each row of table 'raw' into a 2D matrix of values,
which is further appended into images array of 2D matrices of images

**Data Preprocessing**  
Each Image is reshaped into [96,96] matrix for feeding to our NN and color schema changed from (0,255) to (0,1)

**Model Training**  
Model is compiled with MSE as loss function as MSE also works on Outliner values in our data.
Accuracy Metric is MAE.


Model is trained for 100 epochs as i have observed an average increase in accuracy with number of epochs.
Batch size is 255 to devide the whole dataset into not too many batches
(Here, Model is trained on Fast GPU of Google Cloud with using Google colab)

**FInal Outcome**  
The Model being trained for 100 epocs shows accuracy and loss metrics as shown on below graphs
![Accuracy Visualization](https://github.com/AnmolK99/Facial-Landmark-Masking-CNN-/blob/main/images/accuracy_metrics.png)
![Loss Visualization](https://github.com/AnmolK99/Facial-Landmark-Masking-CNN-/blob/main/images/loss_metrics.png)  
(Above Model is trained on fast GPU of Google Colab cloud environment, if you want to try it just export the dataset and .ipynb file to colab directory and run the commands there)

This Method is Detecting the 15 Facial Landmarks using CNN,  
many other pre-built libraries with > 20 facial landmark identification can be found over the Internet such as ,
- Detector of **dlib** library  which comes with the versatile identification of 68 Facial Landmarks
- **PyTorch** (a well-known one)
- **PyCaret**
