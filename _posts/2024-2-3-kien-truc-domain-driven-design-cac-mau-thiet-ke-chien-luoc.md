---
layout: post
title: Kiến trúc Domain-Driven Design - Các mẫu thiết kế chiến lược
description: Domain-Driven Design là một phương pháp thiết kế phần mềm tập trung vào việc phân tích và cấu trúc hệ thống theo các lĩnh vực chính của doanh nghiệp. Bài viết này đi sâu vào Bounded Context, Context Map, Model Integrity Patterns và Core Domain.
keywords: Domain-Driven Design, Bounded Context, Context Map, Model Integrity Patterns, Core Domain, kiến trúc Domain-Driven Design
excerpt: Tìm hiểu chi tiết về các khái niệm Bounded Context, Context Map, Model Integrity Patterns và Core Domain trong Domain-Driven Design.
author: Nguyễn Trường Long
---

### Giới thiệu về Domain-Driven Design

[Domain-Driven Design (DDD)](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) là một phương pháp thiết kế phần mềm tập trung vào việc phân tích và thiết kế phần mềm xung quanh các lĩnh vực chính của doanh nghiệp (domain). Được phát triển bởi Eric Evans vào năm 2003, DDD giúp giải quyết các vấn đề phức tạp trong thiết kế phần mềm và tạo ra các hệ thống dễ bảo trì và mở rộng.

Bài viết này sẽ đi sâu vào các khái niệm Bounded Context, Context Map, Model Integrity Patterns và Core Domain, là những mẫu thiết kế chiến lược quan trọng trong DDD.

### Bounded Context

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Bounded Context là một khái niệm quan trọng để giúp tổ chức và quản lý các thành phần của hệ thống phần mềm. Bounded Context được định nghĩa là một ranh giới rõ ràng và giới hạn của một phần trong hệ thống phần mềm, trong đó các thuật ngữ, hành vi, quy trình, và mô hình được định nghĩa và áp dụng một cách chặt chẽ và rõ ràng.

Bounded Context có một số đặc điểm sau:
- **Rõ ràng và giới hạn**: Bounded Context được định nghĩa rõ ràng và có giới hạn. Nó được xác định bởi các giới hạn chức năng hoặc giới hạn doanh nghiệp.
- **Độc lập**: Mỗi Bounded Context có thể độc lập với nhau và có thể tồn tại một cách riêng biệt trong hệ thống phần mềm.
- **Ngôn ngữ hóa**: Các thuật ngữ, hành vi, quy trình, và mô hình trong Bounded Context phải được định nghĩa và áp dụng một cách chặt chẽ và rõ ràng.
- **Liên kết**: Các liên kết giữa các Bounded Context cần được quản lý và xác định rõ ràng để tránh xung đột hoặc nhầm lẫn trong việc triển khai hệ thống phần mềm.

Ví dụ, trong một hệ thống bán hàng trực tuyến, có thể có hai Bounded Context chính: "Quản lý sản phẩm" và "Quản lý đơn hàng". Mỗi context sẽ có một Domain Model riêng, với các Entity, Value Object và Service riêng biệt. Trong "Quản lý sản phẩm", chúng ta có các Entity như "Product", "Category", "Supplier", và các Service như "ProductService", "CategoryService". Trong "Quản lý đơn hàng", chúng ta có các Entity như "Order", "OrderItem", "Customer", và các Service như "OrderService", "CustomerService". Điều này giúp giảm thiểu sự phức tạp và tăng tính linh hoạt trong việc phát triển và bảo trì hệ thống.

### Context Map

Context Map là một công cụ quan trọng trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) giúp hiển thị các mối quan hệ giữa các Bounded Context khác nhau trong hệ thống. Context Map cung cấp cái nhìn tổng thể về cách các Bounded Context tương tác với nhau và giúp xác định rõ ràng các giới hạn và liên kết giữa chúng.

Context Map có một số đặc điểm quan trọng:
- **Hiển thị mối quan hệ**: Context Map giúp hiển thị các mối quan hệ giữa các Bounded Context, bao gồm các loại mối quan hệ như partnership, shared kernel, customer-supplier, conformist, anti-corruption layer, và open-host service.
- **Quản lý liên kết**: Context Map giúp quản lý các liên kết giữa các Bounded Context, đảm bảo rằng các liên kết này được xác định rõ ràng và không gây ra xung đột hoặc nhầm lẫn.
- **Giao tiếp và hợp tác**: Context Map giúp cải thiện giao tiếp và hợp tác giữa các nhóm phát triển khác nhau bằng cách cung cấp cái nhìn tổng thể về cách các Bounded Context tương tác với nhau.

Ví dụ, trong một hệ thống bán hàng trực tuyến, Context Map có thể hiển thị mối quan hệ giữa "Quản lý sản phẩm" và "Quản lý đơn hàng". "Quản lý sản phẩm" có thể là một shared kernel, nơi các nhóm phát triển chia sẻ một phần mã nguồn chung để đảm bảo tính nhất quán. "Quản lý đơn hàng" có thể là customer-supplier, nơi "Quản lý đơn hàng" phụ thuộc vào dữ liệu từ "Quản lý sản phẩm". Các context này sẽ tương tác và chia sẻ dữ liệu thông qua các API hoặc các dịch vụ web.

