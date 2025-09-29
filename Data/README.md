# Quy trình xử lý dữ liệu trước khi huấn luyện mô hình AI  

## 1. Thu thập dữ liệu  

-   **Nguồn ảnh thật**: dataset công khai (FFHQ, CelebA-HQ, LFW...) hoặc tự thu thập bằng camera.  
-   **Nguồn ảnh giả**: model tạo sinh (StyleGAN, Stable Diffusion, FaceForensics++...).  
-   **Yêu cầu**: đa dạng, cân bằng, định dạng đồng nhất (PNG/JPG).  
-   **Ghi nhãn**: thật = 0, giả = 1.  

**Công cụ hỗ trợ**: - `wget`, `kaggle datasets`, `Google Dataset Search` để tải. - `BeautifulSoup`, `Selenium` để crawl web.  

------------------------------------------------------------------------

## 2. Làm sạch dữ liệu  

-   Loại bỏ ảnh mờ, trùng, không có mặt người.  
-   Xử lý ảnh lỗi hoặc metadata thiếu.  

**Thư viện**: - `PIL`, `OpenCV`, `scikit-image` để kiểm tra & xử lý ảnh. - `imagehash` để phát hiện ảnh trùng lặp.  

------------------------------------------------------------------------

## 3. Tiền xử lý dữ liệu  

-   **Face detection & crop**: MTCNN, dlib.  
-   **Resize**: đồng nhất về (224x224 hoặc 256x256).  
-   **Normalization**: RGB, pixel về \[0,1\] hoặc chuẩn hóa theo mean/std (ImageNet chuẩn).  
-   **Augmentation**: xoay, lật, chỉnh sáng/tối để tránh overfitting.  
-   **Loại watermark/text** nếu có.  

**Thư viện**: - `OpenCV`, `PIL` → resize, crop. - `MTCNN`, `dlib` → face detection. - `albumentations`, `torchvision.transforms` → augmentation.  

------------------------------------------------------------------------

## 4. Chuẩn hóa dữ liệu đầu vào

-   Đồng nhất kích thước, hệ màu, giá trị pixel.  
-   Chia train (70%), validation (15%), test (15%).  

**Công cụ**: - `scikit-learn` → train_test_split. - `pandas` để quản lý metadata.  

------------------------------------------------------------------------

## 5. Xử lý đặc trưng nâng cao (tùy chọn)  

-   Heatmap vùng mắt/miệng (Grad-CAM, attention map).  
-   Phân tích miền tần số (FFT, DCT).  
-   Histogram màu/texture.  

**Thư viện**: - `numpy.fft`, `scipy.fftpack` → phân tích miền tần số. - `matplotlib`, `seaborn` → visualization.  

------------------------------------------------------------------------

## 6. Chuẩn bị Data Loader  

-   Tạo batches (vd: 32), shuffle dữ liệu.  
-   Prefetch/cache để tăng tốc training.  

**Thư viện**: - `PyTorch DataLoader` hoặc `tf.data.Dataset` (TensorFlow). - `tqdm` để theo dõi quá trình loading.  

------------------------------------------------------------------------

## 7. Tổng quan pipeline công cụ

-   **Thu thập**: Kaggle API, Selenium, wget.  
-   **Làm sạch**: OpenCV, imagehash.  
-   **Tiền xử lý**: MTCNN, albumentations, torchvision.  
-   **Chuẩn hóa**: scikit-learn, pandas.  
-   **Đặc trưng nâng cao**: numpy.fft, matplotlib.  
-   **DataLoader**: PyTorch, TensorFlow.  

# Cấu trúc thư mục Data  
---
|-Data  
    |-Train  
        |-Real  
        |-Fake  
    |-Test  
        |-Real  
        |-Fake  
    |-Validation  