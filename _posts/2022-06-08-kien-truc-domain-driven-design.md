---
layout: post
title: Kiến trúc Domain-Driven Design
description: Domain-Driven Design (DDD) là một phương pháp thiết kế phần mềm tập trung vào việc mô hình hóa nghiệp vụ cốt lõi của doanh nghiệp. Nó cung cấp các khối lắp ghép chiến thuật và chiến lược để giải quyết các hệ thống phức tạp.
keywords: Domain-Driven Design, design pattern, DDD, mô hình Domain-Driven Design, kiến trúc Domain-Driven Design, Domain Model, Tactical Patterns, Strategic Patterns
excerpt: Domain-Driven Design là một phương pháp thiết kế phần mềm tập trung vào domain của doanh nghiệp. Nó cung cấp các mẫu thiết kế chiến thuật và chiến lược để giúp xây dựng hệ thống phức tạp, dễ bảo trì và có khả năng mở rộng.
author: Nguyễn Trường Long
---

### Giới thiệu về Domain-Driven Design

[Domain-Driven Design (DDD)](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) do Eric Evans hệ thống hóa trong cuốn *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Cốt lõi của DDD là đưa **domain nghiệp vụ** lên vị trí trung tâm, để mô hình phần mềm phản ánh đúng khái niệm, quy tắc và ngôn ngữ của doanh nghiệp. Khi các khái niệm nghiệp vụ được đặt đúng chỗ, hệ thống có khả năng biến đổi theo nhu cầu thực tế mà không đổ vỡ kiến trúc.

DDD nhấn mạnh vào **Ubiquitous Language**. Đó là ngôn ngữ chung giữa chuyên gia nghiệp vụ và kỹ sư phần mềm, dùng xuyên suốt trong tài liệu, hội thoại, thiết kế và mã nguồn. Khi cả đội cùng nói một thứ tiếng, độ hiểu đúng tăng lên, sai lệch giảm xuống, và mô hình trở nên sáng rõ.

Mục tiêu của DDD không phải là “áp dụng càng nhiều pattern càng tốt” mà là **đưa ra quyết định mô hình hóa đúng lúc, đúng chỗ**, để ràng buộc phức tạp được quản trị một cách chủ động.


### Lý do cần Domain-Driven Design

Hệ thống doanh nghiệp phát triển theo thời gian thường gặp những mùi kiến trúc quen thuộc. Logic nghiệp vụ rải rác trong controller hay trigger. Các tên gọi mơ hồ khiến một thay đổi nhỏ lan ra nhiều module. Mã nguồn bám chặt cách lưu dữ liệu nên mỗi lần đổi công nghệ là cả hệ thống rung lắc.

DDD giải quyết bằng cách đặt câu hỏi đúng. Bản chất nghiệp vụ là gì. Những khái niệm nào doanh nghiệp dùng hằng ngày. Giới hạn nào tách bạch một ngữ cảnh với ngữ cảnh khác. Từ đó mô hình được sinh ra **vì nghiệp vụ**, không phải vì bảng dữ liệu hay framework.

Ba hiệu quả nhìn thấy sớm nhất là  
1) giao tiếp thông suốt nhờ Ubiquitous Language  
2) khả năng thay đổi cao nhờ mô hình hóa đúng ranh giới  
3) giảm nợ kỹ thuật nhờ tách biệt domain với hạ tầng


### Bức tranh tổng thể kiến trúc DDD

Một hệ thống theo DDD thường tổ chức theo các lớp vai trò rõ ràng.

**Presentation** tiếp nhận yêu cầu và trình bày kết quả.  
**Application** điều phối use case, giao tiếp với domain, không chứa quy tắc nghiệp vụ cốt lõi.  
**Domain** là trái tim. Nơi đặt khái niệm, quy tắc, trạng thái và bất biến của nghiệp vụ.  
**Infrastructure** cung cấp kỹ thuật như lưu trữ, message bus, tích hợp ngoài, hiện thực hóa Repository và Adapter.

Luồng điển hình là Presentation gọi Application. Application gọi Domain để thực thi nghiệp vụ. Domain yêu cầu Infrastructure thông qua hợp đồng đã định. Hướng phụ thuộc chảy về Domain để bảo toàn tính độc lập của mô hình.


