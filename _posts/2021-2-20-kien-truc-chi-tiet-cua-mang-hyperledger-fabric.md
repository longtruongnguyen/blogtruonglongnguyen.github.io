---
layout: post
title: Kiến trúc chi tiết của mạng Hyperledger Fabric
description: Hyperledger Fabric là dự án blockchain được phát triển bởi Linux Foundation. Hyperledger Fabric được thiết kế như một nền tảng để phát triển các ứng dụng có kiến trúc module, cho phép nhiều tổ chức tương tác lẫn nhau trong mạng.
excerpt: Hyperledger Fabric là dự án blockchain được phát triển bởi Linux Foundation. Hyperledger Fabric được thiết kế như một nền tảng để phát triển các ứng dụng có kiến trúc module, cho phép nhiều tổ chức tương tác lẫn nhau trong mạng.
thumbnail: 
keywords: mạng Hyperledger Fabric, blockchain, smart contract, chaincode, Membership Service Provider, peer, ledger, Hyperledger
author: Nguyễn Trường Long
---


### Giới thiệu về mạng Hyperledger Fabric

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/HyperledgerFabricWorkFlow.png" alt="Mô hình hoạt động của mạng Hyperledger Fabric">
  <figcaption>
	  <i>Mô hình hoạt động của <a href="https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html" target="_blank">mạng Hyperledger Fabric</a></i>
  </figcaption>
</center>
</figure>

[Mạng Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) bao gồm nhiều tổ chức tương tác lẫn nhau trong mạng. Ví dụ một tổ chức có thể là một ngân hàng trong một mạng lưới bao gồm các tổ chức tài chính hoặc một đối tác vận chuyển trong một mạng lưới chuỗi cung ứng. Mỗi tổ chức có cơ quan cấp chứng chỉ Fabric và một hoặc nhiều node ngang hàng (peer node). Một mạng Fabric cũng có một ordering service được chia sẻ bởi tất cả tổ chức trong mạng và thành phần này giúp xử lý giao dịch cho mạng lưới. Chúng ta sẽ đi vào mô tả chi tiết từng khái niệm và thành phần.

Một tổ chức trong mạng được định nghĩa bởi chứng chỉ gốc (root certificate) dành cho riêng tổ chức đó. Các user và những thành phần khác cũng được định danh bằng các chứng chỉ và các chứng chỉ này đều có nguồn gốc từ chứng chỉ gốc. Điều này giúp đảm bảo các tổ chức khác trong mạng có thể liên hệ người dùng với tổ chức của họ. Các chứng chỉ này cũng chỉ định các quyền cho từng thực thể trên mạng, chẳng hạn như read-only so với full access trên một kênh.
Chứng chỉ gốc của một tổ chức được lưu trữ trên Fabric certificate authority (CA). Fabric CA cũng cấp chứng chỉ cho người dùng trong một tổ chức và xử lý các hoạt động liên quan khác. Fabric CA cấp doanh nghiệp sử dụng nhiều thành phần khác nhau và có thể được triển khai theo nhiều cách khác nhau bằng cách sử dụng Hardware Security Module (HSM) để bảo vệ chứng chỉ gốc.

Một tổ chức cũng tạo ra một hoặc nhiều peer node để thay mặt thực hiện các hoạt động cho tổ chức đó. Cụ thể, một peer node xác nhận các giao dịch được đề xuất trên mạng, lưu trữ và thực thi mã hợp đồng thông minh (được gọi là chaincode trong Fabric) và lưu trữ bản sao cục bộ của sổ cái để truy cập. Fabric clients thường tương tác với peer node để đọc sổ cái, thêm chaincode mới vào mạng hoặc đề xuất một giao dịch mới. Một peer node thường chạy trên chính máy tính của nó.

### Mô hình Hyperledger Fabric

