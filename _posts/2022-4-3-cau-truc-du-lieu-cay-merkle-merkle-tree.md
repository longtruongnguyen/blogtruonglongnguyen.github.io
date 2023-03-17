---
layout: post
title: Cấu trúc dữ liệu cây Merkle (Merkle tree)
description: Cây Merkle là một cấu trúc dữ liệu tổng quát của danh sách băm (hash list). Nó là một cấu trúc cây trong đó mỗi node lá có giá trị là kết quả hàm băm của một block dữ liệu và mỗi node không phải node lá có giá trị là kết quả một hàm băm các node con của nó.
excerpt: Cây Merkle là một cấu trúc dữ liệu tổng quát của danh sách băm (hash list). Nó là một cấu trúc cây trong đó mỗi node lá có giá trị là kết quả hàm băm của một block dữ liệu và mỗi node không phải node lá có giá trị là kết quả một hàm băm các node con của nó.
thumbnail: https://nguyentruonglong.net/images/HashTree.png
keywords: Cấu trúc dữ liệu cây Merkle, cây Merkle, Merkle tree
author: Nguyễn Trường Long
---


[Cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) là một cấu trúc dữ liệu tổng quát của danh sách băm (hash list). Nó là một cấu trúc cây trong đó mỗi node lá có giá trị là kết quả hàm băm của một block dữ liệu và mỗi node không phải node lá có giá trị là kết quả một hàm băm các node con của nó. [Cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) có hệ số phân nhánh là 2 với mỗi node sẽ có tối đa là 2 node con.

[Cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) được sử dụng trong các hệ thống phân tán dùng xác minh dữ liệu. [Cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) tỏ ra hiệu quả vì nó sử dụng hàm băm thay vì các tệp dữ liệu đầy đủ. Hàm băm là cách mã hóa tệp dữ liệu thành các dữ liệu có kích thước nhỏ hơn nhiều so với dữ liệu thực. Hiện tại thì [cấu trúc dữ liệu cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) được ứng dụng chính trong các mạng ngang hàng như [BitTorrent](https://www.bittorrent.com), [Bitcoin](https://bitcoin.org/bitcoin.pdf) và [Git](https://git-scm.com),... 

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/HashTree.png" alt="Cấu trúc dữ liệu cây Merkle">
  <figcaption>
	  <i>Cấu trúc dữ liệu cây Merkle</i>
  </figcaption>
</center>
</figure>

[Cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) thường được triển khai dưới dạng cây nhị phân (binary tree) như ví dụ minh họa trong hình bên trên. Tuy nhiên, cây Merkle cũng có thể tồn tại ở dạng cấu trúc N-ary tree, với mỗi node không phải node lá sẽ có n node con.

Trong hình ảnh bên trên, chúng ta thấy có một dữ liệu đầu vào được chia thành các khối (block) có nhãn từ L1 đến L4. Mỗi khối này được băm bằng cách sử dụng một số hàm băm. Sau đó, các kết quả băm dữ liệu từ đến L1 đến L4 được gom thành các cặp và tiếp tục đệ quy quá trình băm cho đến khi tạo thành node gốc. Giá trị của node gốc là kết quả của hàm băm cho tất cả các node con bên dưới của nó.

Trong các hệ thống phân tán (distributed system) và hệ thống ngang hàng (peer-to-peer system), việc xác minh dữ liệu là rất quan trọng. Điều này là do cùng một dữ liệu được chia sẻ ra và lưu trữ ở nhiều nơi khác nhau. Vì vậy nếu một phần dữ liệu được thay đổi ở một vị trí thì điều quan trọng là dữ liệu phải được thay đổi đồng nhất ở mọi nơi lưu trữ khác. Cơ chế xác minh dữ liệu được sử dụng để đảm bảo dữ liệu giống nhau ở tất cả mọi nơi.

Tuy nhiên việc kiểm tra toàn bộ từng tệp dữ liệu bất kỳ khi nào hệ thống muốn xác minh dữ liệu sẽ tốn rất nhiều thời gian và chi phí tính toán. Vì vậy [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) được sử dụng trong các trường hợp này. Nó giúp giới hạn lượng dữ liệu được gửi qua mạng trong quá trình xác minh càng nhiều càng tốt. Thay vì gửi toàn bộ tệp dữ liệu qua mạng, nó chỉ gửi giá trị kết quả băm của tệp dữ liệu để kiểm tra xem dữ liệu có khớp hay không.

### Ứng dụng của cây Merkle trong Bitcoin

Trong [Bitcoin](https://bitcoin.org/bitcoin.pdf) và các loại tiền điện tử khác, [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) được sử dụng để mã hóa dữ liệu trong [blockchain](https://nguyentruonglong.net/blockchain-la-gi-giai-thich-chi-tiet-ve-blockchain.html) một cách hiệu quả và an toàn hơn. Nó là một cấu trúc dữ liệu toán học được tạo thành từ các giá trị hàm băm của các khối (block) dữ liệu giao dịch khác nhau. [Cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) tổng hợp tất cả các giao dịch trong một khối và tạo ra một dấu vân tay kỹ thuật số của toàn bộ tập hợp các hoạt động, cho phép người dùng xác minh xem nó có bao gồm một giao dịch (transaction) trong khối hay không. Nó cho phép xác minh tính nhất quán nhanh chóng và an toàn trên các bộ dữ liệu lớn. [Cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) được triển khai bằng cách băm các cặp node lặp đi lặp lại cho đến khi chỉ còn lại một kết quả băm cuối cùng, giá trị băm này được gọi là Merkle Root hoặc Root Hash.

### Ứng dụng của cây Merkle trong Git

Đối với [Git](https://git-scm.com), commit ID của mỗi commit là giá trị băm của commit object đó. Giá trị băm này được tính toán từ tất cả dữ liệu liên quan tạo nên commit đó bao gồm:

* Những thay đổi tệp trong commit
* Tên của các tệp trong commit
* Tên của người đã commit
* Thời gian tạo commit
* Message mô tả commit
* Parent commit ID

[Git](https://git-scm.com) sử dụng [object database](https://en.wikipedia.org/wiki/Object_database) để tổ chức và quản lý repository system. Mỗi blob, tree và commit đều có một giá trị băm. Chính vì vậy có thể xem [Git](https://git-scm.com) là một content-addressable filesystem. Nếu chúng ta muốn tham chiếu đến một đối tượng cụ thể, chúng ta chỉ cần biết giá trị băm này. [Git](https://git-scm.com) sử dụng các cơ chế này để đảm bảo các định danh luôn là duy nhất và không xảy ra xung đột. Cách tổ chức trong [object database](https://en.wikipedia.org/wiki/Object_database) của [Git](https://git-scm.com) có cấu trúc tương tự của một [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html). Nói chính xác hơn là cấu trúc của một nhóm các [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) trỏ đến các [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) khác. Cấu trúc này có thể được vận hành mà không cần tốn nhiều chi phí tài nguyên và rất khó sửa đổi nội dung. Các commit nếu muốn chỉnh sửa giả mạo đòi hỏi phải thực hiện rất nhiều tính toán cập nhật. Các cập nhật mới này khi so sánh với những bản sao khác sẽ không trùng khớp và không được chấp nhận.

### Ứng dụng của cây Merkle trong BitTorrent

[BitTorrent](https://www.bittorrent.com) là một giao thức truyền thông (communication protocol) được sử dụng để chia sẻ tệp dữ liệu qua mạng ngang hàng (peer-to-peer network). [Cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) được sử dụng trong [BitTorrent](https://www.bittorrent.com) như một cấu trúc dữ liệu phân cấp để kiểm tra tính toàn vẹn của các phần của tập tin được chia sẻ. Các phần của tập tin được chia thành các khối dữ liệu nhỏ hơn và mỗi khối được băm (hash) bằng một thuật toán băm dữ liệu (hash function) ví dụ như SHA-1 chẳng hạn để tạo ra một mã băm đại diện cho khối dữ liệu. Các mã băm này được tổ chức theo dạng [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html).

Khi một máy tính muốn tải xuống một tập tin từ [BitTorrent](https://www.bittorrent.com), nó sẽ yêu cầu các khối dữ liệu từ các máy tính khác trong mạng. Các khối dữ liệu này được tải xuống theo thứ tự và kiểm tra tính toàn vẹn của nó bằng cách so sánh mã băm của nó với các mã băm trên [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html). Nếu mã băm của khối dữ liệu được tải xuống khớp với mã băm trên [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html), khối dữ liệu đó được xem là hợp lệ và ghi dữ liệu lưu trữ. Nếu mã băm không khớp, khối dữ liệu đó sẽ bị loại bỏ và được tải xuống lại từ một máy tính khác trong mạng.

[Cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) cho phép kiểm tra tính toàn vẹn của tập tin một cách hiệu quả và nhanh chóng. Nếu một khối dữ liệu bị lỗi hoặc không chính xác, [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) sẽ cho phép máy tính tải xuống lại khối dữ liệu đó từ một máy tính khác trong mạng. Các khối dữ liệu được tải xuống một cách độc lập và có thể được kiểm tra tính toàn vẹn một cách hiệu quả mà không cần phải tải xuống toàn bộ tập tin. Điều này giúp cải thiện hiệu suất của giao thức [BitTorrent](https://www.bittorrent.com), giúp người dùng có thể tải xuống tập tin nhanh hơn và đáng tin cậy hơn.

### Ứng dụng của cây Merkle trong mạng Tor

Trong [mạng Tor](https://www.torproject.org), các tin nhắn được mã hóa và gửi qua nhiều node trung gian, mỗi node sẽ giải mã và truyền tiếp tin nhắn đến nút tiếp theo cho đến khi đến node đích. [Cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) dùng để xác thực tính toàn vẹn của thông điệp truyền tải giữa các node trong mạng. Cụ thể là khi thông điệp được gửi từ node nguồn đến node đích, [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) được sử dụng để đảm bảo rằng thông điệp không bị sửa đổi trong quá trình truyền tải. Khi một node truyền tải một thông điệp đến một node khác, nó sẽ kèm theo một đoạn dữ liệu chứa mã băm của toàn bộ thông điệp đó dựa trên một thuật toán băm chẳng hạn như SHA-1.

Sau đó, các mã băm được sử dụng để xây dựng [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html), trong đó mỗi node lá là một mã băm của một khối thông điệp, và các node trung gian được tạo ra bằng cách băm hai mã băm kế đó ở cấp trên để tạo ra một mã băm mới. Cuối cùng, node gốc của [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) sẽ là một mã băm duy nhất của toàn bộ thông điệp.

Khi thông điệp đến đích, nó sẽ được sử dụng để tạo ra một [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) mới, sử dụng các mã băm của thông điệp được nhận để tạo ra các node lá, và sau đó so sánh mã băm cuối cùng của [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) này với mã băm cuối cùng của [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) gốc được gửi từ node nguồn. Nếu hai mã băm này khớp nhau, thông điệp được coi là hợp lệ và chấp nhận, ngược lại nếu không khớp thì thông điệp đó sẽ bị loại bỏ.

[Cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) giúp đảm bảo tính toàn vẹn của thông điệp truyền tải giữa các node trong [mạng Tor](https://www.torproject.org). Nó cũng giúp ngăn chặn các cuộc tấn công giả mạo thông điệp bằng cách đảm bảo rằng bất kỳ thông điệp nào truyền tải giữa các node đều được xác thực và không bị sửa đổi trong quá trình truyền tải. Có thể xem [cây Merkle](https://nguyentruonglong.net/cau-truc-du-lieu-cay-merkle-merkle-tree.html) là một công cụ quan trọng trong [mạng Tor](https://www.torproject.org) để đảm bảo rằng các node trong mạng có thể trao đổi thông tin một cách an toàn và đáng tin cậy.

### Tài liệu tham khảo

* <a href="https://www.investopedia.com/terms/m/merkle-tree.asp" target="_blank">https://www.investopedia.com/terms/m/merkle-tree.asp</a>
* <a href="https://www.gemini.com/cryptopedia/merkle-tree-blockchain-merkle-root" target="_blank">https://www.gemini.com/cryptopedia/merkle-tree-blockchain-merkle-root</a>
* <a href="https://initialcommit.com/blog/Learn-Git-Object-Database" target="_blank">https://initialcommit.com/blog/Learn-Git-Object-Database</a>


