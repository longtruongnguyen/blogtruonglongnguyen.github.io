---
layout: post
title: Kiến trúc Domain-Driven Design
description: Domain-Driven Design là một design pattern ở cấp độ hệ thống được áp dụng cho các nghiệp vụ phức tạp. Nó cung cấp cấp các khối lắp ghép (building blocks) chiến lược để phân tích và cấu trúc cho các vấn đề và giải pháp.
keywords: Domain-Driven Design, design pattern, DDD, mô hình Domain-Driven Design, kiến trúc Domain-Driven Design, mô hình DDD, kiến trúc DDD, Domain Model, Entity, Value Object, Service, Bounded Context, Anti-Corruption Layer
excerpt: Domain-Driven Design là một design pattern ở cấp độ hệ thống được áp dụng cho các nghiệp vụ phức tạp. Nó cung cấp cấp các khối lắp ghép (building blocks) chiến lược để phân tích và cấu trúc cho các vấn đề và giải pháp.
author: Nguyễn Trường Long
---

### Giới thiệu về Domain-Driven Design

[Domain-Driven Design (DDD)](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) là một phương pháp thiết kế phần mềm được phát triển bởi Eric Evans vào năm 2003, và được đặc trưng bởi việc tập trung vào việc phân tích và thiết kế phần mềm xung quanh các domain chính của doanh nghiệp.

DDD được phát triển nhằm giải quyết các vấn đề mà các nhà phát triển phần mềm thường gặp phải trong quá trình thiết kế các ứng dụng doanh nghiệp. Trong quá trình thiết kế, các nhà phát triển thường phải đối mặt với việc phân tích các yêu cầu phức tạp từ người sử dụng, đồng thời cũng phải đối mặt với các yêu cầu về tính mở rộng và bảo trì của ứng dụng. [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) tập trung vào việc hiểu và mô hình hóa lĩnh vực (domain) của hệ thống, đồng thời giải quyết các vấn đề phức tạp trong thiết kế phần mềm. [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) giúp tạo ra các hệ thống phần mềm dễ bảo trì, mở rộng, đáp ứng nhu cầu của khách hàng và linh hoạt trong việc thay đổi.

Hướng tiếp cận khi xây dựng hệ thống của [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) bộc lộ những ưu điểm chính sau:

- <i>Hiểu và phân tích lĩnh vực (domain) của hệ thống</i>: [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) đưa ra phương pháp phân tích và mô hình hóa lĩnh vực (domain) của hệ thống bằng cách sử dụng các phương pháp như Event Storming, User Story Mapping, Domain Modeling, Ubiquitous Language... Điều này giúp xây dựng một mô hình lĩnh vực (domain model) chính xác và đầy đủ, giúp cho việc phát triển hệ thống dễ dàng hơn.
- <i>Tách biệt lớp domain và các lớp khác</i>: [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) giúp phân tách các lớp của hệ thống để dễ dàng bảo trì và mở rộng. Trong đó, lớp domain là trung tâm của hệ thống và được quan tâm đến nhiều nhất. Lớp domain đóng vai trò quan trọng trong việc định nghĩa các luật chung của lĩnh vực (business rules) và giúp kiểm soát và hạn chế sự phát triển của các lớp khác.
 - <i>Sử dụng Ubiquitous Language</i>: Ubiquitous Language là một ngôn ngữ chung được sử dụng bởi tất cả các thành viên trong dự án để truyền đạt và hiểu các khái niệm và thuật ngữ trong lĩnh vực. Dùng Ubiquitous Language giúp cho các thành viên trong dự án hiểu nhau dễ dàng hơn, giảm thiểu sự hiểu nhầm và tăng tính chính xác trong việc phát triển.
- <i>Áp dụng các mẫu thiết kế (design patterns) và kiến trúc (architecture)</i>: [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) sử dụng các mẫu thiết kế và kiến trúc để tạo ra các hệ thống phần mềm có tính mở rộng, dễ bảo trì và đáp ứng nhu cầu của khách hàng. 

