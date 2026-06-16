#  Báo Cáo Kiểm Thử Hiệu Năng (JMeter Performance Testing)

Dự án này thực hiện kiểm tra và đánh giá hiệu năng chịu tải của các hệ thống bằng công cụ **Apache JMeter**[cite: 1]. Mục tiêu chính là đo lường mức độ ổn định, thời gian phản hồi và khả năng xử lý của máy chủ dưới áp lực của hàng loạt người dùng truy cập đồng thời.

---

##  Mục lục
1. [Giới thiệu chung](#1-giới-thiệu-chung)
2. [Kiểm thử Hiệu năng Website (Web Performance)](#2-kiểm-thử-hiệu-năng-website-web-performance)
3. [Kiểm thử Hiệu năng API (API Performance)](#3-kiểm-thử-hiệu-năng-api-api-performance)
4. [Tổng kết & Đánh giá](#4-tổng-kết--đánh-giá)

---

## 1. Giới thiệu chung

Dự án tập trung vào hai đối tượng kiểm thử chính:
*   **Hệ thống Website:** Giao diện người dùng của trường Đại học Phenikaa (`https://phenikaa-uni.edu.vn/vi`)[cite: 1].
*   **Hệ thống API:** Dịch vụ cung cấp dữ liệu thời tiết của OpenWeatherMap (`https://openweathermap.org/current`)[cite: 1].

**Mục tiêu của dự án bao gồm:**
*   Sử dụng JMeter để thiết lập kịch bản giả lập người dùng truy cập[cite: 1].
*   Thực thi kịch bản và thu thập dữ liệu hệ thống[cite: 1].
*   Phân tích các chỉ số trọng yếu: Thời gian phản hồi (Response Time), số lượng yêu cầu thành công/thất bại[cite: 1].
*   Đưa ra kết luận khách quan về năng lực của hệ thống[cite: 1].

---

## 2. Kiểm thử Hiệu năng Website (Web Performance)

### 2.1. Cấu hình Kịch bản (Test Scenario)

| Thành phần JMeter | Cấu hình & Thông số |
| :--- | :--- |
| **Giao thức & URL** | **URL:** `https://phenikaa-uni.edu.vn/vi`[cite: 1]<br>**Method:** `GET`[cite: 1]<br>**Encoding:** `UTF-8`[cite: 1] |
| **Thread Group** | **Số lượng Threads (Users):** `100`[cite: 1]<br>**Thời gian chạy (Duration):** `60 giây`[cite: 1]<br>**Ramp-up Period:** `10 giây`[cite: 1] |
| **Listeners** | View Results Tree[cite: 1], Aggregate Report[cite: 1] |

### 2.2. Phân tích Kết quả
Dựa trên kết quả từ Aggregate Report với tổng số **1000 requests**, hệ thống ghi nhận các chỉ số sau:

*   **Tỷ lệ đáp ứng:**
    *   **Thành công:** 998/1000 yêu cầu (Đạt **99,8%**)[cite: 1].
    *   **Thất bại (Error Rate):** 2/1000 yêu cầu (Chiếm **0,2%**)[cite: 1].
*   **Thời gian phản hồi (Response Time):**
    *   **Trung bình (Average):** `40 ms`[cite: 1].
    *   **Trung vị (Median):** `38 ms`[cite: 1].
    *   **Phân vị 90 (90th Percentile):** `70 ms`[cite: 1].
*   **Thông lượng (Throughput):** Đạt mức `16 yêu cầu/giây`[cite: 1].

> **💡 Kết luận:**
> Trang web `https://phenikaa-uni.edu.vn/vi` có hiệu năng rất tốt[cite: 1]. Tỷ lệ xử lý thành công ở mức cực kỳ ấn tượng (99,8%) với tỷ lệ lỗi không đáng kể (0,2%)[cite: 1]. Tốc độ phản hồi của máy chủ rất mượt mà (trung bình, trung vị và percentil 90 đều dưới 100 ms)[cite: 1]. Mức thông lượng 16 req/s cho thấy hệ thống đáp ứng tốt các luồng truy cập đồng thời[cite: 1].

---

## 3. Kiểm thử Hiệu năng API (API Performance)

### 3.1. Cấu hình Kịch bản (Test Scenario)

| Thành phần JMeter | Cấu hình & Thông số |
| :--- | :--- |
| **Giao thức & URL** | **URL:** `https://openweathermap.org/current`[cite: 1]<br>**Method:** `GET`[cite: 1]<br>**Encoding:** `UTF-8`[cite: 1] |
| **Thread Group** | **Số lượng Threads (Users):** `100`[cite: 1]<br>**Thời gian chạy (Duration):** `60 giây`[cite: 1]<br>**Ramp-up Period:** `10 giây`[cite: 1] |
| **Listeners** | View Results Tree[cite: 1], Aggregate Report[cite: 1] |

### 3.2. Phân tích Kết quả
Sau khi thực hiện gửi **1000 requests** thông qua mô phỏng 100 người dùng, dữ liệu thu được như sau:

*   **Tỷ lệ đáp ứng:**
    *   **Thành công:** 996/1000 yêu cầu (Đạt **99,6%**)[cite: 1].
    *   **Thất bại (Error Rate):** 4/1000 yêu cầu (Chiếm **0,4%**)[cite: 1].
*   **Thời gian phản hồi (Response Time):**
    *   **Trung bình (Average):** `10 ms`[cite: 1].

> **💡 Kết luận:**
> API thời tiết `https://openweathermap.org/current` cho thấy khả năng phản hồi xuất sắc với tốc độ trung bình chỉ đạt 10 ms[cite: 1]. Dù phải chịu tải với 100 thread đồng thời, hệ thống vẫn duy trì được tính ổn định cao với tỷ lệ trả về thành công lên tới 99,6%[cite: 1]. Tỷ lệ lỗi 0,4% hoàn toàn nằm trong ngưỡng an toàn cho phép của các hệ thống Microservices/API[cite: 1].

---

## 4. Tổng kết & Đánh giá

Thông qua hai kịch bản kiểm thử, cả hệ thống **Web** và **API** đều chứng minh được năng lực xử lý tải trọng ổn định. Việc ứng dụng công cụ Apache JMeter đã giúp đội ngũ đo lường chính xác các nút thắt cổ chai (bottlenecks) nếu có, đồng thời khẳng định chất lượng máy chủ hiện tại hoàn toàn đáp ứng tốt nhu cầu truy cập thực tế.
