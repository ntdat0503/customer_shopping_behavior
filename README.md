#  Customer Shopping Behavior

Dự án phân tích dữ liệu hành vi mua sắm của khách hàng sử dụng **Python**, **MySQL** và **Power BI**.

---

## Tổng quan dự án

Dự án khám phá bộ dữ liệu khách hàng bán lẻ nhằm rút ra các insight về xu hướng mua sắm, doanh thu, phân khúc khách hàng và hiệu suất sản phẩm. Phân tích được thực hiện theo quy trình end-to-end chuẩn ngành — từ dữ liệu thô đến dashboard tương tác.

---

## Cấu trúc Repository

```
customer-shopping-behavior/
│
├── data/
│   ├── customer_shopping_behavior.csv        # Dữ liệu thô
│   └── customer_shopping_behavior_full.csv   # Dữ liệu đã làm sạch & xử lý
│
├── python/
│   └── Customer_shopping_behavior.ipynb      # Notebook làm sạch dữ liệu & EDA
│
├── sql/
│   └── project_customer_shopping_behavior.sql  # Các câu truy vấn SQL
│
├── dashboard/
│   └── customer_behavior_dashboard.png       # Ảnh chụp dashboard Power BI
│
└── README.md
```

---

## Công cụ & Công nghệ

| Công cụ | Mục đích |
|---|---|
| Python (Pandas) | Làm sạch dữ liệu, EDA, tạo đặc trưng |
| MySQL | Lưu trữ dữ liệu & phân tích SQL |
| Power BI | Dashboard tương tác & trực quan hóa |
| GitHub | Quản lý phiên bản & lưu trữ portfolio |

---

## Quy trình thực hiện

```
01 Xác định vấn đề kinh doanh
        ↓ Import dữ liệu vào Python
02 Mô hình hóa dữ liệu & EDA trong Python
        ↓ Load vào cơ sở dữ liệu SQL
03 Phân tích dữ liệu bằng SQL
        ↓ Kết nối với Power BI
04 Xây dựng Dashboard tương tác bằng Power BI
        ↓ Tổng hợp kết quả
05 Báo cáo dự án (README này)
```

---

## Bước 1 — Python: Làm sạch dữ liệu & EDA

**File:** `python/Customer_shopping_behavior.ipynb`

Các bước thực hiện:

- Đọc file CSV thô, kiểm tra shape, kiểu dữ liệu và thống kê mô tả
- Xử lý giá trị thiếu trong cột `review_rating` bằng cách điền **median theo từng category**
- Chuẩn hóa tên cột (chữ thường, dấu gạch dưới, đổi tên `purchase_amount_(usd)` → `purchase_amount`)
- Tạo các đặc trưng mới:
  - `age_group` — phân nhóm khách hàng thành 4 nhóm tuổi bằng `pd.qcut`: Young Adult, Adult, Middle-aged, Senior
  - `purchase_frequency_days` — chuyển tần suất mua hàng dạng chữ (Weekly, Monthly...) sang số ngày
- Kiểm tra và xác nhận cột `discount_applied` và `promo_code_used` có giá trị hoàn toàn giống nhau
- Xuất bộ dữ liệu đã xử lý thành file `customer_shopping_behavior_full.csv`

---

## Bước 2 — MySQL: Phân tích dữ liệu

**File:** `sql/project_customer_shopping_behavior.sql`

### Các câu hỏi kinh doanh được trả lời:

| # | Câu hỏi |
|---|---|
| Q1 | Tổng doanh thu theo giới tính |
| Q2 | Khách hàng dùng discount nhưng vẫn chi tiêu trên mức trung bình |
| Q3 | Top 5 sản phẩm có rating trung bình cao nhất |
| Q4 | So sánh giá trị mua hàng trung bình: Standard vs Express shipping |
| Q5 | Khách hàng có subscription có chi tiêu nhiều hơn không? |
| Q6 | Top 5 sản phẩm có tỷ lệ áp dụng discount cao nhất |
| Q7 | Phân khúc khách hàng: New / Returning / Loyal |
| Q8 | Top 3 sản phẩm được mua nhiều nhất trong từng danh mục |
| Q9 | Khách hàng mua lại nhiều có xu hướng đăng ký subscription không? |
| Q10 | Đóng góp doanh thu theo từng nhóm tuổi |

