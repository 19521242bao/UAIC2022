

# UAIC2022-DeadlineKLTN
Nhóm sử dụng mô hình ABCnet cho giai đoạn detection và VietOCR+vedastr cho giai đoạn recognition (mô hình phân loại arttext do sử dụng không hiệu quả nên đã bị bỏ đi)

## 1. Setup môi trường:
Đầu tiên ta cần cài đặt torch với cuda11.1
```
pip install torch==1.10.0+cu111 torchvision==0.11.0+cu111 torchaudio==0.10.0 -f https://download.pytorch.org/whl/torch_stable.html
```

Cài  đặt detectron2
```
git clone https://github.com/facebookresearch/detectron2.git
cd detectron2
git checkout 9eb4831f742ae6a13b8edb61d07b619392fb6543
python -m pip install -e detectron2
```

Install các thư viện cần thiết khác
```
pip install -r requirements.txt
```
Cài đặt text detection
```
cd ABCnet
rm -rf build
python3 setup.py build develop
```

## 2. Chuẩn bị 
Trước khi tiến hành inference, vui lòng để toàn bộ hình ảnh cần được đánh giá vào thư mục `data/public_test_images`
Trước khi tiến hành  inference vui lòng để dữ liệu hình ảnh vào thư mực `datasets/` (ví dụ nếu là tập private test thì đường dẫn tới ảnh của private test sẽ là `datasets/uaic2022_private_test/images/ `)
Để tải mô hình đã được huấn luyện ta chỉ cần chạy lệnh sau
```
cd weights
bash down_weights.sh
```
## 3. Chạy Inference



Sau đó tiến hành chạy inference bằng cách chỉnh sửa đường ảnh trong file `run.sh` (thay `data_dir` ứng với dữ liệu cần chạy )

```
bash run.sh
```
Sau đó ta sẽ tạo file để nộp từ folder submision
```
cd submision
zip -r -D predicted.zip *
```
sẽ lưu trong folder submision file predicted.zip

Ngoài ra nhóm có cung cấp một file notebook inference_UAIC.ipynb ví dụ cho việc inference trên tập private test

https://colab.research.google.com/drive/1ymmU6GVkqqoYq7x5COnCjrPLj1V9AJL4?usp=sharing




