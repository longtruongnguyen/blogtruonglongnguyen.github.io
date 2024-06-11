---
layout: post
title: Kiến trúc Domain-Driven Design
description: Domain-Driven Design là một design pattern ở cấp độ hệ thống được áp dụng cho các nghiệp vụ phức tạp. Nó cung cấp các khối lắp ghép chiến lược để phân tích và cấu trúc cho các vấn đề và giải pháp.
keywords: Domain-Driven Design, design pattern, DDD, mô hình Domain-Driven Design, kiến trúc Domain-Driven Design, mô hình DDD, kiến trúc DDD, Domain Model, Entity, Value Object, Service, Factory, Aggregate, Repository, Module, Bounded Context, Anti-Corruption Layer
excerpt: Domain-Driven Design là một design pattern ở cấp độ hệ thống được áp dụng cho các nghiệp vụ phức tạp. Nó cung cấp các khối lắp ghép chiến lược để phân tích và cấu trúc cho các vấn đề và giải pháp.
author: Nguyễn Trường Long
---

### Giới thiệu về Domain-Driven Design

[Domain-Driven Design (DDD)](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) là một phương pháp thiết kế phần mềm được phát triển bởi Eric Evans vào năm 2003, và được đặc trưng bởi việc tập trung vào việc phân tích và thiết kế phần mềm xung quanh các domain chính của doanh nghiệp.

DDD được phát triển nhằm giải quyết các vấn đề mà các nhà phát triển phần mềm thường gặp phải trong quá trình thiết kế các ứng dụng doanh nghiệp. Trong quá trình thiết kế, các nhà phát triển thường phải đối mặt với việc phân tích các yêu cầu phức tạp từ người sử dụng, đồng thời cũng phải đối mặt với các yêu cầu về tính mở rộng và bảo trì của ứng dụng. [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) tập trung vào việc hiểu và mô hình hóa lĩnh vực (domain) của hệ thống, đồng thời giải quyết các vấn đề phức tạp trong thiết kế phần mềm. [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) giúp tạo ra các hệ thống phần mềm dễ bảo trì, mở rộng, đáp ứng nhu cầu của khách hàng và linh hoạt trong việc thay đổi.

Hướng tiếp cận khi xây dựng hệ thống của [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) bộc lộ những ưu điểm chính sau:

- **Hiểu và phân tích lĩnh vực (domain) của hệ thống**: [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) đưa ra phương pháp phân tích và mô hình hóa lĩnh vực (domain) của hệ thống bằng cách sử dụng các phương pháp như Event Storming, User Story Mapping, Domain Modeling, Ubiquitous Language... Điều này giúp xây dựng một mô hình lĩnh vực (domain model) chính xác và đầy đủ, giúp cho việc phát triển hệ thống dễ dàng hơn.
- **Tách biệt lớp domain và các lớp khác**: [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) giúp phân tách các lớp của hệ thống để dễ dàng bảo trì và mở rộng. Trong đó, lớp domain là trung tâm của hệ thống và được quan tâm đến nhiều nhất. Lớp domain đóng vai trò quan trọng trong việc định nghĩa các luật chung của lĩnh vực (business rules) và giúp kiểm soát và hạn chế sự phát triển của các lớp khác.
- **Sử dụng Ubiquitous Language**: Ubiquitous Language là một ngôn ngữ chung được sử dụng bởi tất cả các thành viên trong dự án để truyền đạt và hiểu các khái niệm và thuật ngữ trong lĩnh vực. Dùng Ubiquitous Language giúp cho các thành viên trong dự án hiểu nhau dễ dàng hơn, giảm thiểu sự hiểu nhầm và tăng tính chính xác trong việc phát triển.
- **Áp dụng các mẫu thiết kế (design patterns) và kiến trúc (architecture)**: [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) sử dụng các mẫu thiết kế và kiến trúc để tạo ra các hệ thống phần mềm có tính mở rộng, dễ bảo trì và đáp ứng nhu cầu của khách hàng.

