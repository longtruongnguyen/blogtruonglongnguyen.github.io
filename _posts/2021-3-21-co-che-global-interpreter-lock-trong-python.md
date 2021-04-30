---
layout: post
title: Cơ chế Global Interpreter Lock trong Python
description: Cơ chế GIL quy định rằng Python chỉ sử dụng một luồng duy nhất để thực thi các lệnh lập trình trong một chương trình. Điều này có nghĩa là trong Python tại một thời điểm chỉ có một luồng duy nhất được thực thi.
keywords: Cơ chế GIL, Cơ chế Global Interpreter Lock, GIL trong Python, Global Interpreter Lock, GIL
excerpt: Trong ngôn ngữ lập trình Python tồn tại một cơ chế được gọi là Global Interpreter Lock (GIL). Cơ chế này không cho phép tăng hiệu suất của các chương trình đa luồng lên nhiều và thậm chí có thể làm giảm hiệu suất của một số chương trình đa luồng.
author: Nguyễn Trường Long
---

### Cơ chế quản lý bộ nhớ trong Python

Quản lý bộ nhớ là quy trình kiểm soát và phân phối tài nguyên bộ nhớ máy tính cho dữ liệu được sinh ra trong các chương trình đang chạy. Quản lý bộ nhớ trong một chương trình kết hợp hai nhiệm vụ liên quan, được gọi là cấp phát (allocation) và tái sử dụng (recycling).

Khi chương trình yêu cầu bộ nhớ, vì máy tính chỉ có bộ nhớ với dung lượng hữu hạn nên trình quản lý bộ nhớ phải tìm một số vùng trống trong bộ nhớ để có thể cung cấp cho chương trình. Quá trình cung cấp bộ nhớ này thường được gọi là cấp phát bộ nhớ. Ngược lại khi dữ liệu không còn cần thiết nữa thì nó có thể bị xóa đi hoặc giải phóng. Tác vụ này có thể được thực hiện thủ công bởi lập trình viên hoặc tự động bởi trình quản lý bộ nhớ.

Có một sự khác biệt đáng kể về mặt quản lý các đối tượng trong không gian bộ nhớ giữa ngôn ngữ lập trình Python và các ngôn ngữ lập trình khác. Tất cả các object trong Python đều được extension từ <i>PyObject</i> chứa hai thông tin cơ bản:

* <i>Py_REFCNT</i>: chứa số lượng tham chiếu của đối tượng
* <i>Py_TYPE</i>: chứa con trỏ đến đối tượng loại tương ứng

Python cung cấp các module hỗ trợ cho cả xử lý đa luồng và xử lý đa tiến trình. Vấn đề là biến số tham chiếu cần được bảo vệ để tránh bị lỗi bởi các vấn đề race condition khi có hai hoặc nhiều luồng được thực thi đồng thời. Nếu biến số tham chiều này lỗi sẽ gây ra rò rỉ bộ nhớ hoặc bộ nhớ được giải phóng không chính xác. Một giải pháp cho vấn đề này là sử dụng một khóa chung duy nhất cho một luồng tương tác với tài nguyên được chia sẻ.

### Giới thiệu về cơ chế Global Interpreter Lock

Trong ngôn ngữ lập trình Python tồn tại một cơ chế được gọi là [Global Interpreter Lock (GIL)](https://nguyentruonglong.net/co-che-global-interpreter-lock-trong-python.html). Cơ chế này khóa toàn bộ trình thông dịch, chỉ cho phép Python sử dụng một luồng duy nhất để thực thi các lệnh lập trình trong một chương trình. Điều này có nghĩa là trong Python tại một thời điểm chỉ có một luồng duy nhất được thực thi. Mỗi luồng muốn thực thi trước tiên phải đợi [GIL](https://nguyentruonglong.net/co-che-global-interpreter-lock-trong-python.html) được giải phóng bởi luồng đang thực thi. Có thể hình dung đơn giản rằng [GIL](https://nguyentruonglong.net/co-che-global-interpreter-lock-trong-python.html) là microphone duy nhất trong một hội nghị chẳng hạn, bất kỳ ai muốn phát biểu đều phải nhận được microphone từ người đang giữ microphone ở thời điểm hiện tại. Do [cơ chế GIL](https://nguyentruonglong.net/co-che-global-interpreter-lock-trong-python.html), hiệu suất của một chương trình đơn luồng và một chương trình đa luồng là tương đương nhau trong Python. Cơ chế này làm cho các chương trình đa luồng không tăng hiệu suất lên nhiều và thậm chí có thể làm giảm hiệu suất của một số chương trình đa luồng. Tác động của [GIL](https://nguyentruonglong.net/co-che-global-interpreter-lock-trong-python.html) không xảy ra trong chương trình đơn luồng, nhưng nó có thể gây ra hiện tượng bottleneck trong CPU-bound và trong các chương trình đa luồng.

### Cơ chế GIL đối với I/O-bound và CPU-bound


### Tài liệu tham khảo

* <a href="https://www.geeksforgeeks.org/what-is-the-python-global-interpreter-lock-gil" target="_blank">https://www.geeksforgeeks.org/what-is-the-python-global-interpreter-lock-gil</a>
* <a href="https://www.javatpoint.com/python-memory-management" target="_blank">https://www.javatpoint.com/python-memory-management</a>
* <a href="https://www.guru99.com/python-multithreading-gil-example.html" target="_blank">https://www.guru99.com/python-multithreading-gil-example.html</a>
* <a href="https://realpython.com/python-memory-management" target="_blank">https://realpython.com/python-memory-management</a>
* <a href="https://www.freecodecamp.org/news/multithreaded-python" target="_blank">https://www.freecodecamp.org/news/multithreaded-python</a>
* <a href="https://docs.python.org/3/c-api/structures.html" target="_blank">https://docs.python.org/3/c-api/structures.html</a>
