---
layout: post
title: Cơ chế Global Interpreter Lock trong Python
description: Cơ chế GIL quy định rằng Python chỉ sử dụng một luồng duy nhất để thực thi các lệnh lập trình trong một chương trình. Điều này có nghĩa là trong Python tại một thời điểm chỉ có một luồng duy nhất được thực thi.
keywords: Cơ chế GIL, Cơ chế Global Interpreter Lock, GIL trong Python, Global Interpreter Lock, GIL
excerpt: Trong ngôn ngữ lập trình Python tồn tại một cơ chế được gọi là Global Interpreter Lock (GIL). Cơ chế này không cho phép tăng hiệu suất của các chương trình đa luồng lên nhiều và thậm chí có thể làm giảm hiệu suất của một số chương trình đa luồng.
author: Nguyễn Trường Long
---

### Giới thiệu về cơ chế Global Interpreter Lock

Python chung cấp các module hỗ trợ cho cả xử lý đa luồng và xử lý đa tiến trình.

Trong ngôn ngữ lập trình Python tồn tại một cơ chế được gọi là Global Interpreter Lock (GIL). Cơ chế này không cho phép tăng hiệu suất của các chương trình đa luồng lên nhiều và thậm chí có thể làm giảm hiệu suất của một số chương trình đa luồng.

Cơ chế GIL quy định rằng Python chỉ sử dụng một luồng duy nhất để thực thi các lệnh lập trình trong một chương trình. Điều này có nghĩa là trong Python tại một thời điểm chỉ có một luồng duy nhất được thực thi. Hiệu suất của một chương trình đơn luồng và chương trình đa luồng là tương đương nhau trong Python.

### Cơ chế quản lý bộ nhớ trong Python

Quản lý bộ nhớ là quy trình kiểm soát và phân phối tài nguyên bộ nhớ máy tính cho dữ liệu được sinh ra trong các chương trình đang chạy. Quản lý bộ nhớ trong một chương trình kết hợp hai nhiệm vụ liên quan, được gọi là cấp phát (allocation) và tái sử dụng (recycling).

Khi chương trình yêu cầu bộ nhớ, vì máy tính chỉ có bộ nhớ với dung lượng hữu hạn nên trình quản lý bộ nhớ phải tìm một số vùng trống trong bộ nhớ để có thể cung cấp cho chương trình. Quá trình cung cấp bộ nhớ này thường được gọi là cấp phát bộ nhớ. Ngược lại khi dữ liệu không còn cần thiết nữa thì nó có thể bị xóa đi hoặc giải phóng. Tác vụ này có thể được thực hiện thủ công bởi lập trình viên hoặc tự động bởi trình quản lý bộ nhớ.

Có một sự khác biệt đáng kể về mặt quản lý các đối tượng trong không gian bộ nhớ giữa ngôn ngữ lập trình Python và các ngôn ngữ lập trình khác. 

### Cơ chế GIL đối với I/O-bound và CPU-bound

### Tài liệu tham khảo

* <a href="https://www.geeksforgeeks.org/what-is-the-python-global-interpreter-lock-gil" target="_blank">https://www.geeksforgeeks.org/what-is-the-python-global-interpreter-lock-gil</a>
* <a href="https://www.javatpoint.com/python-memory-management" target="_blank">https://www.javatpoint.com/python-memory-management</a>
* <a href="https://www.guru99.com/python-multithreading-gil-example.html" target="_blank">https://www.guru99.com/python-multithreading-gil-example.html</a>
* <a href="https://realpython.com/python-memory-management" target="_blank">https://realpython.com/python-memory-management</a>
