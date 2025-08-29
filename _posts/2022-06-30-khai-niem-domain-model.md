---
layout: post
title: Khái niệm Domain Model
description: Domain Model là mô hình khái niệm kết hợp dữ liệu và hành vi để biểu diễn nghiệp vụ cốt lõi của hệ thống. Nó giúp giảm độ phức tạp và tăng tính chính xác trong thiết kế phần mềm.
excerpt: Domain Model là một bản phác thảo các thực thể cơ bản của hệ thống và mối quan hệ giữa chúng. Nó tạo ra mạng lưới các đối tượng phản ánh đúng bản chất nghiệp vụ, giúp cho việc phân tích, thiết kế và bảo trì hệ thống dễ dàng hơn.
thumbnail:
keywords: domain model, khái niệm domain model, mô hình miền, entity, value object, aggregate, repository, service
author: Nguyễn Trường Long
---

### Khái niệm Domain Model

[Domain Model](https://nguyentruonglong.net/khai-niem-domain-model.html) là mô hình khái niệm mô tả các thực thể, hành vi và quan hệ trong một lĩnh vực nghiệp vụ cụ thể. Vai trò của nó là đưa ngữ nghĩa nghiệp vụ vào trung tâm thiết kế để hệ thống nói cùng một ngôn ngữ với doanh nghiệp. Khi Domain Model đúng và rõ ràng, phần mềm trở nên dễ hiểu, dễ kiểm thử và dễ tiến hóa theo yêu cầu mới.

Ba nét đặc trưng quan trọng của Domain Model:

* Kết hợp dữ liệu và hành vi. Mỗi khái niệm nghiệp vụ không chỉ có thuộc tính mà còn có quy tắc và thao tác phù hợp với bản chất của nó.
* Độc lập với công nghệ. Cấu trúc và quy tắc nghiệp vụ không phụ thuộc vào cơ sở dữ liệu hay framework, nhờ đó kiến trúc bền vững hơn.
* Tạo ngôn ngữ chung. Các tên gọi và quy tắc trong mô hình trở thành vốn từ chung giữa kỹ sư và chuyên gia nghiệp vụ, giúp giảm hiểu lầm.

Ví dụ trong hệ thống bán hàng trực tuyến, mô hình có thể bao gồm Đơn hàng, Khách hàng, Sản phẩm và Thanh toán. Mỗi thành phần mang cả thông tin và cách ứng xử. Đơn hàng biết cách tính tổng tiền và kiểm tra điều kiện xác nhận, Sản phẩm biết tình trạng còn hàng, Thanh toán biết trạng thái giao dịch.


### Thành phần chính của Domain Model

#### Entity

Entity là đối tượng có định danh duy nhất và vòng đời riêng. Dù thuộc tính thay đổi theo thời gian, định danh vẫn giúp ta phân biệt đây là cùng một đối tượng. Khách hàng với mã khách hàng cố định, Đơn hàng với mã đơn hàng cố định là các ví dụ quen thuộc.

Điểm cần lưu ý:

* Định danh được sinh ra và bảo toàn trong suốt vòng đời.
* Trạng thái có thể biến đổi nhưng phải tuân thủ các quy tắc nghiệp vụ.
* Hai thực thể chỉ coi là một nếu trùng định danh, không dựa trên so sánh từng thuộc tính.

Khi thiết kế, hãy đặt hành vi gắn chặt với danh tính và bất biến của đối tượng ngay trong Entity để tránh mô hình rỗng.


#### Value Object

Value Object đại diện cho một giá trị có ý nghĩa và được xác định bởi chính các thuộc tính của nó. Không có định danh riêng, thường bất biến để đảm bảo tính an toàn và dễ suy luận. Tiền tệ gồm số tiền và loại tiền, Địa chỉ gồm số nhà, đường, thành phố là những ví dụ điển hình.

Lợi ích khi dùng Value Object:

* Diễn tả khái niệm nghiệp vụ chính xác hơn so với kiểu dữ liệu nguyên thủy.
* Gom các thuộc tính đi cùng nhau thành một đơn vị nhất quán.
* Dễ kiểm soát tính hợp lệ và tái sử dụng quy tắc, ví dụ kiểm tra định dạng địa chỉ hay phép cộng trừ tiền tệ cùng loại.

Hai Value Object bằng nhau khi mọi thuộc tính tương đương về ngữ nghĩa. Cách so sánh dựa trên giá trị giúp giảm lỗi và tăng tính diễn đạt của mô hình.


#### Aggregate

Aggregate là nhóm các Entity và Value Object có liên hệ chặt chẽ và được quản lý như một đơn vị nhất quán. Aggregate có một đầu mối là Aggregate Root. Mọi thao tác từ bên ngoài đi vào Aggregate đều thông qua đầu mối này để bảo toàn bất biến.

Ví dụ quen thuộc là Đơn hàng làm Aggregate Root quản lý danh sách dòng hàng. Việc thêm dòng hàng, cập nhật số lượng hay xác nhận đơn đều đi qua Đơn hàng để giữ các quy tắc như không vượt quá tồn kho, không xác nhận khi thiếu thông tin thanh toán.

Nguyên tắc thực hành:

* Bất biến phải được kiểm tra ở giới hạn của Aggregate.
* Giữa các Aggregate nên tham chiếu lẫn nhau bằng định danh để giảm liên kết chặt.
* Giao dịch nên hoàn tất trong phạm vi một Aggregate để giữ tính nhất quán cục bộ.


#### Repository

Repository cung cấp cổng truy xuất và lưu trữ Entity hoặc Aggregate bằng ngôn ngữ domain. Mục tiêu là để lớp domain không cần biết cơ sở dữ liệu, đồng thời người đọc hiểu được ý định nghiệp vụ qua tên phương thức.

Một Repository tốt có những phẩm chất sau:

* Trả về Aggregate hoàn chỉnh theo đúng ranh giới nhất quán.
* Cung cấp các truy vấn mang ngữ nghĩa nghiệp vụ, ví dụ tìm đơn hàng chờ xác nhận của một khách hàng.
* Ẩn chi tiết hạ tầng và tối ưu lưu trữ ở bên trong, giữ giao diện ổn định cho domain.


#### Service

Service trong domain chứa logic nghiệp vụ không thuộc hẳn về một Entity hay Value Object nào. Thông thường đó là hành vi cần phối hợp nhiều đối tượng. Ví dụ định giá giỏ hàng theo nhiều bảng giá và chương trình khuyến mãi, tính phí vận chuyển theo vùng và trọng lượng.

Phân biệt hai loại thường gặp:

* Domain Service diễn đạt quy tắc cốt lõi, hoạt động trên mô hình và giữ ngôn ngữ domain.
* Application Service điều phối các ca sử dụng, gọi Domain Service và Repository, xử lý giao dịch và chuyển đổi dữ liệu vào ra. Application Service không nên chứa quy tắc nghiệp vụ trọng yếu.


### Quan hệ, bất biến và tính nhất quán

Domain Model không chỉ là danh sách lớp mà còn là mạng lưới quan hệ và các bất biến cần được bảo vệ. Một quan hệ được chọn là thành phần của Aggregate khi nó cần nhất quán giao dịch cùng nhau. Quan hệ ít chặt chẽ hơn nên được mô hình hóa bằng tham chiếu định danh để giảm chi phí đồng bộ và tránh vòng phụ thuộc.

Bất biến là những ràng buộc luôn đúng trong mọi trạng thái hợp lệ. Ví dụ tổng tiền phải bằng tổng dòng hàng sau khuyến mãi, hay đơn đã hủy thì không thể thanh toán. Nơi phù hợp để kiểm tra bất biến là Aggregate Root, vì đây là cổng duy nhất để thay đổi trạng thái bên trong.


### Vòng đời và trạng thái

Mỗi Entity thường đi qua các trạng thái theo thời gian. Hãy mô tả rõ các bước chuyển hợp lệ để tránh lỗi nghiệp vụ. Đơn hàng có thể ở các trạng thái tạo mới, chờ thanh toán, đã xác nhận, đang giao, hoàn tất, đã hủy. Không cho phép nhảy trực tiếp từ tạo mới sang đang giao khi chưa xác nhận thanh toán. Việc ghi lại quy tắc chuyển trạng thái ngay trong mô hình giúp đội ngũ hiểu cùng một cách và ngăn ngừa sai sót từ sớm.


### Domain Event trong mô hình

Sự kiện domain phản ánh điều gì đó có ý nghĩa đã xảy ra, ví dụ đơn hàng được tạo, thanh toán hoàn tất. Việc phát sự kiện giúp tách rời các mối quan tâm, cho phép phần khác của hệ thống phản ứng mà không làm rối Aggregate cốt lõi. Sự kiện nên dùng tên nghiệp vụ, mang theo dữ liệu tối thiểu cần thiết và được phát đúng khoảnh khắc bất biến đã được bảo toàn.


### Ánh xạ lưu trữ và tính nhất quán

Khi đưa mô hình vào lưu trữ, mục tiêu là giữ nguyên ngữ nghĩa domain ở phía trên và giấu đi chi tiết kỹ thuật ở phía dưới. Một số gợi ý thực hành:

* Lưu Value Object như một khối có cấu trúc thay vì rải thành trường rời rạc khó hiểu theo ngữ nghĩa.
* Tải Aggregate theo ranh giới nhất quán, hạn chế lấy từng mảnh rời rạc làm vỡ bất biến.
* Với liên kết giữa Aggregate, cân nhắc nạp lười dựa trên định danh để tránh bùng nổ truy vấn.
* Trong tích hợp đa context, nơi cần nhất quán cuối cùng có thể dùng sự kiện và hàng đợi tin cậy để chuyển giao thay đổi.


### Quy trình xây dựng một Domain Model

Một cách tiếp cận hiệu quả thường đi qua các bước sau:

* Khám phá ngôn ngữ chung bằng các buổi làm việc với chuyên gia nghiệp vụ. Ghi lại thuật ngữ và ví dụ điển hình.
* Phác thảo sự kiện nghiệp vụ quan trọng. Từ sự kiện suy ra lệnh, quy tắc và ranh giới nhất quán.
* Chia thành các ngữ cảnh có ranh giới rõ ràng. Mỗi ngữ cảnh có Domain Model riêng phù hợp với ngôn ngữ của nó.
* Mô hình hóa chiến thuật bên trong ngữ cảnh. Chọn thực thể, giá trị, nhóm thành Aggregate và xác định bất biến.
* Viết thử các ca sử dụng điển hình. Để mô hình bộc lộ điểm vướng và điều chỉnh cho đến khi trôi chảy.

Một ví dụ rút gọn. Người dùng thêm sản phẩm vào giỏ. Giỏ hàng kiểm tra tồn kho, hợp nhất dòng hàng cùng sản phẩm, tính lại tổng tiền bằng cách áp dụng các quy tắc khuyến mãi. Khi đặt hàng, Đơn hàng sinh ra từ giỏ với ảnh chụp giá tại thời điểm đặt, rồi phát sự kiện đặt hàng thành công để khởi động quy trình thanh toán. Từng bước đều dựa vào ngôn ngữ nghiệp vụ rõ ràng, nhờ vậy mô hình dễ đọc và dễ kiểm chứng.


### Khi nào nên áp dụng Domain Model

Domain Model phát huy giá trị trong bối cảnh giàu quy tắc, nhiều trường hợp ngoại lệ và thay đổi thường xuyên. Nếu yêu cầu chỉ là thao tác dữ liệu đơn giản với quy tắc mỏng, cách tiếp cận hướng giao dịch thuần túy có thể phù hợp hơn. Tiêu chí chọn lựa là lợi ích về tính diễn đạt và khả năng tiến hóa có lớn hơn chi phí mô hình hóa hay không.


### Kết luận

Domain Model là hạt nhân giúp phần mềm phản ánh đúng thực tại nghiệp vụ. Khi mô hình kết hợp chặt chẽ dữ liệu và hành vi, tôn trọng bất biến và ranh giới nhất quán, hệ thống trở nên dễ hiểu, dễ thay đổi và ít nợ kỹ thuật. Hãy bắt đầu từ ngôn ngữ chung, để ngôn ngữ dẫn dắt mô hình, rồi để mô hình dẫn dắt kiến trúc. Đó là con đường bền vững cho những sản phẩm sống lâu và tiến hóa liên tục.


### Tài liệu tham khảo

* Eric Evans — *Domain-Driven Design: Tackling Complexity in the Heart of Software*
* Martin Fowler — [Domain Model](https://martinfowler.com/eaaCatalog/domainModel.html)
* InfoQ — [DDD in Practice](https://www.infoq.com/articles/ddd-in-practice)
