---
layout: post
title: Kiến trúc Domain-Driven Design - Các mẫu thiết kế chiến lược
description: Domain-Driven Design là một phương pháp thiết kế phần mềm tập trung vào việc phân tích và cấu trúc hệ thống theo các lĩnh vực chính của doanh nghiệp. Bài viết này đi sâu vào Bounded Context, Context Map, Model Integrity Patterns và Core Domain.
keywords: Domain-Driven Design, Bounded Context, Context Map, Model Integrity Patterns, Core Domain, kiến trúc Domain-Driven Design
excerpt: Tìm hiểu chi tiết về các khái niệm Bounded Context, Context Map, Model Integrity Patterns và Core Domain trong Domain-Driven Design.
author: Nguyễn Trường Long
---

### Giới thiệu

Trong kiến trúc [Domain-Driven Design (DDD)](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), các **mẫu thiết kế chiến lược (Strategic Patterns)** giữ vai trò định hướng ở cấp độ toàn hệ thống.  
Chúng giúp xác định ranh giới, phạm vi, và cách các mô-đun lớn tương tác với nhau, từ đó tránh sự phức tạp không kiểm soát trong những hệ thống doanh nghiệp lớn.  

Bốn mẫu chiến lược quan trọng nhất là:  
- **Bounded Context**  
- **Context Map**  
- **Model Integrity Patterns**  
- **Core Domain**  

---

### Bounded Context

**Định nghĩa**: Bounded Context là một ranh giới rõ ràng trong hệ thống, nơi mà các khái niệm, mô hình, và ngôn ngữ nghiệp vụ được định nghĩa và áp dụng thống nhất.  

Đặc điểm:  
- **Phạm vi rõ ràng**: mỗi context gói trọn một phần nghiệp vụ cụ thể.  
- **Độc lập**: một context có thể phát triển và triển khai riêng.  
- **Ubiquitous Language riêng**: thuật ngữ và quy tắc nghiệp vụ trong một context không nhất thiết giống ở context khác.  
- **Giao tiếp có kiểm soát**: các context chỉ tương tác qua API, service hoặc cơ chế tích hợp đã xác định.  

Ví dụ: trong một hệ thống thương mại điện tử có thể có các bounded context:  
- `Quản lý sản phẩm` (Product Catalog)  
- `Quản lý đơn hàng` (Order Management)  
- `Thanh toán` (Payment)  

Mỗi context hoạt động độc lập, dùng mô hình dữ liệu riêng, nhưng cần tích hợp với nhau khi thực hiện nghiệp vụ hoàn chỉnh.

---

### Context Map

Khi có nhiều Bounded Context, cần một **bản đồ mối quan hệ (Context Map)** để quản lý cách chúng tương tác.  

Các loại quan hệ thường gặp trong Context Map:  
- **Partnership**: hai nhóm phát triển phối hợp chặt chẽ, chia sẻ trách nhiệm.  
- **Shared Kernel**: chia sẻ một phần mô hình chung, thường là các Entity cốt lõi.  
- **Customer–Supplier**: một context phụ thuộc dữ liệu từ context khác.  
- **Conformist**: một context buộc phải tuân theo mô hình của context khác.  
- **Anti-Corruption Layer (ACL)**: lớp bảo vệ để dịch và che chắn mô hình khỏi ảnh hưởng bên ngoài.  
- **Open Host Service**: cung cấp giao diện chung (API/public service) để nhiều context cùng sử dụng.  

Ví dụ:  
- Trong thương mại điện tử, `Order Management` có thể là **Customer**, còn `Product Catalog` là **Supplier** (Order phụ thuộc dữ liệu sản phẩm).  
- `Payment` có thể tích hợp với hệ thống ngân hàng ngoài qua **Anti-Corruption Layer**, để tránh thay đổi trong ngân hàng ảnh hưởng trực tiếp đến Core Domain.  

Context Map giúp các nhóm phát triển hình dung toàn cảnh và lựa chọn chiến lược tích hợp phù hợp.

---

### Model Integrity Patterns

Mục tiêu của **Model Integrity Patterns** là đảm bảo tính toàn vẹn và nhất quán của Domain Model khi hệ thống mở rộng.  

Một số mẫu quan trọng:  
- **Aggregate**: gom các đối tượng liên quan thành một đơn vị nhất quán, với một Aggregate Root điều phối.  
- **Factory**: quản lý logic khởi tạo đối tượng phức tạp, đảm bảo tính hợp lệ ngay từ khi tạo.  
- **Repository**: cung cấp cách thức nhất quán để truy xuất và lưu trữ Aggregate/Entity.  
- **Service Layer**: tách biệt logic nghiệp vụ phức tạp khỏi tầng dữ liệu và trình bày.  
- **Domain Event**: ghi nhận và lan truyền các sự kiện quan trọng trong domain, cho phép các phần khác phản ứng độc lập.  

Ví dụ: Trong `Order Management`, một **Domain Event** như `OrderPlaced` có thể kích hoạt xử lý thanh toán ở context `Payment` mà không cần hai context phụ thuộc chặt chẽ vào nhau.

---

### Core Domain

**Định nghĩa**: Core Domain là phần **giá trị cốt lõi** của hệ thống – nơi chứa những logic nghiệp vụ quan trọng nhất tạo ra lợi thế cạnh tranh cho doanh nghiệp.  

Đặc điểm:  
- **Tập trung đầu tư**: cần nguồn lực tốt nhất (developer giỏi, thời gian, kiểm thử kỹ).  
- **Chất lượng cao**: mã nguồn phải rõ ràng, ít phụ thuộc, dễ mở rộng.  
- **Được bảo vệ**: cách ly khỏi thay đổi không liên quan bằng các kỹ thuật như Anti-Corruption Layer.  

Ví dụ:  
- Trong hệ thống ngân hàng, Core Domain là **xử lý giao dịch tài chính** (đảm bảo tính toàn vẹn số dư, tính toán lãi suất).  
- Trong thương mại điện tử, Core Domain là **quy trình đặt hàng và thanh toán**.  

Những phần khác như báo cáo, giao diện, tích hợp bên ngoài có thể quan trọng nhưng không phải Core Domain – vì không tạo giá trị cạnh tranh dài hạn.

---

### Kết luận

Các mẫu thiết kế chiến lược trong DDD giúp:  
- Phân tách hệ thống thành các phần **độc lập nhưng có tổ chức**.  
- Quản lý mối quan hệ và phụ thuộc giữa các Bounded Context.  
- Giữ vững **tính toàn vẹn của mô hình domain** khi mở rộng.  
- Tập trung nguồn lực vào **Core Domain** – nơi tạo ra giá trị thực sự.  

Nhờ đó, hệ thống có khả năng mở rộng, dễ bảo trì và bền vững trong dài hạn.

---

### Tài liệu tham khảo

* Eric Evans — *Domain-Driven Design: Tackling Complexity in the Heart of Software*  
* [InfoQ - Strategic Design Patterns](https://www.infoq.com/articles/ddd-in-practice)  
* [Microsoft Learn - Introduction to DDD](https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design)  
* [Martin Fowler - DDD](https://martinfowler.com/tags/domain%20driven%20design.html)  