### Model Integrity Patterns

Model Integrity Patterns trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) là các mẫu thiết kế giúp đảm bảo tính toàn vẹn và nhất quán của mô hình domain. Các mẫu này bao gồm một số chiến lược và kỹ thuật để quản lý và duy trì tính toàn vẹn của mô hình trong quá trình phát triển và bảo trì hệ thống.

Một số Model Integrity Patterns quan trọng bao gồm:
- **Aggregate**: Aggregate là một nhóm các đối tượng có liên quan với nhau, được xử lý như một đơn vị duy nhất trong các thao tác. Aggregate giúp đảm bảo tính toàn vẹn của dữ liệu bằng cách quản lý các thao tác trên các đối tượng liên quan thông qua một điểm truy cập duy nhất, gọi là Aggregate Root. Ví dụ, trong một hệ thống quản lý đơn hàng, "Order" có thể là một Aggregate Root, bao gồm các "OrderItem". Mọi thao tác thay đổi trên "OrderItem" phải thông qua "Order" để đảm bảo tính nhất quán. Các đối tượng "OrderItem" không thể thay đổi trực tiếp mà phải thông qua "Order".
- **Factory**: Factory là một mẫu thiết kế được sử dụng để tạo ra các đối tượng phức tạp. Factory giúp tách biệt logic tạo ra các đối tượng khỏi logic sử dụng các đối tượng đó, giúp hệ thống dễ dàng mở rộng và bảo trì. Ví dụ, một "OrderFactory" có thể được sử dụng để tạo ra các đối tượng "Order" với các thuộc tính và kiểm tra nhất quán cần thiết. Điều này giúp đảm bảo rằng tất cả các đơn hàng được tạo ra đều tuân thủ các quy tắc nghiệp vụ nhất định.
- **Repository**: Repository là một mẫu thiết kế được sử dụng để quản lý việc lưu trữ và truy xuất các đối tượng từ cơ sở dữ liệu. Repository cung cấp một giao diện để thực hiện các thao tác CRUD (Create, Read, Update, Delete) trên các đối tượng mà không cần biết chi tiết về cách các đối tượng này được lưu trữ. Ví dụ, "OrderRepository" có thể cung cấp các phương thức để thêm, cập nhật, xóa và truy vấn các đơn hàng từ cơ sở dữ liệu. Điều này giúp tách biệt logic truy xuất dữ liệu khỏi logic nghiệp vụ và làm cho mã nguồn dễ dàng bảo trì hơn.

### Core Domain

Core Domain trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) là phần quan trọng nhất của hệ thống, nơi chứa đựng những giá trị cốt lõi và những logic nghiệp vụ quan trọng nhất. Core Domain cần được đầu tư nhiều nhất về tài nguyên, thời gian và sự chú ý để đảm bảo rằng nó được thiết kế và triển khai một cách tốt nhất.

Core Domain có một số đặc điểm quan trọng:
- **Giá trị cốt lõi**: Core Domain chứa đựng những giá trị cốt lõi và những logic nghiệp vụ quan trọng nhất của hệ thống. Đây là phần tạo ra giá trị thực sự cho doanh nghiệp và cần được đầu tư nhiều nhất.
- **Chất lượng cao**: Core Domain cần được thiết kế và triển khai với chất lượng cao nhất để đảm bảo rằng nó đáp ứng được các yêu cầu nghiệp vụ và có thể dễ dàng mở rộng và bảo trì.
- **Tập trung nguồn lực**: Core Domain cần được tập trung nhiều nguồn lực nhất, bao gồm nhân lực, thời gian và tài nguyên, để đảm bảo rằng nó được phát triển một cách tốt nhất.

Ví dụ, trong một hệ thống bán hàng trực tuyến, Core Domain có thể là phần quản lý quy trình đặt hàng và thanh toán. Đây là nơi chứa đựng những logic nghiệp vụ quan trọng nhất và tạo ra giá trị thực sự cho doanh nghiệp, như xác thực thông tin khách hàng, xử lý thanh toán, và quản lý trạng thái đơn hàng. Phần này cần được thiết kế và triển khai một cách tốt nhất để đảm bảo rằng nó đáp ứng được các yêu cầu nghiệp vụ và có thể dễ dàng mở rộng và bảo trì.

### Tài liệu tham khảo

* [https://opus.ch/ddd-concepts-and-patterns-introduction-and-overview/](https://opus.ch/ddd-concepts-and-patterns-introduction-and-overview/)
* [https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design](https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design)
* [https://www.infoq.com/articles/ddd-in-practice](https://www.infoq.com/articles/ddd-in-practice)
* [https://martinfowler.com/tags/domain%20driven%20design.html](https://martinfowler.com/tags/domain%20driven%20design.html)
