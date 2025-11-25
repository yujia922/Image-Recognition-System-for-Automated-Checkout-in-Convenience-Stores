# Image-Recognition-System-for-Automated-Checkout-in-Convenience-Stores
清大小吃部便利商店於下課時間的排隊結帳人流量大，常常也因為排隊人潮導致耽誤上課的時間。若我們能加速結帳的時間，就以快速消耗掉人潮，甚至能節省超商人力。去年39組做了飲料方面的辨識，若我們能進一步擴大種類，在未來將可以實現影像辨識快速結帳的功能。因此我們組打算從餅乾(洋芋片)類型開始做起，並延伸計算照片內所有商品的總額。
## Technical Approach
This project aims to build an automated checkout system for convenience stores using computer vision. We will focus on snack products (especially chips) as the main category.
### 1. Data Collection
We collect a large set of real-world images of convenience-store snack products. The goal is to replicate a realistic scenario in which a customer places multiple items on a table and captures a single image for instant checkout.
Our dataset includes:
- 47 distinct snack products
- Multiple brands, sizes, packaging variations
- Single-item and multi-item images
- Varying lighting and backgrounds

總計"47"項餅乾種類如下:
- 樂事自然美味海鹽口味洋芋片 $35
- 樂事大波浪椒香嫩雞口味洋芋片 $35
- 樂事神戶厚切牛排口味洋芋片 $35
- 樂事炙鹽香蒜口味洋芋片 $35
- 樂事極品香煎干貝口味洋芋片 $35
- 樂事地獄辛辣拉麵口味洋芋片 $35
- 樂事美國經典原味洋芋片 $35
- 樂事瑞士香濃起司口味洋芋片 $35
- 樂事九州岩燒海苔洋芋片 $35
- 樂事頂級日曬甘味湖鹽口味 $35
- 樂事宮城仙台和牛口味洋芋片 $35
- 樂事波樂香烤肋排口味洋芋片 $35
- 多力多滋美式BBQ豬肋排味玉米片 $35
- 多力多滋勁辣香檸口味與米片 $35
- 多力多滋蒜味牛菲力口味玉米片 $35
- 多力多滋美式辣起士口味玉米片 $35
- 多力多滋爆蒜鮮蝦口味 $35
- 多力多滋黃金起司味玉米片 $35
- 多力多滋超濃起司味玉米片 $35
- 卡辣姆久厚切洋芋片極辛口味 $55
- 卡辣姆久平切洋芋片卡辣海苔口味 $35
- 卡辣姆久平切洋芋片勁辣唐辛子口味 $35
- 湖池屋酥卡玉米脆棒烤鮮蝦 $35
- 湖池屋蘇卡玉米脆棒極致和風醬燒口味 $35
- 波的多洋芋片薄片 (蚵仔煎口味) $35
- 波的多洋芋片 (蚵仔煎口味) $35
- 華元鹹蔬餅 $35
- 華元真魷味紅燒口味 $35
- 乖乖玉米脆條香辣 $30
- 乖乖椰子大 $30
- 乖乖五香大 $30
- 可樂果豌豆酥(酷辣)大 $30
- 可樂果JUMBO正港蒜味豌豆酥 $45
- 可樂果豌豆酥大 $30
- 卡迪那洋芋片牛排口味 $35
- 卡迪那寶卡卡口味 $30
- 卡迪那德州薯條茄汁口味 $45
- 星太郎超寬條餅-雞汁口味 $39
- 星太郎點心麵-大雞汁 $39
- 浪味仙-熔岩辣起司口味(洋芋捲) $30
  浪味仙-田園蔬菜口味 $30
- 奇多家常起司口味玉米棒 $35
- 奇多兩倍濃起司口味玉米棒 $35
- 滿天星原味 $45
- 孔雀香酥脆-香魚 $30
- 蝦味先原味 $32
- 北海鱈魚香絲 $50
   
### 2. Labeling & Price Annotation
After data collection, we will annotate each individual product instance using a bounding-box based labeling tool (i.e. RoboFlow).
For each label, we will record:
- product class (brand / variant)
- product unit price
This allows the inference pipeline to not only detect the bounding-boxes, but also sum the total value in the image automatically.
Annotation format will follow YOLO format (.txt per image).
### 3. Model Training
We will train the object detection model using PyTorch + YOLOv8.
Key steps:
- train/val/test split
- augmentation (random crop, brightness, hue, blur)
- model training with transfer learning (pretrained YOLOv8 weights)
- performance evaluation (mAP, precision, recall)
### 4. Inference & Checkout Calculation
Given an image (e.g. a table with multiple snacks lying on it), the trained model will output all detected products.
Then, we will sum the prices of all detected objects to generate the final total checkout amount.
- 利用手機app DroidCam 讓手機鏡頭作為影像辨識的鏡頭
