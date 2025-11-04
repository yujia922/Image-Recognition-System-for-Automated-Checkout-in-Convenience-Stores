# Image-Recognition-System-for-Automated-Checkout-in-Convenience-Stores
清大小吃部便利商店於下課時間的排隊結帳人流量大，常常也因為排隊人潮導致耽誤上課的時間。若我們能加速結帳的時間，就以快速消耗掉人潮，甚至能節省超商人力。去年39組做了飲料方面的辨識，若我們能進一步擴大種類，在未來將可以實現影像辨識快速結帳的功能。因此我們組打算從餅乾(洋芋片)類型開始做起，並延伸計算照片內所有商品的總額。
## Technical Approach
This project aims to build an automated checkout system for convenience stores using computer vision. We will focus on snack products (especially chips) as the main category.
### 1. Data Collection
We will photograph a large number of actual convenience store snack items across different shelves, lighting conditions, and angles.
The objective is to simulate a realistic “put items on table → take one photo → auto checkout” scenario.
We plan to collect images that reflect:
- multiple brands of chips
- different packaging sizes / colors / variants
- multiple products in a single frame
- occlusion cases (items overlapping)
### 2. Labeling & Price Annotation
After data collection, we will annotate each individual product instance using a bounding-box based labeling tool (i.e. RoboFlow).
For each label, we will record:
- product class (brand / variant)
- product unit price
This allows the inference pipeline to not only detect the bounding-boxes, but also sum the total value in the image automatically.
Annotation format will follow YOLO format (.txt per image).
### 3. Model Training
We will train the object detection model using PyTorch + YOLOv11.
Key steps:
- train/val/test split
- augmentation (random crop, brightness, hue, blur)
- model training with transfer learning (pretrained YOLOv11 weights)
- performance evaluation (mAP, precision, recall)
### 4. Inference & Checkout Calculation
Given an image (e.g. a table with multiple snacks lying on it), the trained model will output all detected products.
Then, we will sum the prices of all detected objects to generate the final total checkout amount.
