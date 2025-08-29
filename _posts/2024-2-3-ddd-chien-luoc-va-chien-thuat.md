---
layout: post
title: "Kiến trúc Domain-Driven Design: Mẫu chiến lược và chiến thuật"
description: "Domain-Driven Design là cách tiếp cận thiết kế phần mềm tập trung vào ngôn ngữ và mô hình nghiệp vụ. Bài viết trình bày đầy đủ các mẫu thiết kế chiến lược như Bounded Context, Context Map, Model Integrity và Core Domain, đồng thời hệ thống hóa các mẫu chiến thuật để đưa mô hình vào mã nguồn."
keywords: "Domain-Driven Design, DDD, Bounded Context, Context Map, Model Integrity Patterns, Core Domain, Tactical Patterns, Entity, Value Object, Aggregate, Repository, Factory, Domain Service, Application Service, Domain Event, Anti-Corruption Layer"
excerpt: "Toàn cảnh Domain-Driven Design ở cấp chiến lược và chiến thuật. Cách xác lập ranh giới Bounded Context, vẽ Context Map, bảo toàn tính toàn vẹn của mô hình và tập trung nguồn lực cho Core Domain, cùng bộ mẫu chiến thuật để hiện thực hóa mô hình trong mã nguồn."
author: "Nguyễn Trường Long"
---

### Giới thiệu