Trong bài viết này chúng ta sẽ cùng lướt qua các khái niệm chính trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) như Domain Model, Entity, Value Object, Service, Bounded Context, Anti-Corruption Layer. Các tài liệu trong phạm vi bài viết này được tham khảo chủ yếu đến từ blog của tác giả Martin Fowler và sách của tác giả Eric Evans.

### Domain Model

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Domain Model đóng vai trò rất quan trọng và là một phần không thể thiếu trong việc thiết kế và phát triển các hệ thống phức tạp. Domain Model cung cấp cho nhóm phát triển một cách nhìn tổng thể về lĩnh vực và các yêu cầu kinh doanh, giúp họ hiểu rõ hơn về hệ thống cần được phát triển và xây dựng một giải pháp phù hợp. Domain Model là một biểu diễn trừu tượng của các khái niệm, quy trình và quan hệ trong một lĩnh vực (domain) cụ thể. Nó được thiết kế để miêu tả các đối tượng, hành vi và quy trình trong lĩnh vực đó và được sử dụng để hỗ trợ cho các quyết định thiết kế và phát triển của hệ thống. Domain Model được tạo ra từ việc sử dụng các ngôn ngữ bổ sung như Ubiquitous Language để phát triển một mô hình chung, đại diện cho tất cả các khía cạnh trong nghiệp vụ phát triển hệ thống. Việc tạo ra mô hình chung này giúp tất cả các thành viên trong nhóm phát triển đồng nhất về các khái niệm và hành động trong lĩnh vực đó, giúp cho việc truyền đạt thông tin và giao tiếp trở nên dễ dàng hơn. Domain Model giúp giảm thiểu sự phức tạp trong hệ thống phần mềm bằng cách tập trung vào các khái niệm và hành động quan trọng trong lĩnh vực cụ thể. Điều này giúp giảm thiểu sự mơ hồ và tập trung vào những điểm quan trọng, từ đó giúp cho việc phát triển và bảo trì hệ thống trở nên dễ dàng hơn. Bằng cách xác định các thực thể và quan hệ giữa chúng trong lĩnh vực cụ thể, việc tích hợp các thành phần khác nhau của hệ thống trở nên hiệu quả.

### Entity

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Entity là một đối tượng trong hệ thống có tính nhất quán và có thể được định danh bằng một ID duy nhất. Điều này có nghĩa là cho dù cho các thuộc tính của Entity có thay đổi đi chăng nữa, nó vẫn được coi là một đối tượng duy nhất nếu nó có cùng ID.

Một Entity có thể có nhiều thuộc tính, phương thức hay hành vi. Thông thường thì Entity sẽ có một số thuộc tính quan trọng được sử dụng để định danh nó và xác định những thuộc tính khác của nó. Khái niệm Entity trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) mang một số đặc điểm sau:

- Entity được xác định bởi một ID duy nhất.
- Entity là một đối tượng độc lập, có thể tồn tại một mình hoặc được liên kết với các đối tượng khác.
- Entity có thể có thuộc tính, phương thức và logic nghiệp vụ kinh doanh riêng của nó.
- Entity có thể có một số trạng thái khác nhau trong vòng đời của nó.

Ví dụ như một Entity "Order" trong hệ thống bán hàng có thể có các thuộc tính như "order number", "customer", "total amount", và "order date". Tất cả các đơn hàng đều có một mã đơn hàng duy nhất để xác định nó. Do đó đây là một ví dụ của một đối tượng được xác định bởi tính định danh của nó.

Entity thường được sử dụng để đại diện cho các đối tượng trong hệ thống thực tế, chẳng hạn như đơn hàng, khách hàng, sản phẩm, các đối tượng vật lý hoặc trừu tượng trong nghiệp vụ kinh doanh. Nó cũng thường được sử dụng để lưu trữ và truy xuất dữ liệu từ cơ sở dữ liệu.