### Kỹ thuật SQL sử dụng:
- Hàm tổng hợp (`SUM`, `AVG`, `COUNT`, `ROUND`)
- Subquery
- Câu lệnh `CASE WHEN`
- CTE (`WITH`)
- Window function (`ROW_NUMBER() OVER PARTITION BY`)

---

## Bước 3 — Power BI: Dashboard tương tác

**File:** `dashboard/customer_behavior_dashboard.png`

### Tính năng Dashboard:

**KPI Cards (hàng trên cùng):**
- Tổng doanh thu: $233.08K
- Giá trị mua hàng trung bình: $59.76
- Tổng khách hàng: 3.90K
- Rating trung bình: 3.75 / 5
- Doanh thu từ subscription: $62.65K

**Biểu đồ:**
- Phân chia theo giới tính (Donut chart)
- Số lượng khách hàng theo tuổi (Bar chart)
- Khách hàng có/không có subscription (Pie chart)
- Doanh số & Doanh thu theo nhóm tuổi (Area + Bar chart)
- Doanh số & Doanh thu theo danh mục (Area + Bar chart)
- Top 5 sản phẩm theo doanh thu (Bar chart)
- Top 5 sản phẩm có rating cao nhất (Table)

**Slicer lọc tương tác:**
- Trạng thái subscription
- Giới tính
- Danh mục sản phẩm
- Nhóm tuổi

---

## Mô tả Dataset

**Nguồn:** Customer Shopping Behavior Dataset

| Cột | Mô tả |
|---|---|
| customer_id | Mã định danh khách hàng |
| age | Tuổi khách hàng |
| gender | Nam / Nữ |
| item_purchased | Tên sản phẩm |
| category | Danh mục sản phẩm (Clothing, Footwear, Accessories, Outerwear) |
| purchase_amount | Giá trị mua hàng (USD) |
| review_rating | Đánh giá sản phẩm (1–5) |
| subscription_status | Có subscription hay không (Yes/No) |
| discount_applied | Có dùng discount hay không (Yes/No) |
| previous_purchases | Số lần mua hàng trước đó |
| age_group | Cột tạo mới: Young Adult / Adult / Middle-aged / Senior |
| purchase_frequency_days | Cột tạo mới: Tần suất mua hàng (số ngày) |

---

## Kết quả & Insights chính

- **Khách hàng nữ** chiếm 68% tổng số khách hàng và đóng góp phần lớn doanh thu
- **Young Adults** tạo ra doanh thu cao nhất trong tất cả các nhóm tuổi
- **Clothing** là danh mục bán chạy nhất cả về doanh số lẫn doanh thu
- **Khách hàng có subscription** đóng góp $62.65K — khoảng 27% tổng doanh thu
- **Blouse, Shirt và Dress** là 3 sản phẩm có doanh thu cao nhất
- **Gloves** có rating trung bình cao nhất (3.86 / 5)

---

## Hướng dẫn chạy dự án

### Python
```bash
pip install pandas jupyter
jupyter notebook python/Customer_shopping_behavior.ipynb
```

### MySQL
```sql
-- Tạo database và bảng, sau đó import file customer_shopping_behavior_full.csv
-- Chạy các câu truy vấn trong file sql/project_customer_shopping_behavior.sql
```

### Power BI
- Mở Power BI Desktop
- Kết nối với MySQL database
- Load bảng `customer_behavior`
- Xây dựng các visual theo mô tả trong phần dashboard

---