Các mẫu pattern cơ bản trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html) có thể được chia thành hai loại là pattern chiến thuật và pattern chiến lược. Các pattern chiến thuật được sử dụng trong khi xây dựng mô hình miền và trong mã nguồn. Các mẫu chiến lược ở mức cao hơn và được sử dụng để xây dựng hệ thống ở mức kiến trúc. Chúng ta sẽ đi vào chi tiết của từng pattern và do đó trước hết cần liệt kê tổng quát ở đây một vài pattern chính.

##### Tactical Patterns

- Entity
- Value Object
- Factory
- Service
- Aggregate
- Repository
- Module

##### Strategic Patterns

- Bounded Context
- Context Map
- Model Integrity Patterns
- Core Domain

Các tài liệu trong phạm vi bài viết này được tham khảo chủ yếu đến từ blog của tác giả Martin Fowler và sách của tác giả Eric Evans.

### Domain Model

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Domain Model đóng vai trò rất quan trọng và là một phần không thể thiếu trong việc thiết kế và phát triển các hệ thống phức tạp. Domain Model cung cấp cho nhóm phát triển một cách nhìn tổng thể về lĩnh vực và các yêu cầu kinh doanh, giúp họ hiểu rõ hơn về hệ thống cần được phát triển và xây dựng một giải pháp phù hợp. Domain Model là một biểu diễn trừu tượng của các khái niệm, quy trình và quan hệ trong một lĩnh vực (domain) cụ thể. Nó được thiết kế để miêu tả các đối tượng, hành vi và quy trình trong lĩnh vực đó và được sử dụng để hỗ trợ cho các quyết định thiết kế và phát triển của hệ thống. Domain Model được tạo ra từ việc sử dụng các ngôn ngữ bổ sung như Ubiquitous Language để phát triển một mô hình chung, đại diện cho tất cả các khía cạnh trong nghiệp vụ phát triển hệ thống. Việc tạo ra mô hình chung này giúp tất cả các thành viên trong nhóm phát triển đồng nhất về các khái niệm và hành động trong lĩnh vực đó, giúp cho việc truyền đạt thông tin và giao tiếp trở nên dễ dàng hơn. Domain Model giúp giảm thiểu sự phức tạp trong hệ thống phần mềm bằng cách tập trung vào các khái niệm và hành động quan trọng trong lĩnh vực cụ thể. Điều này giúp giảm thiểu sự mơ hồ và tập trung vào những điểm quan trọng, từ đó giúp cho việc phát triển và bảo trì hệ thống trở nên dễ dàng hơn. Bằng cách xác định các thực thể và quan hệ giữa chúng trong lĩnh vực cụ thể, việc tích hợp các thành phần khác nhau của hệ thống trở nên hiệu quả.

### Entity

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Entity là một đối tượng trong hệ thống có tính nhất quán và có thể được định danh bằng một ID duy nhất. Điều này có nghĩa là cho dù các thuộc tính của Entity có thay đổi đi chăng nữa, nó vẫn được coi là một đối tượng duy nhất nếu nó có cùng ID.

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

### Factory

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Factory là một mẫu thiết kế được sử dụng để tạo ra các đối tượng phức tạp. Factory cung cấp một cách tiếp cận để tạo ra các đối tượng mà không cần phải chỉ rõ chính xác lớp của đối tượng đó. Điều này giúp tách biệt logic tạo ra các đối tượng khỏi logic sử dụng các đối tượng đó, giúp hệ thống dễ dàng mở rộng và bảo trì.

Factory có thể được triển khai dưới dạng các phương thức hoặc lớp trong hệ thống. Nó giúp giảm thiểu sự phụ thuộc giữa các thành phần trong hệ thống và tăng tính linh hoạt của mã nguồn. Ví dụ trong hệ thống bán hàng, chúng ta có thể sử dụng một Factory để tạo ra các đối tượng "Order" hoặc "Product" mà không cần biết chi tiết về cách các đối tượng này được tạo ra. Điều này giúp cho việc thay đổi cách tạo ra các đối tượng này trở nên dễ dàng hơn mà không ảnh hưởng đến các phần khác của hệ thống.

