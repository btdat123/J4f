#### **Giới thiệu**

Trong thời đại số, đánh giá của khách hàng là nguồn thông tin vô giá giúp doanh nghiệp hiểu rõ nhu cầu và cải thiện dịch vụ. Tuy nhiên, việc phân tích hàng ngàn đánh giá thủ công là không khả thi.Challenge này yêu cầu bạn xây dựng hệ thống AI để:

* Phân loại đa nhãn (Multi-label Classification): Xác định các khía cạnh mà review đề cập (giải trí, lưu trú, nhà hàng, v.v.)
* Phân tích cảm xúc (Sentiment Analysis): Đánh giá mức độ hài lòng (1-5 sao) cho từng khía cạnh



#### **Metrics đánh giá**

###### 1\. Micro-F1 Score (Multi-label Classification) - Đo lường độ chính xác của việc phân loại đa nhãn:

 			Micro-F1 = 2 × (Precision × Recall) / (Precision + Recall)



Với:

\- Precision = TP / (TP + FP)

\- Recall = TP / (TP + FN)

\- TP: Đúng dự đoán có label

\- FP: Sai dự đoán có label (thực tế không có)

\- FN: Sai dự đoán không có label (thực tế có)

###### 2\. Sentiment Quality Score - Đo lường độ chính xác của điểm sentiment (1-5):

 		Sentiment Score = Độ chính xác trung bình của dự đoán sentiment  (Chỉ tính trên các label mà GT có giá trị > 0)



Ví dụ:

\- GT: giai\_tri=0, luu\_tru=4, nha\_hang=5

\- Pred: giai\_tri=0, luu\_tru=5, nha\_hang=5

→ Chỉ tính luu\_tru và nha\_hang (vì GT > 0)

→ Accuracy = (0 + 1) / 2 = 50%



###### 3\. Điểm Overall:

 				Overall Score = 0.7 × Micro-F1 + 0.3 × Sentiment Quality

#### 

#### **6 Danh mục (Labels)**

giai\_tri : Hoạt động giải trí, vui chơi, du lịch

nha\_hang : Nhà hàng, quán ăn cao cấp

van\_chuyen : Phương tiện di chuyển, giao thông

luu\_tru : Khách sạn, resort, homestay

an\_uong : Đồ ăn, thức uống thường ngày

mua\_sam : Mua sắm, shopping



#### **Quy tắc điểm số:**

• 0: Không liên quan đến danh mục này

• 1: Rất không hài lòng

• 2: Không hài lòng

• 3: Trung bình

• 4: Hài lòng

• 5: Rất hài lòng



#### **Ví dụ cụ thể**

###### **Review mẫu:**

"Khách sạn rất đẹp và sạch sẽ, phòng ốc thoải mái. Nhân viên phục vụ nhiệt tình. Nhà hàng trong khách sạn có món ăn ngon. Tuy nhiên giá cả hơi cao so với chất lượng."



###### **Phân tích Ground Truth:**

Danh mục	Điểm	Giải thích

giai\_tri	0	Không đề cập

luu\_tru	4	Hài lòng (đẹp, sạch, thoải mái)

nha\_hang	4	Hài lòng (món ăn ngon)

an\_uong	0	Không đề cập riêng

van\_chuyen	0	Không đề cập

mua\_sam	0	Không đề cập



###### **Dự đoán của bạn:**

stt,giai\_tri,luu\_tru,nha\_hang,an\_uong,van\_chuyen,mua\_sam

1,0,4,4,0,0,0



###### **Kết quả đánh giá:**

• Classification: Đúng 6/6 labels → Micro-F1 = 1.0 (100%)

• Sentiment: Đúng 2/2 điểm (luu\_tru và nha\_hang) → Accuracy = 1.0 (100%)

• Overall: 0.7 × 1.0 + 0.3 × 1.0 = 1.0 (100%)



#### **Format nộp bài**

Bạn cần nộp 1 file CSV với format sau: 

predictions.csv:

stt,giai\_tri,luu\_tru,nha\_hang,an\_uong,van\_chuyen,mua\_sam

1,0,5,0,0,0,0

2,0,0,4,5,0,0

3,3,0,0,0,0,0

4,0,0,0,0,4,3

...



###### **Lưu ý quan trọng:**

Cột stt: Số thứ tự (1, 2, 3, ...)

6 cột danh mục: Giá trị từ 0 đến 5

Giá trị 0 = không liên quan đến danh mục

Giá trị 1-5 = mức độ hài lòng

File phải có đủ số dòng tương ứng với test set