### Value Object

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Value Object (đối tượng giá trị) là một đối tượng đại diện cho một giá trị không thay đổi hoặc không thể thay đổi, nhưng không phải là một định danh riêng biệt (identity) như Entity (đối tượng thực thể). Với các giá trị này thì chúng ta không phải quan tâm đến định danh, mà chỉ quan tâm đến các thuộc tính của nó.

Value Object có các đặc điểm sau:
 - Không có tính chất định danh: Value Object không được xác định bởi một định danh riêng biệt. Thay vào đó, nó được xác định bởi giá trị của các thuộc tính của nó.
- Không có tính chất thay đổi: Value Object là không thể thay đổi, có nghĩa là giá trị của nó không thể bị thay đổi sau khi nó được tạo ra.
- Không có tính chất tồn tại độc lập: Value Object không tồn tại độc lập. Thay vào đó, nó là một phần của một đối tượng khác, ví dụ như Entity hoặc một đối tượng giá trị lớn hơn.

Value Object thường được sử dụng để biểu diễn các giá trị như địa chỉ, tiền tệ, thời gian, số lượng,... Chúng ta cần sử dụng Value Object khi giá trị được biểu diễn là không thể thay đổi và không cần phải có một định danh riêng biệt. Các đối tượng Value Object thường được sử dụng để giảm sự phức tạp của hệ thống và tăng tính rõ ràng trong thiết kế, đồng thời giúp cho các đối tượng Entity trở nên đơn giản hơn. Ngoài ra chúng cũng giúp xác định và phân loại các thuộc tính trong hệ thống theo các khái niệm thực tế.

Lấy ví dụ trong một hệ thống quản lý đơn hàng, một đơn hàng có thể bao gồm các Value Object như địa chỉ giao hàng, ngày đặt hàng và phương thức thanh toán. Các Value Object này không có định danh riêng và không thể được phân biệt bởi các thuộc tính. Chúng chỉ đơn giản là các giá trị mô tả cho đơn hàng đó.

Trong ví dụ khác như ở một hệ thống quản lý tài sản, một tài sản (asset) có thể bao gồm các Value Object như trạng thái hiện tại, ngày mua và giá trị tài sản. Những giá trị này cũng là các thông tin mô tả về tài sản và không có định danh riêng.

### Service

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Service là một khái niệm quan trọng của việc mô hình hóa và thiết kế các hệ thống. Service đại diện cho các chức năng hoặc nhiệm vụ cụ thể mà hệ thống phải thực hiện, thường liên quan đến các thao tác xử lý dữ liệu hoặc tương tác giữa các thành phần khác nhau trong hệ thống. Nó là một phương thức hoặc hành động không thuộc về một Entity hoặc Value Object cụ thể nào. Service thường được sử dụng để thực hiện các hành động liên quan đến nhiều Entity hoặc các hành động phức tạp mà không thể thực hiện bằng cách chỉ sử dụng một Entity.

Một Service có thể bao gồm các thao tác CRUD (Create, Read, Update, Delete) hoặc các thao tác phức tạp hơn như xử lý giao dịch, phân tích dữ liệu, tính toán phức tạp, tương tác với các API bên ngoài và các hệ thống khác, và các nhiệm vụ khác liên quan đến logic kinh doanh của hệ thống.

Service thường được triển khai dưới dạng các phương thức trong các lớp của ứng dụng hoặc được triển khai bằng các service bên ngoài (ví dụ: RESTful API, giao thức RPC,...). Các Service thường được phân loại theo Bounded Context để đảm bảo tính chính xác và sự độc lập giữa các nhiệm vụ khác nhau trong hệ thống.

Ví dụ về Service trong hệ thống bán lẻ có thể là "CheckoutService", "OrderService" hoặc "PaymentService", mỗi Service đóng vai trò quản lý một phần của quy trình mua hàng. Các Service này có thể tương tác với các Entity như "Product", "Customer", "Order" hoặc các Value Object như "ShippingAddress", "PaymentMethod".