- <i>Assets</i>: Có thể hiểu asset trong [mạng Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) được định nghĩa là mọi thứ có giá trị bao gồm tài sản hữu hình và tài sản vô hình (hợp đồng và tài sản trí tuệ). Hyperledger Fabric cung cấp khả năng chỉnh sửa tài sản bằng cách sử dụng các chaincode transaction. Asset được biểu diễn trong Hyperledger Fabric dưới dạng tập hợp các cặp key-value. Các trạng thái thay đổi được ghi lại dưới dạng transaction trên một Channel ledger. Asset có thể được biểu diễn dưới dạng nhị phân hoặc JSON.
- <i>Chaincode</i>: Chaincode là phần mềm xác định asset và transaction instruction để sửa đổi asset. Nói cách khác, chain code mang bản chất business logic. Chaincode thực thi các quy tắc để chỉnh sửa key-value trong state database. Các hàm chaincode được thực thi dựa trên state database hiện tại của ledger và được khởi tạo thông qua đề xuất transaction.
- <i>Ledger Features</i>: Ledger được sắp xếp theo trình tự, có khả năng chống giả mạo các thay đổi trong [mạng Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html). Chuyển đổi trạng thái là kết quả của các lệnh gọi chaincode được gửi bởi những bên tham gia vào mạng. Kết quả của mỗi transaction là tập hợp các cặp khóa-giá trị được commit đến Ledger như tạo, cập nhật và xóa.

### Các thành phần của mạng Hyperledger Fabric

 - Peer Nodes (Node ngang hàng): Peer nodes là các nút mạng trong [mạng blockchain Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html), chứa dữ liệu và xử lý các giao dịch. Các peer nodes có thể được cấu hình để thực hiện các chức năng khác nhau, bao gồm cả nút đồng ý (endorsing node) và nút ghi (committing node). Peer là thành phần cơ bản của [mạng Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html), được sở hữu và duy trì bởi các thành viên. Đây là nơi lưu trữ các bản sao của ledger và các bản sao của smart contract. Lấy ví dụ sau, mạng N bao gồm các peer node là P1, P2 và P3. Mỗi Peer Nodes này đều chứa bản sảo của sổ cái phân tán (distributed ledger) L1. P1, P2 và P3 đều sử dụng chung chaincode S1 để truy cập vào bản sao sổ cái phân tán của nó. Các peer node có thể được tạo, dừng, cấu hình lại và xóa. Có một tập hợp các API cho phép các quản trị viên và ứng dụng tương tác với services mà họ cung cấp.

 - Ordering Service Nodes (Nút sắp xếp): Ordering service nodes là các node mạng đảm nhận vai trò quản lý các giao dịch trong [mạng Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html). Các nút này đảm bảo rằng các giao dịch được xử lý theo đúng thứ tự và được đồng bộ hóa giữa các peer nodes.

 - Chaincode: Chaincode là mã lệnh (smart contract) chạy trên các Peer Nodes để thực thi các giao dịch trong [mạng Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html). [Mạng Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) thực hiện smart contract với công nghệ có tên gọi là chaincode. Có thể hiểu đơn giản chaincode là một đoạn code được dùng để truy cập vào sổ cái. Chaincode được viết dưới dạng một ngôn ngữ lập trình như Go, Java, hoặc Node.js và được triển khai trên các Peer Nodes để thực thi các hợp đồng thông minh.

 - Channels (Kênh): Channels là các kênh mạng được tạo ra để giới hạn quyền truy cập vào các giao dịch trong [mạng Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html). Các kênh này được sử dụng để cô lập các giao dịch giữa các thành viên khác nhau trong [mạng Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html).

 - Identity Management: Quản lý danh tính trong [Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) là một phần quan trọng của mạng Fabric để đảm bảo tính bảo mật và truy cập của các thành viên trong mạng. Các thành viên phải được xác thực và cấp quyền truy cập trên mạng để tránh các cuộc tấn công và gian lận. Identity Management đảm bảo tính toàn vẹn và an ninh của dữ liệu danh tính trong mạng. Identity Management quản lý các thông tin liên quan đến danh tính của các thành viên, bao gồm các thông tin như tên, địa chỉ, chứng chỉ và vai trò của thành viên đó trong mạng.
 
 - Membership Service Provider: Membership Service Provider (MSP) là một thành phần của hệ thống có nhiệm vụ cung cấp các chứng chỉ (credential) cho Client và Peer Nodes để họ tham gia vào [mạng Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html). Membership Service Provider quản lý việc cấp và phân phối chứng chỉ cho các thành viên trong mạng. Với vai trò này, Membership Service Provider đảm bảo tính bảo mật của mạng bằng cách xác minh danh tính của từng thành viên và phân quyền truy cập đối với các hoạt động khác nhau trong mạng.
 
 - SDKs (Software Development Kits): [Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) cung cấp các SDKs để giúp các nhà phát triển xây dựng ứng dụng blockchain trên [nền tảng Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html). Các SDKs này hỗ trợ các ngôn ngữ lập trình khác nhau như Go, Java và Node.js.

