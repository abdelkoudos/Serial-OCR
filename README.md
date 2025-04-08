# National ID Serial Extraction and Recognition

## Project Overview

This project focuses on extracting and recognizing Egyptian national ID serial numbers from images. The serial number consists of two letters followed by seven digits (e.g., AB1234567). The objective is to extract and recognize these serial numbers as text.

Initially, I attempted to solve this problem using pretrained models like Keras OCR and Tesseract. However, I encountered challenges with these solutions. The architectures were unnecessarily complex, leading to significant time delays, and the results were much worse than when implementing my own custom architecture.

### **Note:**
Please note that this project is intended for **documentation purposes**. The dataset used in this project is **confidential**, and as such, I am unable to share the data publicly. However, the methodology and code provided can be adapted to similar datasets for learning or practical applications.

## Steps Taken

1. **Data Preprocessing:**
   - Cleaned data by removing improperly formatted labels (non-alphanumeric characters or labels not of length 9).
   - Split the dataset into training, validation, and testing sets.

2. **Noise Reduction:**
   - Preprocessed images using **Wavelet Denoising** and **Adaptive Thresholding** for enhancment. 
   - Optimized parameters through grid search on the training set to improve image quality.

3. **Image Segmentation:**
   - Applied **Find Contours** and filtered based on **area and aspect ratio** to segment the serial number into individual characters.
   - Removed samples that didn’t have exactly 9 contours, ensuring each character in the serial is captured.

4. **Character Segmentation & Dataset Reconstruction:**
   - Segmented the image into 9 regions corresponding to each character in the serial number.
   - Saved each region as a separate file, with the folder name corresponding to the serial number.
  
6. **Hyperparameters**
   - wavelet type: db1
   - wavelet mode: soft
   - adaptiveThreshold block size: 39
   - adaptiveThreshold C: 15
   - findContours strategy: RETR_EXTERNAL +  CHAIN_APPROX_SIMPLE
   - aspect ratio: ]0.2-1.3[
   - contour minimum area: 9
     
8. **Data Encoding:**
   - Categorical encoding was applied to the labels, with characters encoded as integers from 0 to 35, where 0-9 represent kdigits and 10-35 represent letters.

9. **Model Architecture:**
   - Built and trained a CNN model based on the **MNIST architecture**, consisting of:
     - Two convolutional layers
     - Flatten layer
     - Dense layer for final classification
   - The model was trained on the recognize character images.

10. **Evaluation:**
   - Evaluated the model's performance using **Character Error Rate (CER)** and **Word Error Rate (WER)** on the test set.

11. **Results:**
   - Segmentation
      - Segmetation accuracy for train set: 97.06%
      - Segmetation accuracy for validation set: 95.59%
      - Segmetation accuracy for test set: 97.06%
   - Recognetion my model
      - Recognetion accuracy for train set: 99.33%
      - Recognetion accuracy for train set: 99.32%
      - Average character error rate for test set: 99.32%
      - Average world accuracy for test set: 96.78%
      - By combining segmetation and world accuracies 97.07% x 96.78% = **93.93%** total accuracy for predicting an unkown serial right.
   - Recognetion pretrained models
      - keras OCR average character error rate: 67%
      - Tesseract average character error rate: 88%
    
     

 
