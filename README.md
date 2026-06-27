# California Housing Regression
Trần Việt Hà - 25C23020

Link repo: https://github.com/hatran347/California_Housing

## Giới thiệu

Dự án này thực hiện phân tích dữ liệu và xây dựng mô hình dự báo giá nhà trung vị tại California dựa trên bộ dữ liệu California Housing.

Mục tiêu chính của bài làm là so sánh hiệu quả dự báo của các mô hình hồi quy tuyến tính và hồi quy điều chuẩn.

## Bộ dữ liệu

Bộ dữ liệu California Housing gồm 20,640 quan sát, mô tả đặc điểm nhà ở tại các khu vực điều tra dân số (census block groups) thuộc bang California, dựa trên dữ liệu điều tra dân số năm 1990.

Các biến trong bộ dữ liệu gồm:

1. `longitude`: đo lường vị trí về phía Tây của khu vực; giá trị càng lớn thì càng xa về phía Tây.
2. `latitude`: đo lường vị trí về phía Bắc của khu vực; giá trị càng lớn thì càng xa về phía Bắc.
3. `housing_median_age`: tuổi trung vị của nhà trong một khu vực; giá trị thấp hơn thể hiện khu vực có nhà mới hơn.
4. `total_rooms`: tổng số phòng trong một khu vực.
5. `total_bedrooms`: tổng số phòng ngủ trong một khu vực.
6. `population`: tổng số người sinh sống trong một khu vực.
7. `households`: tổng số hộ gia đình trong một khu vực.
8. `median_income`: thu nhập trung vị của các hộ gia đình trong khu vực, được đo bằng đơn vị chục nghìn USD.
9. `median_house_value`: giá nhà trung vị của các hộ gia đình trong khu vực, được đo bằng USD. Đây là biến mục tiêu cần dự đoán.
10. `ocean_proximity`: vị trí của khu vực so với biển, gồm các nhóm `<1H OCEAN`, `INLAND`, `ISLAND`, `NEAR BAY` và `NEAR OCEAN`.

Lưu ý: Mỗi quan sát không đại diện cho một căn nhà riêng lẻ mà đại diện cho một khu vực điều tra dân số. Do đó, các biến như `total_rooms`, `population` hay `households` là các số liệu tổng hợp ở cấp độ khu vực.
## Các bước thực hiện

Bài làm gồm các bước chính:

1. Tiền xử lý dữ liệu
2. Kiểm tra missing value, duplicate và outlier
3. Phân tích phân phối biến mục tiêu và các biến giải thích
4. Phân tích tương quan và kiểm tra đa cộng tuyến bằng VIF
5. Tạo thêm biến Feature Engineering
6. Chia dữ liệu thành train set và validation set
7. Xây dựng các mô hình dự báo
8. Đánh giá và lựa chọn mô hình phù hợp nhất

## Feature Engineering

Một số biến mới được tạo thêm để chuẩn hóa thông tin theo quy mô hộ gia đình:

* `rooms_per_household`
* `bedrooms_per_room`
* `population_per_household`

Các biến này giúp bổ sung thông tin về cấu trúc nhà ở và mức độ đông đúc của từng khu vực.

## Mô hình sử dụng

Các mô hình được xây dựng và so sánh gồm:

* OLS Regression
* Ridge Regression
* LASSO Regression
* Elastic Net Regression

Đối với Ridge, LASSO và Elastic Net, 5-fold Cross Validation được sử dụng trên tập train để lựa chọn tham số điều chuẩn tối ưu.

## Chỉ số đánh giá

Các mô hình được đánh giá trên tập validation bằng các chỉ số:

* RMSE
* MAE
* MAPE
* R²

## Kết quả chính

Kết quả cho thấy các mô hình sử dụng Feature Engineering cho hiệu quả dự báo tốt hơn so với các mô hình chỉ dùng biến ban đầu.

Trong các mô hình được so sánh, LASSO với Feature Engineering cho kết quả tốt nhất trên tập validation. Do đó, mô hình này được lựa chọn là mô hình phù hợp nhất trong bài làm.

## File trong repository

* `HT.Rmd`: file RMarkdown chứa toàn bộ code và nội dung báo cáo
* `HT.pdf`: báo cáo kết quả cuối cùng
* `California_housing.csv`: dữ liệu sử dụng trong bài làm

## Công cụ sử dụng

```r
library(tidyverse)
library(corrplot)
library(broom)
library(knitr)
library(maps)
library(viridis)
library(scales)
library(GGally)
library(car)
library(glmnet)

