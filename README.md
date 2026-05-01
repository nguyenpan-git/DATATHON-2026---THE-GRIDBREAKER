# DATATHON 2026 - THE GRIDBREAKER
# Breaking Business Boundaries
# Hosted by VinTelligence

| Thành viên         |
|------------------- |
| Đào Đức Thịnh      |
| Nguyễn Văn Phúc An |
| Võ Nhật Tiến       |
| Hoàng Thụy Hồng Ân | 

# TỔNG QUAN BÀI TOÁN
Bộ dữ liệu mô phỏng hoạt động của một doanh nghiệp thời trang thương mại điện tử tại Việt Nam (04/07/2012 - 31/12/2022). Bài toán yêu cầu hai nhiệm vụ chính:

1. **Trực quan hoá & Phân tích (EDA):** Khám phá dữ liệu để tìm ra các insight có ý nghĩa kinh doanh, đánh giá từ mức độ mô tả (Descriptive) đến đề xuất hành động (Prescriptive).
2. **Dự báo Doanh thu (Sales Forecasting):** Xây dựng mô hình học máy để dự báo cột `Revenue` và `COGS` trong khoảng thời gian từ 01/01/2023 đến 01/07/2024.

- **Các mô hình được sử dụng:**
    - [Điền tên mô hình...]
- **Phương pháp giải thích mô hình (Explainability):**
    - [Điền phương pháp...]
- **Chỉ số đánh giá (Metrics):** MAE, RMSE, R²-score.

## Mục lục
1. [Cấu trúc Repository](#1-cấu-trúc-repository)
2. [Cài đặt](#2-cài-đặt)
3. [Cách sử dụng](#3-cách-sử-dụng)
4. [Mô tả Dữ liệu](#4-mô-tả-dữ-liệu)
5. [Kết quả](#5-kết-quả)

---

## 2. Cấu trúc repo

```
DATATHON-2026/
├── report/                  # Chứa dashboard và báo cáo phân tích
├── notebooks/               # Source code phân tích và mô hình (.ipynb)
├── src/                     # Source code dạng script (.py) phục vụ pipeline
├── outputs/                 # Chứa file nộp Kaggle (submission.csv)
├── requirements.txt         # Thư viện môi trường
└── README.md
```
---

## 2. Cài đặt
### 2.1. Clone repository:
Nếu muốn chạy code trên máy tính cục bộ, dùng lệnh bên dưới để tải thư mục code về máy và vào trong thư mục đó rồi mới bắt đầu chạy các file Notebook.
```bash
git clone https://github.com/nguyenpan-git/DATATHON-2026---THE-GRIDBREAKER.git
cd DATATHON-2026---THE-GRIDBREAKER
```
### 2.2. Cài đặt thư viện
Đảm bảo đang sử dụng Python 3.8+.
```bash
pip install --upgrade pip
pip install -r requirements.txt
```
---

## 3. Cách sử dụng (thư mục notebooks)
### 3.1. Phân tích Khám phá Dữ liệu (EDA)
Toàn bộ mã nguồn khám phá dữ liệu tổng quan, làm sạch bước đầu và vẽ biểu đồ được đặt trong:

* **File:** `EDA_1.ipynb`
* **File:** `EDA_2.ipynb`

  * **Mô tả:** Thực hiện nạp dữ liệu, làm sạch bước đầu, xử lý dữ liệu bị thiếu (missing values) và trực quan hóa các thông tin cơ bản.

### 3.2. Phân tích Chuyên sâu (In-depth Analysis)
Dựa trên kết quả từ quá trình EDA, các phân tích chi tiết theo từng khía cạnh kinh doanh được đặt trong các file sau:

* **File:** `Revenue_Analysis.ipynb`
  * **Mô tả:** Phân tích doanh thu, tập trung vào việc bóc tách các yếu tố mang lại lợi nhuận cho mô hình kinh doanh.
* **File:** `DefectiveProduct_Logistic_Analysis.ipynb`
  * **Mô tả:** Phân tích tỷ lệ sản phẩm lỗi (Defect rates) và các rủi ro, thời gian liên quan đến khâu vận chuyển (Logistics).
* **File:** `Performance_SupplyChain_Operations_Analysis.ipynb`
  * **Mô tả:** Đánh giá hiệu suất vận hành tổng thể của chuỗi cung ứng.

### 3.3. Huấn luyện Mô hình
Mã nguồn trích xuất đặc trưng (Feature Engineering), huấn luyện và tối ưu mô hình:

* **File:** `VinUniModel.ipynb`
  * **Đầu ra:** File dự đoán cuối cùng được lưu tại outputs/submissions/submission.csv với đúng format yêu cầu của Kaggle.

---

## 4. Mô tả Dữ liệu
- Nguồn: [Kaggle - DATATHON 2026 - Vòng Sơ loại](https://www.kaggle.com/competitions/datathon-2026-round-1/data)

Bộ dữ liệu được cung cấp bao gồm 15 files CSV về hoạt động của doanh nghiệp, được chia thành 4 lớp dữ liệu chính.

| Lớp dữ liệu | Danh sách bảng | Nội dung chính |
| :--- | :--- | :--- |
| **Master** | `products.csv`, `customers.csv`, `promotions.csv`, `geography.csv` | Thông tin tham chiếu cốt lõi: Danh mục sản phẩm, thông tin khách hàng, các chiến dịch khuyến mãi và phân bổ địa lý. |
| **Transaction** | `orders.csv`, `order_items.csv`, `payments.csv`, `shipments.csv`, `returns.csv`, `reviews.csv` | Lịch sử giao dịch chi tiết: Đơn đặt hàng, chi tiết từng dòng sản phẩm, thanh toán, quá trình vận chuyển, hàng hoàn trả và đánh giá của khách hàng. |
| **Operational** | `inventory.csv`, `inventory_enhanced.csv`, `web_traffic.csv` | Dữ liệu vận hành thực tế: Ảnh chụp tồn kho cuối tháng, các chỉ số tồn kho mở rộng và lưu lượng người dùng truy cập website hàng ngày. |
| **Analytical** | `sales.csv` (Train), `sales_test.csv` (Test) | Dữ liệu tổng hợp doanh thu phục vụ trực tiếp cho bài toán huấn luyện và dự báo. |

**Thông tin bài toán Dự báo (Forecasting):**
- **Biến mục tiêu (Target Variable):** `Revenue` (Tổng doanh thu thuần).
- **Đơn vị dự báo:** Tổng doanh thu và giá vốn (`COGS`) theo từng ngày (`Date`).
                      |
---