Một Factory có thể sử dụng các tham số để tạo ra các đối tượng với các thuộc tính khác nhau, giúp tăng tính linh hoạt và khả năng tái sử dụng của mã nguồn. Ví dụ, trong một hệ thống quản lý sản phẩm, chúng ta có thể có một "ProductFactory" với các phương thức để tạo ra các loại sản phẩm khác nhau, chẳng hạn như sản phẩm điện tử, quần áo, hoặc đồ gia dụng. Mỗi phương thức trong "ProductFactory" sẽ tạo ra một đối tượng "Product" với các thuộc tính và cấu hình phù hợp với loại sản phẩm đó.

Factory cũng có thể được sử dụng để áp dụng các quy tắc nghiệp vụ phức tạp khi tạo ra các đối tượng. Ví dụ, trong một hệ thống quản lý đơn hàng, một "OrderFactory" có thể kiểm tra các điều kiện như số lượng sản phẩm, trạng thái khách hàng, hoặc các ưu đãi giảm giá trước khi tạo ra đối tượng "Order". Điều này giúp đảm bảo rằng tất cả các đơn hàng được tạo ra đều tuân thủ các quy tắc nghiệp vụ của hệ thống.

Ngoài ra, Factory có thể kết hợp với các mẫu thiết kế khác như Singleton hoặc Prototype để quản lý việc tạo ra các đối tượng trong hệ thống. Ví dụ, một "Singleton Factory" có thể đảm bảo rằng chỉ có một phiên bản duy nhất của một đối tượng được tạo ra trong toàn bộ hệ thống, giúp tiết kiệm tài nguyên và đảm bảo tính nhất quán.

### Aggregate

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Aggregate là một nhóm các đối tượng có liên quan với nhau, được xử lý như một đơn vị duy nhất trong các thao tác. Aggregate được sử dụng để đảm bảo tính nhất quán trong các thao tác liên quan đến nhiều đối tượng.

Mỗi Aggregate có một "root" (gốc) được gọi là "Aggregate Root". Aggregate Root là một Entity duy nhất quản lý toàn bộ Aggregate và là điểm truy cập duy nhất cho các thao tác trên Aggregate. Các đối tượng khác trong Aggregate không thể được truy cập trực tiếp từ bên ngoài Aggregate mà chỉ thông qua Aggregate Root.

Ví dụ trong hệ thống quản lý đơn hàng, một "Order" có thể là một Aggregate Root, và các "OrderItem" có thể là các đối tượng bên trong Aggregate này. Các thao tác liên quan đến "Order" và "OrderItem" sẽ được thực hiện thông qua "Order", đảm bảo tính nhất quán của toàn bộ Aggregate.

Aggregate giúp kiểm soát tính toàn vẹn của dữ liệu bằng cách áp đặt các quy tắc nghiệp vụ và ràng buộc trên các đối tượng bên trong nó. Ví dụ, trong một hệ thống quản lý tài chính, một "Account" có thể là một Aggregate Root, và các "Transaction" có thể là các đối tượng bên trong Aggregate này. Các quy tắc nghiệp vụ như "số dư tài khoản không được âm" hoặc "mỗi giao dịch phải có một loại cụ thể" sẽ được áp dụng thông qua "Account", đảm bảo rằng tất cả các giao dịch đều tuân thủ các quy tắc này.

