---
layout: post
title: Kiến trúc Domain-Driven Design
description: Domain-Driven Design là một design pattern ở cấp độ hệ thống được áp dụng cho các nghiệp vụ phức tạp. Nó cung cấp cấp các khối lắp ghép (building blocks) chiến lược để phân tích và cấu trúc cho các vấn đề và giải pháp.
keywords: Domain-Driven Design, design pattern, DDD, mô hình Domain-Driven Design, kiến trúc Domain-Driven Design, mô hình DDD, kiến trúc DDD
excerpt: Domain-Driven Design là một design pattern ở cấp độ hệ thống được áp dụng cho các nghiệp vụ phức tạp. Nó cung cấp cấp các khối lắp ghép (building blocks) chiến lược để phân tích và cấu trúc cho các vấn đề và giải pháp.
author: Nguyễn Trường Long
---

### Giới thiệu về Domain-Driven Design

Hôm vừa rồi tình cờ đọc được một số bài viết về [kiến trúc Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html). Thấy có hứng thú nên quyết định tìm hiểu sâu thêm về kiến trúc này mặc dù nó chưa thật sự phổ biến ở Việt Nam. Tài liệu được tham khảo chủ yếu đến từ blog của tác giả Martin Fowler và sách của tác giả Eric Evans.

Trong bài viết này chúng ta sẽ cùng lướt qua các khái niệm chính trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) như Domain Model, Entity, Value Object, Service, Bounded Context, Anti-Corruption Layer.

### Domain Model

Domain Model là một mô hình bao gồm các đối tượng (Objects), phương thức (Methods) và quan hệ giữa chúng được định nghĩa để mô tả và giải quyết vấn đề trong lĩnh vực kinh doanh (business domain). Nó được tạo ra từ việc sử dụng các ngôn ngữ bổ sung như Ubiquitous Language để phát triển một mô hình chung, đại diện cho tất cả các khía cạnh của lĩnh vực kinh doanh.

### Entity

Entity là một đối tượng trong Domain Model, được định nghĩa bởi các thuộc tính riêng biệt và có một định danh (identity) duy nhất. Entity được định nghĩa để đại diện cho các đối tượng vật lý hoặc trừu tượng trong lĩnh vực kinh doanh.

### Value Object

Value Object là một đối tượng trong Domain Model, không có định danh duy nhất và được xác định bởi các thuộc tính của nó. Value Object thường được sử dụng để biểu diễn các thuộc tính hoặc trạng thái của các Entity.

### Service

Service là một phương thức hoặc hành động trong Domain Model, không thuộc về một Entity hoặc Value Object cụ thể nào. Service thường được sử dụng để thực hiện các hành động liên quan đến nhiều Entity hoặc các hành động phức tạp mà không thể thực hiện bằng cách chỉ sử dụng một Entity.

### Bounded Context

Bounded Context là một giới hạn về mặt ngữ nghĩa của Domain Model, trong đó các thuật ngữ và quan hệ giữa các đối tượng chỉ áp dụng trong phạm vi của Bounded Context. Nó cho phép tách và tổ chức các phần của một hệ thống phức tạp thành các thành phần nhỏ hơn và dễ quản lý hơn.

### Anti-Corruption Layer

Anti-Corruption Layer là một lớp trừu tượng trong Domain Model, giúp giảm thiểu tác động của các thành phần hệ thống bên ngoài lên Domain Model. Nó giúp đảm bảo tính độc lập và kiểm soát việc chuyển đổi dữ liệu giữa Domain Model và các hệ thống bên ngoài.

### Tài liệu tham khảo

* <a href="https://www.infoq.com/articles/ddd-in-practice" target="_blank">https://www.infoq.com/articles/ddd-in-practice</a>
* <a href="https://martinfowler.com/tags/domain%20driven%20design.html" target="_blank">https://martinfowler.com/tags/domain%20driven%20design.html</a>
