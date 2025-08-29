---
layout: post
title: Khái niệm Domain Model
description: Domain Model là mô hình khái niệm kết hợp dữ liệu và hành vi để biểu diễn nghiệp vụ cốt lõi của hệ thống. Nó giúp giảm độ phức tạp và tăng tính chính xác trong thiết kế phần mềm.
excerpt: Domain Model là một bản phác thảo các thực thể cơ bản của hệ thống và mối quan hệ giữa chúng. Nó tạo ra mạng lưới các đối tượng phản ánh đúng bản chất nghiệp vụ, giúp cho việc phân tích, thiết kế và bảo trì hệ thống dễ dàng hơn.
thumbnail:
keywords: domain model, khái niệm domain model, mô hình miền, entity, value object, aggregate, repository, service
author: Nguyễn Trường Long
---

### Khái niệm Domain Model

[Domain Model](https://nguyentruonglong.net/khai-niem-domain-model.html) là một mô hình khái niệm mô tả **các thực thể, hành vi và mối quan hệ** trong một lĩnh vực (domain) nghiệp vụ cụ thể.  
Nó đóng vai trò trung tâm trong kiến trúc **Domain-Driven Design (DDD)**, giúp phản ánh đúng cách hệ thống hoạt động theo ngữ nghĩa nghiệp vụ, thay vì chỉ dựa vào dữ liệu hoặc công nghệ.

Đặc điểm quan trọng của Domain Model:
- **Kết hợp dữ liệu và hành vi**: mô hình không chỉ mô tả thông tin (attributes) mà còn bao gồm các quy tắc, hành vi nghiệp vụ (methods, logic).  
- **Độc lập với công nghệ**: domain model tập trung vào nghiệp vụ, không phụ thuộc vào cơ sở dữ liệu hay framework.  
- **Hỗ trợ giao tiếp**: trở thành “ngôn ngữ chung” giữa nhà phát triển và chuyên gia nghiệp vụ.  

Ví dụ: trong hệ thống bán hàng trực tuyến, Domain Model có thể bao gồm:
- `Order` (Đơn hàng)  
- `Customer` (Khách hàng)  
- `Product` (Sản phẩm)  
- `Payment` (Thanh toán)  
Mỗi thành phần đều có thuộc tính và hành vi riêng, phản ánh đúng nghiệp vụ bán hàng.

---

### Thành phần chính của Domain Model

#### 1. Entity

- **Định nghĩa**: Là đối tượng có định danh (ID) duy nhất, tồn tại độc lập trong hệ thống. Dù thuộc tính có thay đổi, ID vẫn xác định nó là cùng một Entity.  
- **Đặc điểm**:  
  - Có vòng đời riêng (lifecycle).  
  - Có thể thay đổi trạng thái nhưng vẫn giữ nguyên định danh.  
- **Ví dụ**: `Customer` có `customerId`; `Order` có `orderId`.  

Entity thường được sử dụng để biểu diễn **các đối tượng kinh doanh quan trọng** như khách hàng, đơn hàng, tài khoản.

---

#### 2. Value Object

- **Định nghĩa**: Là đối tượng được xác định **bởi giá trị**, không có định danh riêng.  
- **Đặc điểm**:  
  - Bất biến (immutable).  
  - Hai Value Object bằng nhau nếu tất cả thuộc tính của chúng bằng nhau.  
- **Ví dụ**: `Address` (địa chỉ: số nhà, đường, thành phố), `Money` (số tiền, loại tiền tệ).  

Value Object giúp làm cho mô hình gọn nhẹ, rõ ràng và dễ kiểm soát tính toàn vẹn dữ liệu.

---

#### 3. Aggregate

- **Định nghĩa**: Là một **nhóm các Entity và Value Object có liên quan**, được quản lý như một đơn vị duy nhất.  
- **Aggregate Root**: Một Entity duy nhất làm điểm truy cập chính để đảm bảo tính nhất quán của Aggregate.  
- **Ví dụ**: `Order` (Aggregate Root) quản lý danh sách `OrderItem`. Việc thêm, sửa, xóa `OrderItem` phải thông qua `Order`.  

Aggregate giúp tránh việc truy cập trực tiếp và đảm bảo quy tắc nghiệp vụ luôn được áp dụng đúng.

---

#### 4. Repository

- **Định nghĩa**: Lớp trừu tượng để **lưu trữ và truy xuất** Entity hoặc Aggregate.  
- **Chức năng**:  
  - Ẩn chi tiết kỹ thuật của cơ sở dữ liệu.  
  - Cung cấp các phương thức truy vấn theo ngôn ngữ nghiệp vụ.  
- **Ví dụ**: `OrderRepository` có thể có các phương thức `findById(orderId)` hoặc `findOrdersByCustomer(customerId)`.  

Repository giúp domain model **không phụ thuộc trực tiếp vào tầng dữ liệu**.

---

#### 5. Service

- **Định nghĩa**: Thành phần chứa logic nghiệp vụ **không thuộc về một Entity hay Value Object cụ thể**.  
- **Đặc điểm**:  
  - Thực hiện các hành động có ý nghĩa nghiệp vụ.  
  - Thường kết hợp nhiều Entity/Value Object/Repository.  
- **Ví dụ**: `OrderService` xử lý việc tạo đơn hàng mới, kiểm tra tồn kho, và gọi `PaymentService` để xử lý thanh toán.  

Service giúp domain model giữ được sự gọn gàng, tránh việc nhồi nhét logic vào Entity.

---

### Ý nghĩa của Domain Model

- **Giảm độ phức tạp**: tập trung vào khái niệm và hành vi quan trọng nhất của nghiệp vụ.  
- **Cải thiện giao tiếp**: là cầu nối giữa kỹ thuật và chuyên gia nghiệp vụ.  
- **Tái sử dụng và mở rộng**: mô hình có thể mở rộng khi yêu cầu thay đổi.  
- **Dễ bảo trì**: logic nghiệp vụ tập trung và rõ ràng, không bị phân tán.  

---

### Kết luận

Domain Model là **linh hồn của Domain-Driven Design**.  
Nếu coi DDD như một kiến trúc tổng thể, thì Domain Model chính là **trái tim** giúp phản ánh nghiệp vụ, giảm sự phức tạp, và tạo nền tảng để xây dựng các hệ thống phần mềm bền vững, dễ bảo trì.

---

### Tài liệu tham khảo

* Eric Evans — *Domain-Driven Design: Tackling Complexity in the Heart of Software*  
* [Martin Fowler: Domain Model](https://martinfowler.com/eaaCatalog/domainModel.html)  
* [InfoQ - DDD in Practice](https://www.infoq.com/articles/ddd-in-practice)  