Aggregate cũng giúp tối ưu hóa hiệu suất của hệ thống bằng cách giới hạn phạm vi của các thao tác đồng bộ. Thay vì phải đồng bộ hóa toàn bộ hệ thống mỗi khi có một thay đổi nhỏ, chỉ cần đồng bộ hóa Aggregate tương ứng. Điều này giúp giảm thiểu chi phí đồng bộ hóa và tăng hiệu suất của hệ thống. Ví dụ, trong một hệ thống quản lý kho hàng, một "Warehouse" có thể là một Aggregate Root, và các "InventoryItem" có thể là các đối tượng bên trong Aggregate này. Khi cập nhật số lượng hàng tồn kho, chỉ cần đồng bộ hóa "Warehouse" và các "InventoryItem" liên quan, không cần phải đồng bộ hóa toàn bộ hệ thống kho hàng.

Ngoài ra, Aggregate giúp tăng tính rõ ràng và dễ hiểu của mô hình domain bằng cách nhóm các đối tượng có liên quan với nhau. Điều này giúp cho việc phát triển và bảo trì hệ thống trở nên dễ dàng hơn. Ví dụ, trong một hệ thống quản lý dự án, một "Project" có thể là một Aggregate Root, và các "Task", "Milestone" và "Resource" có thể là các đối tượng bên trong Aggregate này. Bằng cách nhóm các đối tượng có liên quan với nhau, mô hình domain trở nên dễ hiểu và dễ quản lý hơn.

### Repository

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Repository là một mẫu thiết kế được sử dụng để quản lý việc lưu trữ và truy xuất các đối tượng từ cơ sở dữ liệu. Repository cung cấp một giao diện để thực hiện các thao tác CRUD (Create, Read, Update, Delete) trên các đối tượng mà không cần biết chi tiết về cách các đối tượng này được lưu trữ.

Repository giúp tách biệt logic lưu trữ khỏi logic nghiệp vụ, giúp hệ thống dễ dàng mở rộng và bảo trì. Nó cung cấp một cách tiếp cận nhất quán để làm việc với các đối tượng trong cơ sở dữ liệu và giảm sự phụ thuộc giữa các thành phần trong hệ thống.

Ví dụ trong hệ thống bán hàng, chúng ta có thể có các Repository như "OrderRepository", "ProductRepository" để quản lý việc lưu trữ và truy xuất các đối tượng "Order" và "Product". Các Repository này cung cấp các phương thức để thêm, cập nhật, xóa và truy vấn các đối tượng từ cơ sở dữ liệu.

Repository không chỉ giúp quản lý việc lưu trữ mà còn có thể được sử dụng để thực hiện các truy vấn phức tạp và tối ưu hóa hiệu suất của hệ thống. Ví dụ, trong một hệ thống quản lý khách hàng, một "CustomerRepository" có thể cung cấp các phương thức để tìm kiếm khách hàng dựa trên nhiều tiêu chí khác nhau như tên, địa chỉ, hoặc lịch sử mua hàng. Điều này giúp tách biệt logic truy vấn khỏi logic nghiệp vụ và làm cho mã nguồn dễ dàng bảo trì hơn.

Repository cũng giúp tăng tính linh hoạt của hệ thống bằng cách cho phép thay đổi cách lưu trữ và truy xuất dữ liệu mà không ảnh hưởng đến các phần khác của hệ thống. Ví dụ, trong một hệ thống quản lý đơn hàng, một "OrderRepository" có thể bắt đầu sử dụng một cơ sở dữ liệu NoSQL thay vì một cơ sở dữ liệu quan hệ mà không cần thay đổi logic nghiệp vụ của hệ thống. Điều này giúp hệ thống dễ dàng thích nghi với các thay đổi về công nghệ và yêu cầu nghiệp vụ.

Ngoài ra, Repository có thể kết hợp với các mẫu thiết kế khác như Unit of Work để quản lý các thay đổi trong một phiên làm việc duy nhất. Điều này giúp đảm bảo tính toàn vẹn của dữ liệu và giảm thiểu các xung đột dữ liệu. Ví dụ, trong một hệ thống quản lý tài chính, một "TransactionRepository" có thể sử dụng Unit of Work để quản lý các thay đổi trong một phiên làm việc duy nhất, đảm bảo rằng tất cả các giao dịch đều được xử lý đúng và nhất quán.

