## Dữ liệu Training - Polyp Segmentation

### Cấu trúc thư mục

```
data/polyp/train/
├── train.zip          # File nén chứa toàn bộ dữ liệu training
├── images/            # Thư mục chứa ảnh nội soi đại tràng gốc
│   ├── 1.png
│   ├── 2.png
│   └── ...
└── masks/             # Thư mục chứa mask ground truth tương ứng
    ├── 1.png
    ├── 2.png
    └── ...
```

### Mô tả dữ liệu

**Mục đích:** Dữ liệu training để sinh viên phát triển mô hình phân đoạn polyp trong ảnh nội soi đại tràng.

**Nội dung:**
- **images/**: Chứa ảnh nội soi đại tràng dạng PNG
  - Tất cả ảnh đều chứa polyp (khối u lành tính)
  - Format: `.png`
  - Tên file: số thứ tự (1.png, 2.png, ...)

- **masks/**: Chứa mask binary ground truth
  - Mỗi mask tương ứng với 1 ảnh (cùng tên file)
  - Pixel trắng (255): vùng có polyp
  - Pixel đen (0): vùng nền
  - Format: `.png` grayscale

**Cặp dữ liệu:**
```
images/1.png  ←→  masks/1.png
images/2.png  ←→  masks/2.png
...
```

### Hướng dẫn sử dụng

**Cho sinh viên:**
1. Download file `train.zip` hoặc truy cập thư mục `images/` và `masks/`
2. Sử dụng cặp (image, mask) để training mô hình segmentation
3. Mục tiêu: Dự đoán mask cho ảnh test (public/private)
4. Đánh giá: IoU (Intersection over Union) và Dice Coefficient

**Lưu ý:**
- Tất cả ảnh trong bộ dữ liệu này đều có polyp (không có ảnh normal)
- Mask là binary: polyp (trắng) vs background (đen)
- Kích thước ảnh và mask phải giống nhau

### Ví dụ sử dụng (Python)

```python
from PIL import Image
import numpy as np

# Load image và mask
image = Image.open('data/polyp/train/images/1.png')
mask = Image.open('data/polyp/train/masks/1.png').convert('L')

# Convert to numpy
img_array = np.array(image)
mask_array = np.array(mask)

# Binary mask: 0 hoặc 255
mask_binary = (mask_array > 127).astype(np.uint8)
```