Một số tính năng chính của Fabric ledger:
-	Truy vấn và cập nhật ledger sử dụng tra cứu qua khóa, truy vấn phạm vi và truy vấn khóa tổng hợp (composite key).
-	Transaction bao gồm phiên bản của keys/values được đọc trong chaincode (read set) và keys/values được write trong chaincode (write set).
-	Transaction bao gồm chữ ký của mọi endorsing peer và được gửi đến Ordering Service Nodes.
-	Các transaction được sắp xếp thành các khối và được "phân phối" từ Ordering Service Nodes đến các Peer Nodes trong một Channel.
-	Các peer xác thực giao dịch dựa trên các chính sách chứng thực (endorsement policies) và thực thi các chính sách này.

### Ứng dụng trong thực tế

[Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) là một nền tảng blockchain được thiết kế để xây dựng các ứng dụng doanh nghiệp. Nó cung cấp một môi trường phát triển và triển khai các ứng dụng blockchain an toàn, đáng tin cậy và có thể mở rộng. Dưới đây là một số ứng dụng chính của [Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html):

 - <i>Quản lý chuỗi cung ứng</i>: [Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) có thể được sử dụng để giám sát và quản lý các hoạt động của chuỗi cung ứng. Với Fabric, các công ty có thể theo dõi tình trạng của các sản phẩm, từ quá trình sản xuất đến phân phối.
 - <i>Quản lý tài sản</i>: [Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) cũng có thể được sử dụng để quản lý các tài sản, bao gồm cả tài sản vật chất và tài sản không vật chất. Với Fabric, các tổ chức có thể tạo ra các hợp đồng thông minh để theo dõi và quản lý tài sản của mình.
 - <i>Quản lý hồ sơ</i>: [Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) có thể được sử dụng để quản lý các hồ sơ của các tổ chức, bao gồm cả hồ sơ nhân viên và khách hàng. Với Fabric, các tổ chức có thể tạo ra các hồ sơ được mã hóa để đảm bảo tính riêng tư và an toàn.
 - <i>Quản lý tài chính</i>: [Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) cũng có thể được sử dụng để quản lý các giao dịch tài chính, bao gồm cả việc chuyển tiền và giao dịch chứng khoán. Với Fabric, các tổ chức có thể tạo ra các hợp đồng thông minh để tự động hóa các giao dịch và giảm thiểu các rủi ro.
 - <i>Quản lý bảo hiểm</i>: [Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) cũng có thể được sử dụng để quản lý các chính sách bảo hiểm và đền bù. Với Fabric, các tổ chức có thể tạo ra các hợp đồng thông minh để tự động hóa quy trình đền bù và giảm thiểu các rủi ro.

### Tài liệu tham khảo

* <a href="https://glpcoin.medium.com/hyperledger-fabric-4b2704f5f6d8" target="_blank">https://glpcoin.medium.com/hyperledger-fabric-4b2704f5f6d8</a>