### Bounded Context

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Bounded Context là một khái niệm quan trọng để giúp tổ chức và quản lý các thành phần của hệ thống phần mềm. Bounded Context được định nghĩa là một ranh giới rõ ràng và giới hạn của một phần trong hệ thống phần mềm, trong đó các thuật ngữ, hành vi, quy trình, và mô hình được định nghĩa và áp dụng một cách chặt chẽ và rõ ràng.

Một Bounded Context có thể bao gồm nhiều thực thể (Entities) và giá trị (Value Objects), cũng như các dịch vụ (Services) liên quan đến chức năng của Bounded Context đó. Tuy nhiên, một thực thể hoặc giá trị có thể có nhiều Bounded Context khác nhau và được định nghĩa khác nhau trong từng Bounded Context. Vì vậy, một cách tiếp cận đúng đắn trong việc thiết kế hệ thống phần mềm là phải cân nhắc và xác định rõ ràng Bounded Context và quản lý các liên kết giữa các Bounded Context. Các thuật ngữ và quan hệ giữa các đối tượng chỉ áp dụng trong phạm vi của Bounded Context. Nó cho phép tách và tổ chức các phần của một hệ thống phức tạp thành các thành phần nhỏ hơn và dễ quản lý hơn.

Bounded Context có một số đặc điểm sau:
- <b>Rõ ràng và giới hạn</b>: Bounded Context được định nghĩa rõ ràng và có giới hạn. Nó được xác định bởi các giới hạn chức năng hoặc giới hạn doanh nghiệp.
- <b>Độc lập</b>: Mỗi Bounded Context có thể độc lập với nhau và có thể tồn tại một cách riêng biệt trong hệ thống phần mềm.
- <b>Ngôn ngữ hóa</b>: Các thuật ngữ, hành vi, quy trình, và mô hình trong Bounded Context phải được định nghĩa và áp dụng một cách chặt chẽ và rõ ràng.
- <b>Liên kết</b>: Các liên kết giữa các Bounded Context cần được quản lý và xác định rõ ràng để tránh xung đột hoặc nhầm lẫn trong việc triển khai hệ thống phần mềm.

Ví dụ chúng ta đang phát triển một hệ thống bán hàng trực tuyến, trong đó có hai context chính là "Quản lý sản phẩm" và "Quản lý đơn hàng". Mỗi context sẽ có một Domain Model riêng, với các Entity, Value Object và Service riêng biệt. Trong context "Quản lý sản phẩm", các khái niệm quan trọng có thể bao gồm: Product, Category, Review, Image, Supplier, Stock, và các service như ProductService, CategoryService, ImageService. Trong context "Quản lý đơn hàng", các khái niệm quan trọng có thể bao gồm: Order, Customer, Payment, Shipping, OrderItem, và các service như OrderService, PaymentService, ShippingService.

Việc phân chia thành các Bounded Context khác nhau sẽ giúp chúng ta tập trung vào các yêu cầu và quy trình kinh doanh cụ thể trong mỗi context, đồng thời giảm thiểu sự phức tạp và sự rắc rối khi phát triển hệ thống. Ngoài ra, Bounded Context cũng giúp định rõ các giới hạn và các quy tắc liên quan đến quản lý dữ liệu và logic kinh doanh, giúp tăng tính linh hoạt và tái sử dụng của hệ thống.

### Anti-Corruption Layer

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Anti-Corruption Layer (ACL) là một lớp được sử dụng để giữ cho các thành phần của hệ thống không bị ảnh hưởng bởi các thành phần khác nằm bên ngoài, đặc biệt là các thành phần được thiết kế bởi các nhóm khác hoặc bên thứ ba. Khi một hệ thống phần mềm được phát triển trên nhiều nền tảng và có các thành phần khác nhau, nhưng các thành phần này không tuân thủ cùng một ngôn ngữ chung, điều này dẫn đến sự khó khăn trong việc tích hợp các thành phần này với nhau. Để giải quyết vấn đề này, khái niệm Anti-Corruption Layer được đưa ra.