### Từ yêu cầu đến mô hình domain

DDD không bắt đầu từ database. Nó bắt đầu từ hội thoại.

**Khám phá ngôn ngữ**. Thu thập thuật ngữ và tình huống điển hình. Làm rõ nghĩa từng từ qua ví dụ cụ thể.  
**Event Storming** hoặc workshop tương đương. Vẽ những sự kiện nghiệp vụ quan trọng. Từ sự kiện lần ra lệnh và quy tắc.  
**Ranh giới ngữ cảnh**. Nhận diện những vùng ngôn ngữ khác nhau để xác định Bounded Context.  
**Mô hình hóa chiến thuật**. Bên trong mỗi context, xác định Entity, Value Object, Aggregate, Domain Service.  
**Tích hợp giữa context**. Quy ước cách trao đổi và mức độ phụ thuộc, vẽ Context Map để cả đội cùng thấy bức tranh chung.

Quá trình này lặp lại. Mỗi vòng lặp làm ngôn ngữ rõ hơn và mô hình tinh gọn hơn.


### Các mẫu thiết kế trong Domain-Driven Design

Trong DDD có hai nhóm mẫu chính. **Tactical Patterns** dùng để cấu trúc domain model ở cấp mã nguồn. **Strategic Patterns** dùng để tổ chức toàn hệ thống và mối quan hệ giữa các ngữ cảnh. Bài viết này giới thiệu bức tranh chung để bạn định hướng. Diễn giải chi tiết từng nhóm được trình bày riêng trong  
**Khái niệm Domain Model** và các mẫu chiến thuật tại bài *[Khái niệm Domain Model](https://nguyentruonglong.net/khai-niem-domain-model.html)*  
**Các mẫu chiến lược** tại bài *[Kiến trúc DDD — Các mẫu thiết kế chiến lược](https://nguyentruonglong.net/kien-truc-domain-driven-design-cac-mau-thiet-ke-chien-luoc.html)*

#### Tactical Patterns ở mức khái quát

**Entity** là đối tượng có định danh ổn định theo thời gian. Trạng thái thay đổi nhưng danh tính vẫn là một.  
**Value Object** đại diện cho một giá trị có ý nghĩa, bất biến, xác định bởi thuộc tính. Dùng để diễn tả tiền tệ, khoảng thời gian, địa chỉ.  
**Aggregate** gom các đối tượng liên quan thành một đơn vị nhất quán, có **Aggregate Root** điều phối bất biến và giao tiếp với bên ngoài.  
**Repository** cung cấp cách truy xuất và lưu trữ Aggregate theo ngôn ngữ domain, che giấu chi tiết hạ tầng.  
**Factory** khởi tạo các đối tượng phức tạp, đảm bảo bất biến ngay từ lúc sinh.  
**Domain Service** chứa nghiệp vụ không gắn chặt vào một Entity hay Value Object nào.  
**Module** tổ chức các khái niệm liên quan thành một không gian đặt tên gọn ghẽ.

Những khối lắp ghép này giúp mã nguồn nói đúng ngôn ngữ nghiệp vụ và giữ được tính nhất quán.

#### Strategic Patterns ở mức khái quát

**Bounded Context** đặt ranh giới cho một mô hình và ngôn ngữ. Mỗi context có mô hình riêng, triển khai độc lập, giao tiếp qua hợp đồng.  
**Context Map** mô tả quan hệ giữa các context như Shared Kernel, Customer Supplier, Conformist, Anti Corruption Layer, Open Host Service.  
**Model Integrity Patterns** là tập kỹ thuật giữ cho mô hình không bị xói mòn khi hệ thống mở rộng, tiêu biểu là Aggregate, Domain Event, Service Layer.  
**Core Domain** là phần cốt lõi tạo lợi thế cạnh tranh. Đó là nơi dồn nguồn lực tốt nhất và được bảo vệ khỏi thay đổi không cần thiết.


### Ví dụ dẫn đường ngắn

Giả sử bạn xây dựng hệ thống đặt hàng trực tuyến.

Trong **context Quản lý đơn hàng**, *Đơn hàng* là một **Aggregate** với Root là `Order`. Mỗi dòng hàng là `OrderItem`. Giá tiền là **Value Object** `Money`. Quy tắc như “không thể xác nhận nếu chưa có phương thức thanh toán hợp lệ” là bất biến của Aggregate.

Trong **context Danh mục sản phẩm**, khái niệm *Sản phẩm* có ngôn ngữ riêng. Giá và thuộc tính được quản trị bởi nhóm khác. Hai context giao tiếp qua API đã thỏa thuận. Nếu hệ thống ngoài thay đổi, lớp **Anti Corruption Layer** chuyển đổi thông điệp để không làm rò rỉ khái niệm ngoại lai vào domain bên trong.

Khi người dùng đặt hàng, **Application Service** gọi `Order.place(...)`. Aggregate kiểm tra bất biến, phát `OrderPlaced` như một **Domain Event**. Context **Thanh toán** lắng nghe sự kiện để khởi động quy trình thu tiền. Mỗi phần chạy theo ngôn ngữ của mình nhưng phối hợp nhịp nhàng nhờ hợp đồng rõ ràng.


### Khi nào nên áp dụng DDD

DDD tỏa sáng ở những domain giàu quy tắc, thay đổi thường xuyên, đòi hỏi hiểu biết sâu về nghiệp vụ. Nếu bài toán chỉ là CRUD đơn giản ít thay đổi, áp dụng đầy đủ DDD có thể tạo cảm giác nặng nề. Khi bạn thấy giao tiếp giữa kỹ sư và chuyên gia nghiệp vụ khó khăn, yêu cầu hay đổi hướng, logic rắc rối, đó là dấu hiệu tốt để bắt đầu bằng Ubiquitous Language và Bounded Context.


### Rủi ro và sai lầm thường gặp

Mô hình hóa theo cấu trúc dữ liệu thay vì khái niệm nghiệp vụ khiến domain bị dẫn dắt bởi bảng. Đặt quá nhiều logic vào Application Service làm domain rỗng ruột. Nhập nhằng ranh giới giữa các context khiến khái niệm bị mượn dùng tùy tiện. Quá khích tách nhỏ thành nhiều service khi ngôn ngữ chưa chín muồi dẫn đến phức tạp tích hợp. Cách khắc phục là quay về hội thoại, làm rõ ngôn ngữ, củng cố bất biến, để mô hình dẫn đường cho kiến trúc kỹ thuật.


### Ưu điểm khi áp dụng DDD

Hệ thống phản ánh đúng nghiệp vụ nên dễ giải thích và kiểm chứng. Mô hình tách rời hạ tầng nên đổi công nghệ lưu trữ hay tích hợp ngoài không làm đảo lộn domain. Ngôn ngữ chung giúp tăng tốc phát triển vì giảm hiểu nhầm. Khi có ranh giới rõ ràng, nhóm có thể chia nhỏ công việc và triển khai độc lập mà vẫn giữ toàn vẹn tổng thể.


### Kết luận

Domain-Driven Design là một cách tiếp cận toàn diện để đối diện với phức tạp. Nó bắt đầu từ ngôn ngữ và ranh giới, tiếp tục bằng mô hình hóa chiến thuật, và được giữ nhịp bởi bản đồ quan hệ giữa các context. Không phải hệ thống nào cũng cần trọn bộ DDD, nhưng với bài toán giàu quy tắc và thay đổi liên tục, DDD giúp kiến trúc vững, mã nguồn sáng, và đội ngũ nói cùng một tiếng nói.

Để đi sâu vào từng mảnh ghép, xem thêm  
bài *Khái niệm Domain Model* và các mẫu chiến thuật  
bài *Kiến trúc DDD — Các mẫu thiết kế chiến lược* đã liên kết ở trên.


### Tài liệu tham khảo

* Eric Evans — *Domain-Driven Design: Tackling Complexity in the Heart of Software*  
* Martin Fowler — [Domain-Driven Design](https://martinfowler.com/tags/domain%20driven%20design.html)  
* [InfoQ - DDD in Practice](https://www.infoq.com/articles/ddd-in-practice)
