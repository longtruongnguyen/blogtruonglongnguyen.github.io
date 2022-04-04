---
layout: post
title: Cấu trúc dữ liệu cây Merkle (Merkle tree)
description: Cây Merkle là một cấu trúc dữ liệu tổng quát của danh sách băm (hash list). Nó là một cấu trúc cây trong đó mỗi node lá có giá trị là kết quả hàm băm của một block dữ liệu và mỗi node không phải node lá có giá trị là kết quả một hàm băm các node con của nó.
excerpt: Cây Merkle là một cấu trúc dữ liệu tổng quát của danh sách băm (hash list). Nó là một cấu trúc cây trong đó mỗi node lá có giá trị là kết quả hàm băm của một block dữ liệu và mỗi node không phải node lá có giá trị là kết quả một hàm băm các node con của nó.
thumbnail: https://nguyentruonglong.net/images/HashTree.png
keywords: Cấu trúc dữ liệu cây Merkle, cây Merkle, Merkle tree
author: Nguyễn Trường Long
---


Cây Merkle là một cấu trúc dữ liệu tổng quát của danh sách băm (hash list). Nó là một cấu trúc cây trong đó mỗi node lá có giá trị là kết quả hàm băm của một block dữ liệu và mỗi node không phải node lá có giá trị là kết quả một hàm băm các node con của nó. Cây Merkle có hệ số phân nhánh là 2, nghĩa là mỗi node có tối đa 2 nút con.

Cây Merkle được sử dụng trong các hệ thống phân tán dùng xác minh dữ liệu. Cây Merkle tỏ ra hiệu quả vì nó sử dụng hàm băm thay vì các tệp dữ liệu đầy đủ. Hàm băm là cách mã hóa tệp thành các dữ liệu có kích thước nhỏ hơn nhiều so với tệp thực. Hiện tại thì cấu trúc dữ liệu cây Merkle được ứng dụng chính trong các mạng ngang hàng như Tor, Bitcoin và Git,... 

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/HashTree.png" alt="Cấu trúc dữ liệu cây Merkle">
  <figcaption>
	  <i>Cấu trúc dữ liệu cây Merkle</i>
  </figcaption>
</center>
</figure>

Cây Merkle thường được triển khai dưới dạng cây nhị phân (binary tree) như ví dụ minh họa trong hình bên trên. Tuy nhiên, cây Merkle cũng có thể tồn tại ở dạng cấu trúc N-ary tree, với mỗi node không phải node lá sẽ có n node con.

Trong hình ảnh bên trên, chúng ta thấy có một dữ liệu đầu vào được chia thành các khối (block) có nhãn từ L1 đến L4. Mỗi khối này được băm bằng cách sử dụng một số hàm băm. Sau đó, các kết quả băm dữ liệu từ đến L1 đến L4 được gom thành các cặp và tiếp tục đệ quy quá trình băm cho đến khi tạo thành node gốc. Giá trị của node gốc là kết quả của hàm băm cho tất cả các node con bên dưới của nó.
