#### **Giới thiệu**

Polyp là những khối u nhỏ phát triển trên niêm mạc đại tràng. Việc phát hiện và loại bỏ polyp sớm là rất quan trọng trong việc ngăn ngừa ung thư đại tràng. Trong challenge này, nhiệm vụ của bạn là xây dựng mô hình phân đoạn (segmentation)tự động để xác định vị trí chính xác của polyp trong ảnh nội soi đại tràng.



###### **Mục tiêu:**

* Nhận diện chính xác vùng polyp trong ảnh
* Tạo mask binary phân đoạn polyp với background
* Đạt độ chính xác cao nhất có thể (IoU score)



#### **Metrics đánh giá**

###### 1\. IoU (Intersection over Union) - Đo lường độ chồng lấp giữa mask dự đoán và mask ground truth:



&nbsp;		IoU = (Diện tích giao nhau) / (Diện tích hợp)

&nbsp;		IoU = |Pred ∩ GT| / |Pred ∪ GT| = (số pixel giao nhau) / (số pixel hợp)

Ví dụ:

\- Pred có 100 pixel trắng

\- GT có 120 pixel trắng  

\- Giao nhau: 80 pixel

\- Hợp: 100 + 120 - 80 = 140 pixel

→ IoU = 80 / 140 = 0.571 (57.1%)



###### 2\. Dice Coefficient - Metric phụ để tham khảo (không dùng để xếp hạng):

&nbsp;		Dice = 2 × (Diện tích giao nhau) / (Tổng diện tích)

###### 

###### 3\. Điểm Overall:

&nbsp;		Overall Score = IoU



#### **Ví dụ cụ thể**

###### Scenario: Bạn nộp bài với 3 ảnh

1. Ảnh 1.png:

• GT mask: 1000 pixels polyp

• Your mask: 900 pixels polyp

• Giao nhau: 850 pixels

• Hợp: 1000 + 900 - 850 = 1050 pixels

→ IoU = 850/1050 = 0.810



2\. Ảnh 2.png:

• GT mask: 1500 pixels polyp

• Your mask: 1400 pixels polyp

• Giao nhau: 1300 pixels

• Hợp: 1500 + 1400 - 1300 = 1600 pixels

→ IoU = 1300/1600 = 0.813



3\. Ảnh 3.png:

• GT mask: 800 pixels polyp

• Your mask: 600 pixels polyp

• Giao nhau: 550 pixels

• Hợp: 800 + 600 - 550 = 850 pixels

→ IoU = 550/850 = 0.647



Overall Score = (0.810 + 0.813 + 0.647) / 3 = 0.757 (75.7%)



#### **Format nộp bài**

Bạn chỉ cần nộp 1 file ZIP chứa các mask dự đoán:

pred\_mask.zip

├── 1.png

├── 2.png

├── 3.png

└── ...



###### **Lưu ý:**

\- Tên file mask phải trùng với tên file ảnh test

\- Format: PNG grayscale hoặc binary

\- Pixel trắng (>127): vùng polyp

\- Pixel đen (≤127): vùng background



###### **Lưu ý quan trọng:**

Không cần file predictions.csv (chỉ cần masks)

Kích thước mask phải giống với ảnh gốc

Nếu thiếu mask cho ảnh nào đó → điểm IoU = 0 cho ảnh đó

