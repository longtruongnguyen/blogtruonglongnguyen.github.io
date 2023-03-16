---
layout: post
title: Khái niệm Domain Model
description: Trong công nghệ phần mềm, domain model là một bản phác thảo các thực thể cơ bản của hệ thống và các mối quan hệ giữa chúng. Domain model tạo ra một mạng lưới các đối tượng được kết nối với nhau, trong đó mỗi đối tượng đại diện cho một số cá thể có ý nghĩa như một tập đoàn hay một dòng thông tin trên đơn đặt hàng.
excerpt: Trong công nghệ phần mềm, domain model là một bản phác thảo các thực thể cơ bản của hệ thống và các mối quan hệ giữa chúng. Domain model tạo ra một mạng lưới các đối tượng được kết nối với nhau, trong đó mỗi đối tượng đại diện cho một số cá thể có ý nghĩa như một tập đoàn hay một dòng thông tin trên đơn đặt hàng.
thumbnail:
keywords: khái niệm domain model, domain model, domain model là gì, mô hình miền, mô hình domain model, tìm hiểu domain model
author: Nguyễn Trường Long
---

Trong công nghệ phần mềm, [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) là một mô hình khái niệm của [miền](https://vi.wikipedia.org/wiki/Mi%E1%BB%81n_(c%C3%B4ng_ngh%E1%BB%87_ph%E1%BA%A7n_m%E1%BB%81m)) kết hợp cả hành vi và dữ liệu. [Domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) là một phần quan trọng trong thiết kế hệ thống phần mềm, nó cung cấp một cách tiếp cận để mô tả và hiểu một lĩnh vực cụ thể mà hệ thống sẽ được sử dụng. Domain model thường được sử dụng trong các dự án phần mềm lớn và phức tạp, nơi mà việc hiểu rõ nhu cầu và yêu cầu của khách hàng là rất quan trọng. [Domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) tạo ra một mạng lưới các đối tượng được kết nối với nhau, trong đó mỗi đối tượng đại diện cho một số cá thể có ý nghĩa như một tập đoàn hay một dòng thông tin trên đơn đặt hàng. [Domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) là một bản phác thảo của các thực thể cơ bản của hệ thống và các mối quan hệ giữa chúng. Nó độc lập với nền tảng (không dành cho bất kỳ ngôn ngữ lập trình cụ thể nào) và các thuộc tính không có kiểu dữ liệu. [Domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) được xem như một biểu diễn trực quan có cấu trúc của các khái niệm được kết nối với nhau hoặc các đối tượng trong thế giới thực kết hợp giữa từ vựng, khái niệm chính, hành vi và mối quan hệ của tất cả các thực thể trong đó.

[Domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) có thể được mô tả bằng các biểu đồ lớp (class diagrams), biểu đồ trạng thái (state diagrams), hay các biểu đồ hoạt động (activity diagrams), tùy thuộc vào nhu cầu của dự án. Các thành phần chính của [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) bao gồm:

- <strong>Entity</strong>: Là đối tượng thực tế trong lĩnh vực, có ý nghĩa và được định danh bởi một thuộc tính duy nhất. Ví dụ: trong hệ thống quản lý khách sạn, đối tượng "khách hàng" có thể được đại diện bởi một entity với thuộc tính duy nhất là mã khách hàng.

- <strong>Value object</strong>: Là đối tượng có giá trị nhưng không được định danh duy nhất trong lĩnh vực. Ví dụ: trong hệ thống bán hàng trực tuyến, một đối tượng "địa chỉ" có thể được đại diện bởi một value object gồm các thuộc tính như đường, thành phố và quốc gia.

- <strong>Aggregate</strong>: Là một nhóm các đối tượng liên quan đến nhau, được quản lý và duy trì bởi một đối tượng root. Ví dụ: trong hệ thống quản lý đơn hàng, một aggregate có thể bao gồm các đối tượng liên quan như đơn hàng, khách hàng, sản phẩm và phiếu giao hàng, và được quản lý bởi đối tượng root là đơn hàng.

- <strong>Repository</strong>: Là một interface định nghĩa các phương thức để lưu trữ và truy xuất đối tượng trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html). Repository cung cấp các phương thức như thêm, sửa, xóa và truy vấn để tương tác với cơ sở dữ liệu hoặc bất kỳ hệ thống lưu trữ nào được sử dụng trong hệ thống.

- <strong>Service</strong>: Là một đối tượng thực hiện một hoặc nhiều chức năng trong hệ thống, thường xuyên liên quan đến nhiều đối tượng trong [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html). Ví dụ: trong hệ thống bán hàng trực tuyến, một service "xử lý đơn hàng" có thể thực hiện các chức năng như kiểm tra tính khả dụng của sản phẩm, tính toán giá trị đơn hàng và tạo ra phiếu giao hàng.

Những thành phần này tạo nên một [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) đầy đủ và chi tiết, giúp cho việc phát triển và bảo trì hệ thống phần mềm trở nên dễ dàng hơn. Việc xây dựng một [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) đòi hỏi sự tương tác chặt chẽ giữa các nhà phát triển phần mềm và các chuyên gia về lĩnh vực được mô tả. Các chuyên gia về lĩnh vực có thể cung cấp kiến thức chuyên môn và thông tin chi tiết về các khái niệm, quy trình, và ngữ cảnh liên quan đến lĩnh vực của họ. Các nhà phát triển phần mềm có thể sử dụng thông tin này để xây dựng một [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) chính xác và đáp ứng được yêu cầu của khách hàng.

Khi xây dựng một hệ thống phần mềm, [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) giúp các nhà phát triển hiểu rõ các yêu cầu, quy trình, và ngữ cảnh liên quan đến lĩnh vực của hệ thống. Nó cung cấp một cách tiếp cận toàn diện và cấu trúc hóa để phát triển hệ thống phần mềm, giúp đảm bảo tính chính xác, độ tin cậy, và dễ dàng bảo trì của hệ thống.

Ví dụ, trong một ứng dụng đặt hàng trực tuyến, [domain model](https://nguyentruonglong.net/khai-niem-domain-model.html) sẽ mô tả các đối tượng như Order (đơn hàng), Customer (khách hàng), Product (sản phẩm), Address (địa chỉ), Payment (thanh toán), v.v... Các thuộc tính của các đối tượng sẽ được mô tả, ví dụ như các thuộc tính của đơn hàng như số lượng sản phẩm, giá tiền, địa chỉ nhận hàng, v.v... Các mối quan hệ giữa các đối tượng sẽ được mô tả, ví dụ như một đơn hàng sẽ có nhiều sản phẩm, mỗi sản phẩm sẽ có một giá tiền và một số lượng, mỗi khách hàng sẽ có nhiều đơn hàng,...

### Tài liệu tham khảo
* <a href="https://livebook.manning.com/book/functional-and-reactive-domain-modeling/chapter-1/265" target="_blank">https://livebook.manning.com/book/functional-and-reactive-domain-modeling/chapter-1/265</a>
