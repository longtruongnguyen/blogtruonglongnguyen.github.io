---
layout: post
title: Khái niệm Domain Model
description: Trong công nghệ phần mềm, domain model là một bản phác thảo các thực thể cơ bản của hệ thống và các mối quan hệ giữa chúng. Domain model tạo ra một mạng lưới các đối tượng được kết nối với nhau, trong đó mỗi đối tượng đại diện cho một số cá thể có ý nghĩa như một tập đoàn hay một dòng thông tin trên đơn đặt hàng.
excerpt: Trong công nghệ phần mềm, domain model là một bản phác thảo các thực thể cơ bản của hệ thống và các mối quan hệ giữa chúng. Domain model tạo ra một mạng lưới các đối tượng được kết nối với nhau, trong đó mỗi đối tượng đại diện cho một số cá thể có ý nghĩa như một tập đoàn hay một dòng thông tin trên đơn đặt hàng.
thumbnail:
keywords: khái niệm domain model, domain model, domain model là gì, mô hình miền, mô hình domain model, tìm hiểu domain model, aggregate, entity
author: Nguyễn Trường Long
---

Trong công nghệ phần mềm, [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) là một mô hình khái niệm của [miền](https://vi.wikipedia.org/wiki/Mi%E1%BB%81n_(c%C3%B4ng_ngh%E1%BB%87_ph%E1%BA%A7n_m%E1%BB%81m)) kết hợp cả hành vi và dữ liệu. [Domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) là một phần quan trọng trong thiết kế hệ thống phần mềm, nó cung cấp một cách tiếp cận để mô tả và hiểu một lĩnh vực cụ thể mà hệ thống sẽ được sử dụng. [Domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) thường được sử dụng trong các dự án phần mềm lớn và phức tạp, nơi mà việc hiểu rõ nhu cầu và yêu cầu của khách hàng là rất quan trọng. [Domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) tạo ra một mạng lưới các đối tượng được kết nối với nhau, trong đó mỗi đối tượng đại diện cho một số cá thể có ý nghĩa như một tập đoàn hay một dòng thông tin trên đơn đặt hàng. [Domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) là một bản phác thảo của các thực thể cơ bản của hệ thống và các mối quan hệ giữa chúng. Nó độc lập với nền tảng (không dành cho bất kỳ ngôn ngữ lập trình cụ thể nào) và các thuộc tính không có kiểu dữ liệu. [Domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) được xem như một biểu diễn trực quan có cấu trúc của các khái niệm được kết nối với nhau hoặc các đối tượng trong thế giới thực kết hợp giữa từ vựng, khái niệm chính, hành vi và mối quan hệ của tất cả các thực thể trong đó.

[Domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) có thể được mô tả bằng các biểu đồ lớp (class diagrams), biểu đồ trạng thái (state diagrams), hay các biểu đồ hoạt động (activity diagrams), tùy thuộc vào nhu cầu của dự án. Các thành phần chính của [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) bao gồm:

- <strong>Entity</strong>: Là đối tượng thực tế trong lĩnh vực, có ý nghĩa và được định danh bởi một thuộc tính duy nhất. Ví dụ: trong hệ thống quản lý khách sạn, đối tượng "khách hàng" có thể được đại diện bởi một entity với thuộc tính duy nhất là mã khách hàng.

- <strong>Value object</strong>: Là đối tượng có giá trị nhưng không được định danh duy nhất trong lĩnh vực. Ví dụ: trong hệ thống bán hàng trực tuyến, một đối tượng "địa chỉ" có thể được đại diện bởi một value object gồm các thuộc tính như đường, thành phố và quốc gia.

- <strong>Aggregate</strong>: Là một nhóm các đối tượng liên quan đến nhau, được quản lý và duy trì bởi một đối tượng root. Ví dụ: trong hệ thống quản lý đơn hàng, một aggregate có thể bao gồm các đối tượng liên quan như đơn hàng, khách hàng, sản phẩm và phiếu giao hàng, và được quản lý bởi đối tượng root là đơn hàng.

- <strong>Repository</strong>: Là một interface định nghĩa các phương thức để lưu trữ và truy xuất đối tượng trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html). Repository cung cấp các phương thức như thêm, sửa, xóa và truy vấn để tương tác với cơ sở dữ liệu hoặc bất kỳ hệ thống lưu trữ nào được sử dụng trong hệ thống.