### Module

Trong [Domain-Driven Design](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), Module là một khái niệm được sử dụng để tổ chức và phân chia các thành phần của hệ thống thành các đơn vị logic. Module giúp quản lý sự phức tạp của hệ thống bằng cách nhóm các thành phần có liên quan lại với nhau, giúp hệ thống dễ hiểu và dễ bảo trì hơn.

Module thường được sử dụng để nhóm các đối tượng, dịch vụ và các thành phần khác có liên quan đến một lĩnh vực cụ thể trong hệ thống. Điều này giúp tăng tính rõ ràng và tính nhất quán của mã nguồn, đồng thời giảm sự phụ thuộc giữa các thành phần trong hệ thống.

Ví dụ trong hệ thống bán hàng, chúng ta có thể tổ chức các thành phần liên quan đến "Quản lý sản phẩm" vào một module, và các thành phần liên quan đến "Quản lý đơn hàng" vào một module khác. Mỗi module sẽ chứa các đối tượng, dịch vụ và các thành phần khác có liên quan đến lĩnh vực đó, giúp hệ thống dễ hiểu và dễ bảo trì hơn.

Module không chỉ giúp tổ chức mã nguồn mà còn giúp quản lý các phụ thuộc giữa các thành phần trong hệ thống. Bằng cách nhóm các thành phần có liên quan lại với nhau, Module giúp giảm sự phụ thuộc giữa các thành phần, làm cho hệ thống dễ dàng mở rộng và bảo trì hơn. Ví dụ, trong một hệ thống quản lý dự án, chúng ta có thể tổ chức các thành phần liên quan đến "Quản lý công việc" vào một module, và các thành phần liên quan đến "Quản lý tài nguyên" vào một module khác. Điều này giúp giảm sự phụ thuộc giữa các thành phần và làm cho mã nguồn dễ hiểu hơn.

Module cũng giúp tăng tính tái sử dụng của mã nguồn bằng cách nhóm các thành phần có liên quan lại với nhau. Các thành phần trong một module có thể được tái sử dụng trong các module khác mà không cần phải viết lại mã nguồn. Ví dụ, trong một hệ thống quản lý kho hàng, chúng ta có thể tạo ra một module "Quản lý sản phẩm" chứa các đối tượng và dịch vụ liên quan đến sản phẩm. Module này có thể được tái sử dụng trong các hệ thống khác như hệ thống bán lẻ hoặc hệ thống quản lý tài sản mà không cần phải viết lại mã nguồn.

Ngoài ra, Module giúp cải thiện quy trình phát triển phần mềm bằng cách chia hệ thống thành các phần nhỏ hơn và dễ quản lý hơn. Điều này giúp cho việc phát triển, kiểm thử và triển khai hệ thống trở nên dễ dàng hơn. Ví dụ, trong một hệ thống quản lý doanh nghiệp, chúng ta có thể chia hệ thống thành các module như "Quản lý nhân sự", "Quản lý tài chính" và "Quản lý khách hàng". Mỗi module sẽ được phát triển, kiểm thử và triển khai độc lập, giúp giảm thiểu rủi ro và tăng tính linh hoạt của hệ thống.

Để hiểu thêm về các mẫu thiết kế chiến lược trong Domain-Driven Design, có thể tham khảo bài viết chi tiết về [các mẫu thiết kế chiến lược](https://nguyentruonglong.net/kien-truc-domain-driven-design-cac-mau-thiet-ke-chien-luoc.html).

### Tài liệu tham khảo

* [https://opus.ch/ddd-concepts-and-patterns-introduction-and-overview/](https://opus.ch/ddd-concepts-and-patterns-introduction-and-overview/)
* [https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design](https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design)
* [https://www.infoq.com/articles/ddd-in-practice](https://www.infoq.com/articles/ddd-in-practice)
* [https://martinfowler.com/tags/domain%20driven%20design.html](https://martinfowler.com/tags/domain%20driven%20design.html)