Theo đó thì Anti-Corruption Layer là một lớp trung gian giữa hai thành phần phân tán khác nhau trong hệ thống phần mềm, một thành phần được phát triển với một ngôn ngữ hoặc mô hình thiết kế cụ thể, trong khi thành phần còn lại được phát triển với một ngôn ngữ hoặc mô hình thiết kế khác. Lớp này chịu trách nhiệm cho việc chuyển đổi dữ liệu giữa hai ngôn ngữ hoặc mô hình thiết kế khác nhau. Các thành phần sử dụng lớp này để truy cập vào dữ liệu và chức năng của thành phần khác mà không cần biết chi tiết về ngôn ngữ hoặc mô hình thiết kế của thành phần đó. Các tính năng của Anti-Corruption Layer bao gồm:

- Đóng gói tất cả các phần liên quan đến tương tác với các hệ thống bên ngoài vào một nơi duy nhất.
- Tách biệt các phần tương tác với các hệ thống bên ngoài khỏi các phần khác của hệ thống, giúp giảm thiểu rủi ro khi thay đổi các hệ thống bên ngoài.
- Đảm bảo rằng các phần khác của hệ thống của chúng ta không bị ảnh hưởng bởi các thay đổi của các hệ thống bên ngoài.

Ví dụ giả sử chúng ta có hai thành phần trong hệ thống của chúng ta: một thành phần là một ứng dụng web được phát triển bằng ngôn ngữ PHP và mô hình MVC, còn một thành phần khác là một ứng dụng di động được phát triển bằng Java và mô hình MVP. Hai mô hình thiết kế này có các đặc điểm và cách tiếp cận khác nhau, do đó việc tích hợp hai thành phần này lại với nhau là một thách thức lớn. Để giải quyết vấn đề này, chúng ta có thể sử dụng mô hình Anti-Corruption Layer để tạo ra một lớp trung gian chịu trách nhiệm chuyển đổi dữ liệu giữa hai thành phần. Điều này cho phép mỗi thành phần sử dụng ngôn ngữ và mô hình thiết kế của nó để truy cập vào dữ liệu và chức năng của thành phần khác mà không cần biết chi tiết về ngôn ngữ hoặc mô hình thiết kế của thành phần đó.

Anti-Corruption Layer có thể được hiểu như một lớp trung gian đứng giữa các thành phần của hệ thống phần mềm, chịu trách nhiệm xử lý dữ liệu truyền qua giữa các thành phần sao cho đảm bảo tính toàn vẹn và độ chính xác của dữ liệu. Nó giúp đảm bảo tính độc lập và kiểm soát việc chuyển đổi dữ liệu giữa Domain Model và các hệ thống bên ngoài. Các thành phần khác nằm bên ngoài được biết đến là "Legacy Systems" hoặc "External Systems". Việc sử dụng Anti-Corruption Layer giúp cho hệ thống phần mềm không bị ảnh hưởng bởi các hệ thống khác, đặc biệt là các hệ thống cũ hoặc các hệ thống bên ngoài mà không có sự kiểm soát và quản lý.

### Tài liệu tham khảo

* <a href="https://opus.ch/ddd-concepts-and-patterns-introduction-and-overview/" target="_blank">https://opus.ch/ddd-concepts-and-patterns-introduction-and-overview/</a>
* <a href="https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design" target="_blank">https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design</a>
* <a href="https://www.infoq.com/articles/ddd-in-practice" target="_blank">https://www.infoq.com/articles/ddd-in-practice</a>
* <a href="https://martinfowler.com/tags/domain%20driven%20design.html" target="_blank">https://martinfowler.com/tags/domain%20driven%20design.html</a>
