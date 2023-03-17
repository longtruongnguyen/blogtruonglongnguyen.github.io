---
layout: post
title: Kiến trúc Domain-Driven Design
description: Domain-Driven Design là một design pattern ở cấp độ hệ thống được áp dụng cho các nghiệp vụ phức tạp. Nó cung cấp cấp các khối lắp ghép (building blocks) chiến lược để phân tích và cấu trúc cho các vấn đề và giải pháp.
keywords: Domain-Driven Design, design pattern, DDD, mô hình Domain-Driven Design, kiến trúc Domain-Driven Design, mô hình DDD, kiến trúc DDD, Anti-Corruption Layer, Domain Model
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

Trong [Domain-Driven Design (DDD)](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Service là một khái niệm quan trọng của việc mô hình hóa và thiết kế các hệ thống. Service đại diện cho các chức năng hoặc nhiệm vụ cụ thể mà hệ thống phải thực hiện, thường liên quan đến các thao tác xử lý dữ liệu hoặc tương tác giữa các thành phần khác nhau trong hệ thống. Nó là một phương thức hoặc hành động không thuộc về một Entity hoặc Value Object cụ thể nào. Service thường được sử dụng để thực hiện các hành động liên quan đến nhiều Entity hoặc các hành động phức tạp mà không thể thực hiện bằng cách chỉ sử dụng một Entity.

Một Service có thể bao gồm các thao tác CRUD (Create, Read, Update, Delete) hoặc các thao tác phức tạp hơn như xử lý giao dịch, phân tích dữ liệu, tính toán phức tạp, tương tác với các API bên ngoài và các hệ thống khác, và các nhiệm vụ khác liên quan đến logic kinh doanh của hệ thống.

Service thường được triển khai dưới dạng các phương thức trong các lớp của ứng dụng hoặc được triển khai bằng các service bên ngoài (ví dụ: RESTful API, giao thức RPC, v.v.). Các Service thường được phân loại theo Bounded Context để đảm bảo tính chính xác và sự độc lập giữa các nhiệm vụ khác nhau trong hệ thống.

Ví dụ về Service trong hệ thống bán lẻ có thể là "CheckoutService", "OrderService" hoặc "PaymentService", mỗi Service đóng vai trò quản lý một phần của quy trình mua hàng. Các Service này có thể tương tác với các Entity như "Product", "Customer", "Order" hoặc các Value Object như "ShippingAddress", "PaymentMethod".

### Bounded Context

Trong [Domain-Driven Design (DDD)](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Bounded Context là một khái niệm quan trọng để giúp tổ chức và quản lý các thành phần của hệ thống phần mềm. Bounded Context được định nghĩa là một ranh giới rõ ràng và giới hạn của một phần trong hệ thống phần mềm, trong đó các thuật ngữ, hành vi, quy trình, và mô hình được định nghĩa và áp dụng một cách chặt chẽ và rõ ràng.

Một Bounded Context có thể bao gồm nhiều thực thể (Entities) và giá trị (Value Objects), cũng như các dịch vụ (Services) liên quan đến chức năng của Bounded Context đó. Tuy nhiên, một thực thể hoặc giá trị có thể có nhiều Bounded Context khác nhau và được định nghĩa khác nhau trong từng Bounded Context. Vì vậy, một cách tiếp cận đúng đắn trong việc thiết kế hệ thống phần mềm là phải cân nhắc và xác định rõ ràng Bounded Context và quản lý các liên kết giữa các Bounded Context. Các thuật ngữ và quan hệ giữa các đối tượng chỉ áp dụng trong phạm vi của Bounded Context. Nó cho phép tách và tổ chức các phần của một hệ thống phức tạp thành các thành phần nhỏ hơn và dễ quản lý hơn.

Bounded Context có một số đặc điểm sau:
- <b>Rõ ràng và giới hạn</b>: Bounded Context được định nghĩa rõ ràng và có giới hạn. Nó được xác định bởi các giới hạn chức năng hoặc giới hạn doanh nghiệp.
- <b>Độc lập</b>: Mỗi Bounded Context có thể độc lập với nhau và có thể tồn tại một cách riêng biệt trong hệ thống phần mềm.
- <b>Ngôn ngữ hóa</b>: Các thuật ngữ, hành vi, quy trình, và mô hình trong Bounded Context phải được định nghĩa và áp dụng một cách chặt chẽ và rõ ràng.
- <b>Liên kết</b>: Các liên kết giữa các Bounded Context cần được quản lý và xác định rõ ràng để tránh xung đột hoặc nhầm lẫn trong việc triển khai hệ thống phần mềm.

Ví dụ chúng ta đang phát triển một hệ thống bán hàng trực tuyến, trong đó có hai context chính là "Quản lý sản phẩm" và "Quản lý đơn hàng". Mỗi context sẽ có một Domain Model riêng, với các Entity, Value Object và Service riêng biệt. Trong context "Quản lý sản phẩm", các khái niệm quan trọng có thể bao gồm: Product, Category, Review, Image, Supplier, Stock, và các service như ProductService, CategoryService, ImageService. Trong context "Quản lý đơn hàng", các khái niệm quan trọng có thể bao gồm: Order, Customer, Payment, Shipping, OrderItem, và các service như OrderService, PaymentService, ShippingService.

Việc phân chia thành các Bounded Context khác nhau sẽ giúp chúng ta tập trung vào các yêu cầu và quy trình kinh doanh cụ thể trong mỗi context, đồng thời giảm thiểu sự phức tạp và sự rắc rối khi phát triển hệ thống. Ngoài ra, Bounded Context cũng giúp định rõ các giới hạn và các quy tắc liên quan đến quản lý dữ liệu và logic kinh doanh, giúp tăng tính linh hoạt và tái sử dụng của hệ thống.

### Anti-Corruption Layer

Trong [Domain-Driven Design (DDD)](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Anti-Corruption Layer (ACL) là một lớp được sử dụng để giữ cho các thành phần của hệ thống không bị ảnh hưởng bởi các thành phần khác nằm bên ngoài, đặc biệt là các thành phần được thiết kế bởi các nhóm khác hoặc bên thứ ba. Khi một hệ thống phần mềm được phát triển trên nhiều nền tảng và có các thành phần khác nhau, nhưng các thành phần này không tuân thủ cùng một ngôn ngữ chung, điều này dẫn đến sự khó khăn trong việc tích hợp các thành phần này với nhau. Để giải quyết vấn đề này, khái niệm Anti-Corruption Layer được đưa ra.

Theo đó thì Anti-Corruption Layer là một lớp trung gian giữa hai thành phần phân tán khác nhau trong hệ thống phần mềm, một thành phần được phát triển với một ngôn ngữ hoặc mô hình thiết kế cụ thể, trong khi thành phần còn lại được phát triển với một ngôn ngữ hoặc mô hình thiết kế khác. Lớp này chịu trách nhiệm cho việc chuyển đổi dữ liệu giữa hai ngôn ngữ hoặc mô hình thiết kế khác nhau. Các thành phần sử dụng lớp này để truy cập vào dữ liệu và chức năng của thành phần khác mà không cần biết chi tiết về ngôn ngữ hoặc mô hình thiết kế của thành phần đó. Các tính năng của Anti-Corruption Layer bao gồm:

- Đóng gói tất cả các phần liên quan đến tương tác với các hệ thống bên ngoài vào một nơi duy nhất.
- Tách biệt các phần tương tác với các hệ thống bên ngoài khỏi các phần khác của hệ thống, giúp giảm thiểu rủi ro khi thay đổi các hệ thống bên ngoài.
- Đảm bảo rằng các phần khác của hệ thống của chúng ta không bị ảnh hưởng bởi các thay đổi của các hệ thống bên ngoài.

Ví dụ giả sử chúng ta có hai thành phần trong hệ thống của chúng ta: một thành phần là một ứng dụng web được phát triển bằng ngôn ngữ PHP và mô hình MVC, còn một thành phần khác là một ứng dụng di động được phát triển bằng Java và mô hình MVP. Hai mô hình thiết kế này có các đặc điểm và cách tiếp cận khác nhau, do đó việc tích hợp hai thành phần này lại với nhau là một thách thức lớn. Để giải quyết vấn đề này, chúng ta có thể sử dụng mô hình Anti-Corruption Layer để tạo ra một lớp trung gian chịu trách nhiệm chuyển đổi dữ liệu giữa hai thành phần. Điều này cho phép mỗi thành phần sử dụng ngôn ngữ và mô hình thiết kế của nó để truy cập vào dữ liệu và chức năng của thành phần khác mà không cần biết chi tiết về ngôn ngữ hoặc mô hình thiết kế của thành phần đó.

Anti-Corruption Layer có thể được hiểu như một lớp trung gian đứng giữa các thành phần của hệ thống phần mềm, chịu trách nhiệm xử lý dữ liệu truyền qua giữa các thành phần sao cho đảm bảo tính toàn vẹn và độ chính xác của dữ liệu. Nó giúp đảm bảo tính độc lập và kiểm soát việc chuyển đổi dữ liệu giữa Domain Model và các hệ thống bên ngoài. Các thành phần khác nằm bên ngoài được biết đến là "Legacy Systems" hoặc "External Systems". Việc sử dụng Anti-Corruption Layer giúp cho hệ thống phần mềm không bị ảnh hưởng bởi các hệ thống khác, đặc biệt là các hệ thống cũ hoặc các hệ thống bên ngoài mà không có sự kiểm soát và quản lý.

### Tài liệu tham khảo

* <a href="https://www.infoq.com/articles/ddd-in-practice" target="_blank">https://www.infoq.com/articles/ddd-in-practice</a>
* <a href="https://martinfowler.com/tags/domain%20driven%20design.html" target="_blank">https://martinfowler.com/tags/domain%20driven%20design.html</a>
