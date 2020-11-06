---
layout: post
title: Đồng bộ hóa giữa các Thread trong Python
description: Đồng bộ hóa giữa các Thread trong Python
keywords: cơ chế đồng bộ trong Python, đồng bộ hóa trong Python, đồng bộ hóa thread, synchronization, đồng bộ trong Python, ngôn ngữ lập trình Python, đồng bộ các luồng trong Python
excerpt: Một trong những vấn đề lớn mà chúng ta thường hay gặp nhất trong việc thiết kế những hệ thống chạy đồng thời (concurrent systems) chính là deadlock. Bài toán buổi ăn tối của các triết gia (Dining Philosophers Problem) thường được xem là ví dụ minh họa tốt nhất cho khái niệm deadblock này. Chúng ta hãy cùng tìm hiểu bài toán này.
author: Nguyễn Trường Long
---

Một trong những vấn đề lớn mà chúng ta thường hay gặp nhất trong việc thiết kế những hệ thống chạy đồng thời (concurrent systems) chính là deadlock. Bài toán buổi ăn tối của các triết gia (Dining Philosophers Problem) thường được xem là ví dụ minh họa tốt nhất cho khái niệm deadblock này. Chúng ta hãy cùng tìm hiểu bài toán này.

### Giới thiệu về bài toán kinh điển "Bữa ăn tối của các triết gia"

Bài toán buổi ăn tối của các triết gia được đề xuất lần đầu tiên bởi E. W. Dijkstra. Mình tạm dịch tóm lược lại nội dung của <a href="https://en.wikipedia.org/wiki/Dining_philosophers_problem" target="_blank">bài toán này</a> từ Wikipedia như sau:<br/>

* Có 5 triết gia ngồi xung quanh một chiếc bàn tròn
* Mỗi triết gia có một bát mỳ Ý và một chiếc nĩa được đặt giữa mỗi cặp triết gia kề nhau
* Mỗi triết gia chỉ có hai trạng thái luân phiên nhau là suy nghĩ và ăn mỳ
* Tuy nhiên, một triết gia chỉ có thể ăn mỳ khi họ cả cả nĩa đặt bên trái và nĩa đặt bên phải của họ
* Mỗi một chiếc nĩa chỉ được sử dụng bởi một triết gia tại một thời điểm, do đó một triết gia chỉ sử dụng được nĩa khi nó hiện đang chưa được sử dụng bởi triết gia khác
* Sau khi một triết gia ăn mỳ xong cần đặt cả hai nĩa trở về vị trí gốc ban đầu để các triết gia còn lại có thể sử dụng
* Một triết gia không thể bắt đầu ăn khi họ chưa lấy được đầy đủ cả hai nĩa bên trái lẫn bên phải
* Giả sử việc ăn uống của mỗi triết gia này là không bị giới hạn