- <strong>Service</strong>: Là một đối tượng thực hiện một hoặc nhiều chức năng trong hệ thống, thường xuyên liên quan đến nhiều đối tượng trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html). Ví dụ: trong hệ thống bán hàng trực tuyến, một service "xử lý đơn hàng" có thể thực hiện các chức năng như kiểm tra tính khả dụng của sản phẩm, tính toán giá trị đơn hàng và tạo ra phiếu giao hàng.

Những thành phần này tạo nên một [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) đầy đủ và chi tiết, giúp cho việc phát triển và bảo trì hệ thống phần mềm trở nên dễ dàng hơn. Việc xây dựng một [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) đòi hỏi sự tương tác chặt chẽ giữa các nhà phát triển phần mềm và các chuyên gia về lĩnh vực được mô tả. Các chuyên gia về lĩnh vực có thể cung cấp kiến thức chuyên môn và thông tin chi tiết về các khái niệm, quy trình, và ngữ cảnh liên quan đến lĩnh vực của họ. Các nhà phát triển phần mềm có thể sử dụng thông tin này để xây dựng một [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) chính xác và đáp ứng được yêu cầu của khách hàng.

Khi xây dựng một hệ thống phần mềm, [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) giúp các nhà phát triển hiểu rõ các yêu cầu, quy trình, và ngữ cảnh liên quan đến lĩnh vực của hệ thống. Nó cung cấp một cách tiếp cận toàn diện và cấu trúc hóa để phát triển hệ thống phần mềm, giúp đảm bảo tính chính xác, độ tin cậy, và dễ dàng bảo trì của hệ thống.

Ví dụ, trong một ứng dụng đặt hàng trực tuyến, [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) sẽ mô tả các đối tượng như Order (đơn hàng), Customer (khách hàng), Product (sản phẩm), Address (địa chỉ), Payment (thanh toán),... Các thuộc tính của các đối tượng sẽ được mô tả, ví dụ như các thuộc tính của đơn hàng như số lượng sản phẩm, giá tiền, địa chỉ nhận hàng,... Các mối quan hệ giữa các đối tượng sẽ được mô tả, ví dụ như một đơn hàng sẽ có nhiều sản phẩm, mỗi sản phẩm sẽ có một giá tiền và một số lượng, mỗi khách hàng sẽ có nhiều đơn hàng,...

### Khái niệm Entity trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html)

Entity là một khái niệm quan trọng trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html), vì nó giúp định nghĩa và đại diện cho các đối tượng trong hệ thống. Đây là một đối tượng có tính định danh và có sự tồn tại riêng biệt trong hệ thống. 

Một Entity có thể được coi như là một thực thể hoặc đối tượng có tính chất độc lập, độc nhất và không thể thay đổi. Các Entity thường được lưu trữ trong cơ sở dữ liệu và có thể được truy vấn, cập nhật hoặc xóa.

Ví dụ về Entity trong hệ thống quản lý bán hàng có thể là sản phẩm. Sản phẩm có các thuộc tính như tên, mô tả, giá, số lượng tồn kho và mã sản phẩm. Trong hệ thống, sản phẩm được coi là một Entity bởi vì nó có tính định danh (mã sản phẩm) và có sự tồn tại riêng biệt. Nó cũng có thể được lưu trữ trong cơ sở dữ liệu và được truy vấn để lấy thông tin hoặc cập nhật thông tin.

Một ví dụ khác về Entity là một tài khoản người dùng trong một hệ thống quản lý thành viên. Tài khoản người dùng có các thuộc tính như tên đăng nhập, mật khẩu, địa chỉ email và định danh người dùng (user ID). Trong hệ thống, tài khoản người dùng được coi là một Entity bởi vì nó có tính định danh (user ID) và có sự tồn tại riêng biệt. Tài khoản người dùng cũng có thể được lưu trữ trong cơ sở dữ liệu và được truy vấn để lấy thông tin hoặc cập nhật thông tin.

