# Quy trình xây dựng và huấn luyện mô hình CNN

## 1. Chuẩn bị dữ liệu

-   Dữ liệu đã được xử lý & chuẩn hóa từ pipeline trước (ảnh thật vs ảnh giả).  
-   Chia train (70%), validation (15%), test (15%).  
-   Sử dụng DataLoader (PyTorch) hoặc tf.data.Dataset (TensorFlow).  

**Thư viện**: PyTorch, TensorFlow, torchvision, albumentations.  

## 2. Xây dựng mô hình CNN

**Kiến trúc CNN cơ bản**:  
    -   Conv2D → ReLU → MaxPooling → Dropout.  
    -   Lặp lại nhiều tầng để trích xuất đặc trưng.  
    -   Flatten → Fully Connected → Softmax/Sigmoid.  
**Lựa chọn kiến trúc nâng cao** (nếu cần): ResNet, EfficientNet,MobileNet.  

**Thư viện**: PyTorch (nn.Module, torch.nn.Conv2d), TensorFlow/Keras(Sequential, Conv2D).  

## 3. Thiết lập huấn luyện

-   **Loss function**: Binary Cross-Entropy (ảnh thật vs giả).  
-   **Optimizer**: Adam, SGD, RMSprop.  
-   **Learning rate**: thường 1e-3 → 1e-5.  
-   **Batch size**: 32 hoặc 64.  
-   **Epochs**: 20--100 tùy dataset.  

**Thư viện**: torch.optim, tf.keras.optimizers.  

## 4. Training Loop

-   Với PyTorch:  
    -   Forward pass → tính loss → backward pass → update weights.  
    -   Theo dõi loss/accuracy sau mỗi epoch.  
-   Với TensorFlow/Keras:  
    -   model.fit() với callback (EarlyStopping, ReduceLROnPlateau).

**Công cụ hỗ trợ**: tqdm (progress bar), TensorBoard (log).  

## 5. Validation & Hyperparameter Tuning

-   Kiểm tra accuracy, precision, recall, F1-score trên validation set.  
-   Điều chỉnh learning rate, batch size, depth của CNN.  
-   Sử dụng cross-validation nếu dataset nhỏ.  

**Thư viện**: scikit-learn (classification_report, confusion_matrix).  

## 6. Đánh giá trên Test Set

-   Đo lường final accuracy, ROC-AUC.  
-   Vẽ confusion matrix, ROC curve.  
-   So sánh với baseline/random guess.  

**Thư viện**: matplotlib, seaborn.  

## 7. Triển khai mô hình

-   Lưu mô hình (PyTorch: .pt, TensorFlow: .h5 hoặc SavedModel).  
-   Dùng cho inference trên ảnh mới.  
-   Tích hợp vào ứng dụng (API Flask/FastAPI hoặc app di động).  

**Thư viện**: torch.save, tf.keras.models.save_model, Flask, FastAPI.  

## 8. Tổng quan pipeline công cụ

-   **Chuẩn bị dữ liệu**: torchvision, albumentations, tf.data.  
-   **Xây dựng CNN**: PyTorch nn.Module, Keras Sequential.  
-   **Huấn luyện**: torch.optim, keras optimizers, TensorBoard.  
-   **Validation**: scikit-learn, matplotlib.  
-   **Triển khai**: Flask, FastAPI, TorchScript, TensorFlow Lite.  
