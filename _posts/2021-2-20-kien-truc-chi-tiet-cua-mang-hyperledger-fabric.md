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

[Mạng Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) bao gồm nhiều tổ chức tương tác lẫn nhau trong mạng. Ví dụ một tổ chức có thể là một ngân hàng trong một mạng lưới bao gồm các tổ chức tài chính hoặc một đối tác vận chuyển trong một mạng lưới chuỗi cung ứng. Mỗi tổ chức có cơ quan cấp chứng chỉ Fabric và một hoặc nhiều nút ngang hàng (peer node). Một mạng Fabric cũng có một ordering service được chia sẻ bởi tất cả tổ chức trong mạng và thành phần này giúp xử lý giao dịch cho mạng lưới. Chúng ta sẽ đi vào mô tả chi tiết từng khái niệm và thành phần.

Một tổ chức trong mạng được định nghĩa bởi chứng chỉ gốc (root certificate) dành cho riêng tổ chức đó. Các user và những thành phần khác cũng được định danh bằng các chứng chỉ và các chứng chỉ này đều có nguồn gốc từ chứng chỉ gốc. Điều này giúp đảm bảo các tổ chức khác trong mạng có thể liên hệ người dùng với tổ chức của họ. Các chứng chỉ này cũng chỉ định các quyền cho từng thực thể trên mạng, chẳng hạn như read-only so với full access trên một kênh.
Chứng chỉ gốc của một tổ chức được lưu trữ trên Fabric certificate authority (CA). Fabric CA cũng cấp chứng chỉ cho người dùng trong một tổ chức và xử lý các hoạt động liên quan khác. Fabric CA cấp doanh nghiệp sử dụng nhiều thành phần khác nhau và có thể được triển khai theo nhiều cách khác nhau bằng cách sử dụng Hardware Security Module (HSM) để bảo vệ chứng chỉ gốc.

Một tổ chức cũng tạo ra một hoặc nhiều peer node để thay mặt thực hiện các hoạt động cho tổ chức đó. Cụ thể, một peer node xác nhận các giao dịch được đề xuất trên mạng, lưu trữ và thực thi mã hợp đồng thông minh (được gọi là chaincode trong Fabric) và lưu trữ bản sao cục bộ của sổ cái để truy cập. Fabric clients thường tương tác với peer node để đọc sổ cái, thêm chaincode mới vào mạng hoặc đề xuất một giao dịch mới. Một peer node thường chạy trên chính máy tính của nó.

### [Mô hình Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html)

- <i>Assets</i>: Có thể hiểu asset trong [mạng Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) được định nghĩa là mọi thứ có giá trị bao gồm tài sản hữu hình và tài sản vô hình (hợp đồng và tài sản trí tuệ). Hyperledger Fabric cung cấp khả năng chỉnh sửa tài sản bằng cách sử dụng các chaincode transaction. Asset được biểu diễn trong Hyperledger Fabric dưới dạng tập hợp các cặp key-value. Các trạng thái thay đổi được ghi lại dưới dạng transaction trên một Channel ledger. Asset có thể được biểu diễn dưới dạng nhị phân hoặc JSON.
- <i>Chaincode</i>: Chaincode là phần mềm xác định asset và transaction instruction để sửa đổi asset. Nói cách khác, chain code mang bản chất business logic. Chaincode thực thi các quy tắc để chỉnh sửa key-value trong state database. Các hàm chaincode được thực thi dựa trên state database hiện tại của ledger và được khởi tạo thông qua đề xuất transaction.
- <i>Ledger Features</i>: Ledger được sắp xếp theo trình tự, có khả năng chống giả mạo các thay đổi trong [mạng Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html). Chuyển đổi trạng thái là kết quả của các lệnh gọi chaincode được gửi bởi những bên tham gia vào mạng. Kết quả của mỗi transaction là tập hợp các cặp khóa-giá trị được commit đến Ledger như tạo, cập nhật và xóa.

### Các thành phần của [mạng Hyperledger Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html)

- Ledger: Một ledger (sổ cái) bao gồm 2 phần khác nhau là "blockchain" và "state database".
- Membership Service Provider: Membership Service Provider (MSP) là một thành phần của hệ thống có nhiệm vụ cung cấp các chứng chỉ (credential) cho client và peer để họ tham gia vào [Hyperledger Fabric network](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html).
- Smart Contract: Smart Contract là một đoạn mã được gọi bởi ứng dụng của client bên ngoài mạng blockchain - quản lý quyền truy cập và sửa đổi đối với một tập hợp các cặp khóa-giá trị ở "state database".
- Peer: Peer là thành phần cơ bản của network, được sở hữu và duy trì bởi các thành viên. Đây là nơi lưu trữ các bản sao của ledger và các bản sao của smart contract. Trong ví dụ sau, mạng N bao gồm các peer node là P1, P2 và P3. Mỗi peer node này đều chứa bản sảo của sổ cái phân tán (distributed ledger) L1. P1, P2 và P3 đều sử dụng chung chaincode S1 để truy cập vào bản sao sổ cái phân tán của nó. Các peer node có thể được tạo, dừng, cấu hình lại và xóa. Có một tập hợp các API cho phép các quản trị viên và ứng dụng tương tác với services mà họ cung cấp.
- [Mạng Fabric](https://nguyentruonglong.net/kien-truc-chi-tiet-cua-mang-hyperledger-fabric.html) thực hiện smart contract với công nghệ có tên gọi là chaincode. Có thể hiểu đơn giản chaincode là một đoạn code được dùng để truy cập vào sổ cái. Chaincode được viết dưới dạng một ngôn ngữ lập trình.

Một số tính năng chính của Fabric ledger:
-	Truy vấn và cập nhật ledger sử dụng tra cứu qua khóa, truy vấn phạm vi và truy vấn khóa tổng hợp (composite key).
-	Transaction bao gồm phiên bản của keys/values được đọc trong chaincode (read set) và keys/values được write trong chaincode (write set).
-	Transaction bao gồm chữ ký của mọi endorsing peer và được gửi đến ordering service.
-	Các transaction được sắp xếp thành các khối và được "phân phối" từ ordering service đến các peer trong một channel.
-	Các peer xác thực giao dịch dựa trên các chính sách chứng thực (endorsement policies) và thực thi các chính sách này.


### Tài liệu tham khảo

* <a href="https://glpcoin.medium.com/hyperledger-fabric-4b2704f5f6d8" target="_blank">https://glpcoin.medium.com/hyperledger-fabric-4b2704f5f6d8</a>