### Khái niệm Aggregate trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html)

Aggregate được coi là một phần quan trọng trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html). Aggregate là một nhóm các đối tượng liên quan đến nhau và được quản lý như một đơn vị truy vấn/cập nhật dữ liệu trong hệ thống phần mềm. Aggregate có thể bao gồm nhiều Entity và Value Object, và có một Aggregate Root chịu trách nhiệm quản lý các đối tượng trong Aggregate.

Aggregate giúp định nghĩa và đại diện cho các đối tượng có mối liên kết chặt chẽ với nhau trong hệ thống. Một Aggregate thường có một Aggregate Root, đó là một đối tượng chịu trách nhiệm quản lý các đối tượng khác trong Aggregate.

Các đối tượng trong Aggregate liên kết chặt chẽ với nhau và thường được quản lý bởi Aggregate Root. Trong khi đó, các đối tượng nằm ngoài Aggregate thường không được quản lý trực tiếp bởi Aggregate Root và không được truy cập từ bên ngoài Aggregate.

Một Aggregate có thể bao gồm nhiều Entity và Value Object, và chúng liên kết với nhau theo một quy tắc cụ thể. Ví dụ trong hệ thống quản lý bán hàng, một Aggregate có thể là một đơn hàng với các Entity như sản phẩm, khách hàng, địa chỉ giao hàng, thanh toán,... Các Entity này liên kết với nhau theo một quy tắc cụ thể và đều phụ thuộc vào Aggregate Root là đơn hàng.

Khi truy vấn hoặc cập nhật dữ liệu cho một Aggregate, chúng ta cần thực hiện thông qua Aggregate Root. Tất cả các thao tác này đều được thực hiện một cách an toàn và đồng bộ. Nếu ta muốn thao tác với một đối tượng riêng lẻ trong Aggregate, ta cần truy cập thông qua Aggregate Root và thực hiện thao tác theo quy tắc cụ thể của Aggregate.

### Khái niệm Value Object trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html)

Trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html), Value Object là một đối tượng không có sự định danh duy nhất và được sử dụng để đại diện cho các giá trị hay thuộc tính của một đối tượng Entity trong hệ thống phần mềm. Nó không có tính chất thay đổi trạng thái và được sử dụng để đại diện cho các giá trị hay thuộc tính của một đối tượng Entity, tạo ra giá trị mới từ các thuộc tính của nó.

Value Object có giá trị chỉ được xác định bởi các thuộc tính của nó. Nó không có một ID hay khóa chính để định danh duy nhất và không được quản lý bởi một Aggregate. Thay vào đó, Value Object được sử dụng để tạo ra một giá trị mới từ các thuộc tính của nó và không có tính chất thay đổi trạng thái.

Một số ví dụ về Value Object có thể bao gồm ngày tháng, giờ, địa chỉ, số điện thoại, tọa độ vị trí, số tiền,... Ví dụ, trong một hệ thống quản lý khách hàng, địa chỉ khách hàng có thể được đại diện bởi một Value Object gồm các thuộc tính như số nhà, tên đường, thành phố, quốc gia,...

Một điểm quan trọng khi sử dụng Value Object là chúng không được truy cập trực tiếp bởi bên ngoài. Thay vào đó, các đối tượng Entity sẽ sử dụng chúng để thực hiện các thao tác và truy xuất dữ liệu. Sử dụng Value Object có thể giúp đơn giản hóa kiến trúc, giảm độ phức tạp và tăng tính linh hoạt của hệ thống. Nó cũng có thể giúp cho việc thực hiện các thao tác với dữ liệu dễ dàng hơn và tăng tính nhất quán của dữ liệu trong hệ thống.

### Khái niệm Repository trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html)

