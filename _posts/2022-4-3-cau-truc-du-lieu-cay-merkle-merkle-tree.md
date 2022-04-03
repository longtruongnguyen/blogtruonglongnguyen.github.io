---
layout: post
title: Cấu trúc dữ liệu cây Merkle (Merkle tree)
description: Cây Merkle là một cấu trúc dữ liệu tổng quát của danh sách băm (hash list). Nó là một cấu trúc cây trong đó mỗi node lá có giá trị là kết quả hàm băm của một block dữ liệu và mỗi node không phải node lá có giá trị là kết quả một hàm băm các node con của nó.
excerpt: Cây Merkle là một cấu trúc dữ liệu tổng quát của danh sách băm (hash list). Nó là một cấu trúc cây trong đó mỗi node lá có giá trị là kết quả hàm băm của một block dữ liệu và mỗi node không phải node lá có giá trị là kết quả một hàm băm các node con của nó.
thumbnail: 
keywords: Cấu trúc dữ liệu cây Merkle, cây Merkle, Merkle tree
author: Nguyễn Trường Long
---


Cây Merkle là một cấu trúc dữ liệu tổng quát của danh sách băm (hash list). Nó là một cấu trúc cây trong đó mỗi node lá có giá trị là kết quả hàm băm của một block dữ liệu và mỗi node không phải node lá có giá trị là kết quả một hàm băm các node con của nó. Cây Merkle có hệ số phân nhánh là 2, nghĩa là mỗi node có tối đa 2 nút con.

Cây Merkle được sử dụng trong các hệ thống phân tán dùng xác minh dữ liệu. Cây Merkle tỏ ra hiệu quả vì nó sử dụng hàm băm thay vì các tệp dữ liệu đầy đủ. Hàm băm là cách mã hóa tệp thành các dữ liệu có kích thước nhỏ hơn nhiều so với tệp thực. Hiện tại thì cấu trúc dữ liệu cây Merkle được ứng dụng chính trong các mạng ngang hàng như Tor, Bitcoin,... 

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/HashTree.png" alt="Cấu trúc dữ liệu cây Merkle">
  <figcaption>
	  <i>Cấu trúc dữ liệu cây Merkle</i>
  </figcaption>
</center>
</figure>