Trong kiến trúc [Domain-Driven Design (DDD)](https://nguyentruonglong.net/kien-truc-domain-driven-design.html), các mẫu thiết kế chiến lược định hình cấu trúc ở tầm toàn hệ thống, còn các mẫu chiến thuật biến mô hình nghiệp vụ thành mã nguồn rõ ràng và có thể kiểm thử. Khi hai tầng này ăn khớp, hệ thống giữ được tính diễn đạt của ngôn ngữ nghiệp vụ, đồng thời vẫn linh hoạt trước thay đổi.

Bài viết đi theo hai lớp tư duy. Trước hết là lớp chiến lược để xác lập ranh giới, mối quan hệ và trọng tâm giá trị. Sau đó là lớp chiến thuật để tổ chức thực thể, giá trị, nhóm nhất quán và cổng truy xuất dữ liệu. Phần cuối liên kết hai lớp bằng ví dụ nghiệp vụ xuyên suốt.

---

### Toàn cảnh thiết kế chiến lược

Chiến lược trong DDD trả lời bốn câu hỏi lớn: mô hình nào thuộc về đâu, các mô hình nói chuyện với nhau thế nào, làm sao bảo toàn tính toàn vẹn khi mở rộng và phần nào xứng đáng nhận nhiều đầu tư nhất.

#### Bounded Context

Bounded Context là ranh giới trong đó một mô hình và ngôn ngữ nghiệp vụ được định nghĩa và sử dụng một cách nhất quán. Mỗi ranh giới mang theo từ vựng riêng, quy tắc riêng, nhịp triển khai riêng.

* Cách nhận diện. Nhìn vào mục tiêu nghiệp vụ, quy tắc tính toán và nhóm người dùng. Nếu cùng thuật ngữ nhưng ý nghĩa khác nhau ở hai nhóm, khả năng cao cần hai context tách biệt.
* Ubiquitous Language theo context. Thuật ngữ có thể trùng tên nhưng nghĩa khác. Ví dụ Giá trong bối cảnh Niêm yết có thể khác Giá trong bối cảnh Khuyến mãi.
* Triển khai độc lập. Một context có thể thay đổi mô hình nội bộ mà không làm vỡ các context khác, miễn là hợp đồng tích hợp được giữ ổn định.

Ví dụ trong thương mại điện tử thường có ba context rõ ràng: Quản lý sản phẩm, Đơn hàng và Thanh toán. Ba context này có nhịp phát triển khác nhau, quy tắc khác nhau và vòng đời dữ liệu khác nhau.

#### Context Map

Khi đã có nhiều Bounded Context, cần một bức tranh thể hiện quan hệ giữa chúng. Context Map mô tả luồng dữ liệu, phụ thuộc, mức chủ động của từng bên và chiến lược chống lẫn lộn mô hình.

* Partnership. Hai nhóm cùng chịu trách nhiệm, cùng lập kế hoạch và điều chỉnh mô hình để đáp ứng mục tiêu chung.
* Shared Kernel. Chia sẻ một phần mô hình cốt lõi đã được thỏa thuận. Phần chia sẻ nhỏ, ổn định và có quy trình thay đổi nghiêm ngặt.
* Customer và Supplier. Một context tiêu thụ dữ liệu do context khác cung cấp. Lịch phát hành và hợp đồng dữ liệu cần minh bạch để tránh tắc nghẽn.
* Conformist. Bên tiêu thụ chấp nhận mô hình của bên cung cấp. Thường dùng khi không có quyền thay đổi nguồn dữ liệu.
* Anti Corruption Layer. Lớp chuyển đổi và cách ly để bảo vệ mô hình nội bộ khỏi mô hình bên ngoài. Dữ liệu được dịch sang ngôn ngữ của context đích.
* Open Host Service. Bên cung cấp mở giao diện tiêu chuẩn hóa để nhiều context sử dụng mà không cần tích hợp riêng lẻ.

Một Context Map tốt giúp các nhóm thảo luận bằng sự kiện và hợp đồng thay vì giả định và suy diễn.

#### Model Integrity Patterns

Mục tiêu của nhóm mẫu này là bảo toàn tính nhất quán của mô hình khi hệ thống phát triển theo chiều ngang lẫn chiều dọc.

* Ranh giới nhất quán ở mức Aggregate. Thay đổi phải đi qua đầu mối để bất biến được kiểm tra tại cửa vào.
* Giao dịch hẹp. Cố gắng giữ giao dịch gói gọn trong một Aggregate. Giữa các Aggregate dùng định danh và nhất quán cuối cùng khi cần.
* Sự kiện domain để lan truyền thay đổi. Phát thông điệp sau khi bất biến nội bộ đã bền vững. Bên nhận tự quyết định thời điểm đồng bộ.

#### Core Domain

Core Domain là phần tạo ra giá trị khác biệt cho doanh nghiệp. Đây là nơi cần ngôn ngữ sắc nét, mô hình tinh gọn và tiêu chuẩn chất lượng cao.

* Tập trung nguồn lực tốt nhất. Chất lượng thiết kế, độ bao phủ kiểm thử và khả năng phân rã cần cao hơn phần còn lại.
* Bảo vệ khỏi nhiễu. Dùng Anti Corruption Layer khi tích hợp đòi hỏi thỏa hiệp lớn, tránh để mô hình ngoại lai phá vỡ ngôn ngữ cốt lõi.
* Loại bỏ phần không cốt lõi khỏi lớp domain. Những việc như báo cáo định kỳ, đồng bộ dữ liệu, gửi thông báo có thể đặt ở các context hỗ trợ.

---

### Bộ mẫu thiết kế chiến thuật

Các mẫu chiến thuật giúp hiện thực hóa mô hình trong phạm vi một Bounded Context. Chúng trả lời câu hỏi mô hình nội bộ trông ra sao và mã nguồn tổ chức thế nào để bảo toàn ngôn ngữ và bất biến.

#### Entity

Thực thể có định danh duy nhất và vòng đời riêng. So sánh thực thể dựa trên định danh thay vì từng thuộc tính. Hành vi gắn liền với tính đồng nhất phải nằm trong thực thể để tránh mô hình rỗng.

#### Value Object

Đối tượng được xác định bằng giá trị. Thường bất biến, có thể được kiểm tra tính hợp lệ khi khởi tạo. Dùng Value Object để gói các trường đi cùng nhau, ví dụ Tiền tệ hoặc Địa chỉ, giúp quy tắc nghiệp vụ mạch lạc và an toàn.

#### Aggregate và Aggregate Root

Nhóm các thực thể và giá trị có liên hệ chặt chẽ, với một đầu mối điều phối. Tất cả thay đổi trạng thái từ bên ngoài đi vào thông qua đầu mối để bất biến nội bộ luôn đúng. Giữa các Aggregate tham chiếu bằng định danh để giảm liên kết chặt.

#### Repository

Cổng truy xuất lưu trữ cho Aggregate hoặc Entity. Giao diện nói theo ngôn ngữ domain, ẩn chi tiết hạ tầng. Trả về một Aggregate hoàn chỉnh trong ranh giới nhất quán, đồng thời hỗ trợ các truy vấn mang nghĩa nghiệp vụ.

#### Factory

Vị trí gom logic khởi tạo phức tạp, tạo đối tượng ở trạng thái hợp lệ ngay từ đầu. Hữu ích khi cần xây nhiều thành phần con hoặc áp dụng nhiều kiểm tra ràng buộc lúc sinh đối tượng.

#### Domain Service

Nơi đặt quy tắc nghiệp vụ quan trọng không thuộc riêng một thực thể hay giá trị nào. Thường điều phối nhiều đối tượng để thực hiện một phép tính hoặc quyết định có ý nghĩa nghiệp vụ.

#### Application Service

Lớp điều phối ca sử dụng. Gọi Domain Service, làm việc với Repository, quản lý giao dịch, ánh xạ dữ liệu vào ra. Không chứa quy tắc nghiệp vụ cốt lõi để tránh làm mờ domain.

#### Domain Event

Tín hiệu cho biết điều có ý nghĩa đã xảy ra trong domain. Giúp tách rời mối quan tâm và kết nối lỏng giữa các phần. Sự kiện được đặt tên bằng ngôn ngữ nghiệp vụ và mang theo dữ liệu đủ dùng.

#### Module

Cách nhóm các khái niệm có liên quan để giảm độ phức tạp nhận thức. Tên module nên phản ánh từ vựng trong context để người đọc định hướng nhanh.

#### Specification và Unit of Work

Specification diễn đạt tiêu chí nghiệp vụ có thể kết hợp và tái sử dụng. Unit of Work theo dõi thay đổi trong một phiên làm việc để áp dụng lưu trữ một cách an toàn và gọn ghẽ.

---

### Kết nối chiến lược với chiến thuật

Chiến lược vạch đường đi, chiến thuật chọn bước chân. Sau khi vẽ được Boundaries và Context Map, mỗi Bounded Context sẽ áp dụng bộ mẫu chiến thuật để triển khai mô hình nội tại. Anti Corruption Layer ở rìa context dùng ngôn ngữ bản địa ở phía trong và ngôn ngữ đối tác ở phía ngoài, Domain Event bắc cầu giữa context mà không làm chúng khóa chặt vào nhau. Core Domain nhận thêm thời gian tinh chỉnh thực thể, giá trị và bất biến, còn các context hỗ trợ ưu tiên đơn giản và ổn định.

---

### Ví dụ tổng hợp theo dòng nghiệp vụ

Giả sử một nền tảng bán lẻ trực tuyến với ba context: Sản phẩm, Đơn hàng và Thanh toán.

Trong Sản phẩm, Giá niêm yết và Tồn kho thuộc ngôn ngữ riêng. Sự kiện Cập nhật tồn kho phát ra khi nhập hàng. Context Đơn hàng nhận định danh sản phẩm, tra cứu qua hợp đồng dữ liệu đã chuẩn hóa hoặc qua lớp cách ly. Đơn hàng là Aggregate Root nắm danh sách dòng hàng. Khi thêm dòng hàng, bất biến về tồn kho và giới hạn giỏ được kiểm tra. Sau khi người dùng xác nhận, sự kiện Đơn hàng được tạo phát đi.

Context Thanh toán lắng nghe sự kiện này. Ứng với mỗi phương thức thanh toán sẽ có logic xác minh riêng. Khi giao dịch thành công, sự kiện Thanh toán hoàn tất được phát lại. Đơn hàng nhận sự kiện và chuyển trạng thái từ chờ thanh toán sang đã xác nhận. Các bước trên tránh giao dịch phân tán nhờ giữ nhất quán cục bộ trong từng Aggregate và lan truyền bằng sự kiện giữa các context.

---

### Khi nào nên áp dụng

Cách tiếp cận này đặc biệt hiệu quả trong miền nghiệp vụ phong phú, nhiều quy tắc và thường xuyên thay đổi. Với bài toán thuần ghi nhận dữ liệu, chi phí mô hình hóa có thể không tương xứng. Dấu hiệu nên cân nhắc DDD là khi nhóm thường xuyên tranh luận về thuật ngữ, khi cùng một từ có nhiều nghĩa và khi thay đổi nhỏ ở một nơi kéo theo hiệu ứng dây chuyền ở nơi khác.

---

### Kết luận

Chiến lược đặt nền, chiến thuật dựng nhà. Bằng việc xác lập ranh giới rõ ràng, mô tả mối quan hệ giữa các context, bảo toàn tính toàn vẹn của mô hình và tập trung nỗ lực vào phần cốt lõi, DDD giúp hệ thống lớn vẫn giữ được sự mạch lạc. Khi bộ mẫu chiến thuật được áp dụng nhất quán bên trong từng context, mô hình trở nên sống động, dễ bảo trì và sẵn sàng cho mở rộng.

---

### Tài liệu tham khảo

* Eric Evans — *Domain-Driven Design: Tackling Complexity in the Heart of Software*  
* [InfoQ - Strategic Design Patterns](https://www.infoq.com/articles/ddd-in-practice)  
* [Microsoft Learn - Introduction to DDD](https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design)  
* [Martin Fowler - DDD](https://martinfowler.com/tags/domain%20driven%20design.html)  