Repository là một khái niệm quan trọng của [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html), được sử dụng để quản lý truy cập và lưu trữ dữ liệu của ứng dụng, đại diện cho một lớp trừu tượng để tương tác với cơ sở dữ liệu. Nó được sử dụng để tách lớp dịch vụ và lớp lưu trữ (data access layer), giúp cho code của chúng ta dễ đọc, dễ bảo trì hơn. Repository cung cấp một giao diện để truy xuất, thêm, sửa đổi và xóa dữ liệu từ cơ sở dữ liệu hoặc bất kỳ nguồn dữ liệu nào khác mà hệ thống của bạn có thể sử dụng.

Repository định nghĩa một số phương thức để tương tác với cơ sở dữ liệu, bao gồm phương thức lấy danh sách các đối tượng, phương thức tìm kiếm đối tượng theo ID, phương thức lưu đối tượng mới và cập nhật đối tượng có sẵn trong cơ sở dữ liệu.

Một ví dụ đơn giản của Repository trong thiết kế hệ thống phần mềm là khi chúng ta có một đối tượng User trong ứng dụng của mình. Chúng ta có thể sử dụng một Repository để tương tác với cơ sở dữ liệu của hệ thống để xử lý thông tin liên quan đến đối tượng User. Repository của User sẽ cung cấp các phương thức để truy vấn và thao tác dữ liệu người dùng từ cơ sở dữ liệu, ví dụ như lấy tất cả người dùng, tìm kiếm người dùng bằng tên, thêm mới người dùng, cập nhật thông tin người dùng hoặc xóa người dùng khỏi cơ sở dữ liệu. Repository giúp cho các lớp dịch vụ không phải quan tâm đến cách lấy và lưu trữ dữ liệu, mà chỉ cần gọi các phương thức từ Repository để thực hiện các thao tác này.

Việc sử dụng Repository trong thiết kế hệ thống phần mềm giúp cho việc quản lý dữ liệu trở nên đơn giản và linh hoạt hơn, đồng thời giúp giảm thiểu sự phụ thuộc vào các nguồn dữ liệu cụ thể. Nó cũng giúp cho việc kiểm thử và bảo trì ứng dụng dễ dàng hơn bởi vì các logic truy vấn và xử lý dữ liệu được đóng gói và tách rời khỏi các thành phần khác trong ứng dụng của chúng ta.

### Khái niệm Service trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html)

Trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html), Service là một phần quan trọng giúp xác định và thực hiện các chức năng và nhiệm vụ cụ thể của hệ thống, đại diện cho các hành động hoặc nghiệp vụ được thực hiện bởi hệ thống. Service tập trung vào việc cung cấp các chức năng chính cho hệ thống bao gồm như xử lý và trả về dữ liệu cho người dùng, tính toán và xử lý các dữ liệu được lưu trữ trong cơ sở dữ liệu và tương tác với các hệ thống khác.

Một Service thường được tạo ra bằng cách kết hợp các đối tượng và hành động của [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) để thực hiện một tác vụ cụ thể. Service thường đóng vai trò trung gian giữa giao diện người dùng và cơ sở dữ liệu, giúp các thành phần khác của hệ thống tương tác và trao đổi thông tin.

Ví dụ trong một ứng dụng quản lý đơn hàng, Service có thể được tạo ra để thực hiện các chức năng như tạo mới đơn hàng, xử lý đơn hàng, cập nhật trạng thái đơn hàng, và xóa đơn hàng. Để thực hiện các nghiệp vụ này, Service có thể sử dụng các đối tượng như Order, Customer, Payment, và Shipping, cũng như thao tác với cơ sở dữ liệu để lưu trữ và truy xuất thông tin. Service này cũng có thể đảm nhận các nhiệm vụ như xác minh thông tin đặt hàng, kiểm tra tính khả dụng của sản phẩm, tính toán tổng giá trị đơn hàng và lưu trữ thông tin đặt hàng vào cơ sở dữ liệu. Ngoài ra thì một Service có thể kết hợp với Repository để lấy dữ liệu và lưu trữ dữ liệu, cũng như với các đối tượng khác như Entity và Value Object để xử lý và định dạng dữ liệu.

### Tài liệu tham khảo
* <a href="https://livebook.manning.com/book/functional-and-reactive-domain-modeling/chapter-1/265" target="_blank">https://livebook.manning.com/book/functional-and-reactive-domain-modeling/chapter-1/265</a>
