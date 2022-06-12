---
layout: post
title: Kiến trúc Domain-Driven Design
description: Domain-Driven Design là một design pattern ở cấp độ hệ thống được áp dụng cho các nghiệp vụ phức tạp. Nó cung cấp cấp các khối lắp ghép (building blocks) chiến lược để phân tích và cấu trúc cho các vấn đề và giải pháp.
keywords: Domain-Driven Design, design pattern, DDD, mô hình Domain-Driven Design, kiến trúc Domain-Driven Design, mô hình DDD, kiến trúc DDD
excerpt: Domain-Driven Design là một design pattern ở cấp độ hệ thống được áp dụng cho các nghiệp vụ phức tạp. Nó cung cấp cấp các khối lắp ghép (building blocks) chiến lược để phân tích và cấu trúc cho các vấn đề và giải pháp.
author: Nguyễn Trường Long
---

### Giới thiệu về Domain-Driven Design

Hôm vừa rồi tình cờ đọc được một số bài viết về [kiến trúc Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html). Thấy có hứng thú nên quyết định tìm hiểu sâu thêm về kiến trúc này mặc dù nó chưa thật sự phổ biến ở Việt Nam. Tài liệu được tham khảo chủ yếu đến từ blog của tác giả Martin Fowler và sách của tác giả Eric Evans. Những tài liệu này sẽ được đính kèm ở mục tài liệu tham khảo bên dưới cuối bài viết này để mọi người cũng có thể đọc và tìm hiểu thêm. Trong bài viết này mình sẽ note lại những kiến thức trong quá trình tìm hiểu được dù thật sự chưa bao giờ có cơ hội làm việc trên kiến trúc này. Nếu có điều gì sai sót mong sẽ nhận được nhiều góp ý.

Trong bài viết này chúng ta sẽ cùng lướt qua các khái niệm chính trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) như Domain Model, Entity, Value Object, Service, Bounded Context, Anti-Corruption Layer,...

### Tài liệu tham khảo

* <a href="https://www.infoq.com/articles/ddd-in-practice" target="_blank">https://www.infoq.com/articles/ddd-in-practice</a>
* <a href="https://martinfowler.com/tags/domain%20driven%20design.html" target="_blank">https://martinfowler.com/tags/domain%20driven%20design.html</a>
