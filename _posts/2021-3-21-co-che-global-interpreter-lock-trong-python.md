---
layout: post
title: Cơ chế Global Interpreter Lock trong Python
description: Cơ chế GIL quy định rằng Python chỉ sử dụng một luồng duy nhất để thực thi các lệnh lập trình trong một chương trình. Điều này có nghĩa là trong Python tại một thời điểm chỉ có một luồng duy nhất được thực thi.
keywords: Cơ chế GIL, Cơ chế Global Interpreter Lock, GIL trong Python, Global Interpreter Lock, GIL, lập trình Python
excerpt: Trong ngôn ngữ lập trình Python tồn tại một cơ chế được gọi là Global Interpreter Lock (GIL). Cơ chế GIL không cho phép tăng hiệu suất của các chương trình đa luồng lên nhiều và thậm chí có thể làm giảm hiệu suất của một số chương trình đa luồng.
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

Trong ngôn ngữ lập trình Python tồn tại một cơ chế được gọi là [Global Interpreter Lock (GIL)](https://nguyentruonglong.net/co-che-global-interpreter-lock-trong-python.html). Cơ chế này khóa toàn bộ trình thông dịch, chỉ cho phép Python sử dụng một luồng duy nhất để thực thi các lệnh lập trình trong một chương trình. Điều này có nghĩa là trong Python tại một thời điểm chỉ có một luồng duy nhất được thực thi. Mỗi luồng muốn thực thi trước tiên phải đợi [GIL](https://nguyentruonglong.net/co-che-global-interpreter-lock-trong-python.html) được giải phóng bởi luồng đang thực thi. Có thể hình dung đơn giản rằng [GIL](https://nguyentruonglong.net/co-che-global-interpreter-lock-trong-python.html) là microphone duy nhất trong một hội nghị chẳng hạn, bất kỳ ai muốn phát biểu đều phải nhận được microphone từ người đang giữ microphone ở thời điểm hiện tại. Do [cơ chế GIL](https://nguyentruonglong.net/co-che-global-interpreter-lock-trong-python.html), hiệu suất của một chương trình đơn luồng và một chương trình đa luồng là tương đương nhau trong Python. Cơ chế này làm cho các chương trình đa luồng không tăng hiệu suất lên nhiều và thậm chí có thể làm giảm hiệu suất của một số chương trình đa luồng. Mình có viết thử một chương trình sau làm ví dụ minh họa cho vấn đề này:



Chúng ta có thể thấy trong 10 trường hợp sử dụng tối đa lần lượt từ 1 đến 10 thread khác nhau cùng thực thi tác vụ ban đầu, thời gian thực thi tác vụ vẫn là xấp xỉ nhau và không có bất kỳ trường hợp nào tăng hiệu suất lên đáng kể. Tác động của [GIL](https://nguyentruonglong.net/co-che-global-interpreter-lock-trong-python.html) không xảy ra trong chương trình đơn luồng, nhưng nó có thể gây ra hiện tượng bottleneck trong CPU-bound và trong các chương trình đa luồng.

### Cơ chế GIL đối với I/O-bound và CPU-bound

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/IOBound.png" alt="Ảnh minh họa cho vấn đề I/O-bound">
  <figcaption>
	  <i>Ảnh minh họa cho vấn đề I/O-bound</i>
  </figcaption>
</center>
</figure>

Trong ảnh minh họa trên, các ô màu xanh lam biểu diễn thời gian khi chương trình đang hoạt động và các ô màu đỏ biểu diễn thời gian chờ đợi tác vụ I/O hoàn tất. Tốc độ của chương trình bị giới hạn bởi phần lớp thời gian chờ đợi các tác vụ input/output được thực thi hoàn tất. Các tác vụ input/output này có thể là reading/writing dữ liệu từ ổ đĩa, reading/waiting dữ liệu từ bàn phím hoặc chuột máy tính, reading/waiting dữ liệu từ network,... . Có thể hiểu tổng quát các tác vụ input/output là tất cả những gì mà máy tính không thể tự thực hiện được và phải chờ đợi phản hồi từ những thành phần khác, ví dụ như trình duyệt trên máy tính chờ đợi dữ liệu phản hồi từ máy chủ.

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/CPUBound.png" alt="Ảnh minh họa cho vấn đề CPU-bound">
  <figcaption>
	  <i>Ảnh minh họa cho vấn đề CPU-bound</i>
  </figcaption>
</center>
</figure>

Mặt khác, có những chương trình thực hiện các tính toán mà không cần truy cập mạng hoặc truy cập những thành phần ngoại vi khác. Trong ảnh minh họa trên, chúng ta có thể thấy những tác vụ I/O không có bất kỳ ảnh hưởng đáng kể nào trong quá trình thực thi chương trình. Đây là những chương trình CPU-bound hay chương trình bị ràng buộc bởi CPU vì tài nguyên giới hạn tốc độ chương trình là CPU chứ không phải mạng hoặc những thành phần ngoại vi. Tóm lại thì CPU-bound là vấn đề tốc độ thực thi chương trình để hoàn thành một tác vụ chủ yếu được xác định và bị giới hạn bởi tốc độ của CPU. Việc tăng tốc những chương trình CPU-bound liên quan đến việc tìm kiếm phương thức để thực hiện nhiều phép tính toán hơn trong cùng một khoảng thời gian.

Có 3 hướng tiếp cận chính có thể sử dụng để giải quyết những vấn đề này mình đã tham khảo từ các nguồn khác nhau và được mô tả tóm gọn trong bảng bên dưới.

<style type="text/css">
    .tg {
        border-collapse: collapse;
        border-spacing: 0;
    }
    .tg td {
        border-color: black;
        border-style: solid;
        border-width: 1px;
        font-family: Arial, sans-serif;
        font-size: 16px;
        overflow: hidden;
        padding: 15px 10px;
        word-break: normal;
    }
    .tg th {
        border-color: black;
        border-style: solid;
        border-width: 1px;
        font-family: Arial, sans-serif;
        font-size: 16px;
        font-weight: normal;
        overflow: hidden;
        padding: 15px 10px;
        word-break: normal;
    }
    .tg .tg-fymr {
        border-color: inherit;
        font-weight: bold;
        text-align: left;
        vertical-align: top;
    }
    .tg .tg-0pky {
        border-color: inherit;
        text-align: left;
        vertical-align: top;
    }
</style>

<figure>
    <center>
        <table class="tg">
            <thead>
                <tr>
                    <th class="tg-fymr">Approach</th>
                    <th class="tg-fymr">Python package</th>
                    <th class="tg-fymr">Better</th>
                    <th class="tg-fymr">Parallel</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td class="tg-0pky">Threading</td>
                    <td class="tg-0pky">threading</td>
                    <td class="tg-0pky">I/O-bound</td>
                    <td class="tg-0pky">No</td>
                </tr>
                <tr>
                    <td class="tg-0pky">Multiprocessing</td>
                    <td class="tg-0pky">multiprocessing</td>
                    <td class="tg-0pky">CPU-bound</td>
                    <td class="tg-0pky">Yes</td>
                </tr>
                <tr>
                    <td class="tg-0pky">Asynchronous</td>
                    <td class="tg-0pky">asyncio</td>
                    <td class="tg-0pky">I/O-bound</td>
                    <td class="tg-0pky">No</td>
                </tr>
            </tbody>
        </table>
        <figcaption>
            <i></i>
        </figcaption>
    </center>
</figure>

### Tài liệu tham khảo

* <a href="https://www.geeksforgeeks.org/what-is-the-python-global-interpreter-lock-gil" target="_blank">https://www.geeksforgeeks.org/what-is-the-python-global-interpreter-lock-gil</a>
* <a href="https://www.javatpoint.com/python-memory-management" target="_blank">https://www.javatpoint.com/python-memory-management</a>
* <a href="https://www.guru99.com/python-multithreading-gil-example.html" target="_blank">https://www.guru99.com/python-multithreading-gil-example.html</a>
* <a href="https://realpython.com/python-memory-management" target="_blank">https://realpython.com/python-memory-management</a>
* <a href="https://www.freecodecamp.org/news/multithreaded-python" target="_blank">https://www.freecodecamp.org/news/multithreaded-python</a>
* <a href="https://docs.python.org/3/c-api/structures.html" target="_blank">https://docs.python.org/3/c-api/structures.html</a>
* <a href="https://realpython.com/python-concurrency" target="_blank">https://realpython.com/python-concurrency</a>
* <a href="https://granulate.io/introduction-to-the-infamous-python-gil" target="_blank">https://granulate.io/introduction-to-the-infamous-python-gil</a>
* <a href="https://www.programmersought.com/article/8984296557" target="_blank">https://www.programmersought.com/article/8984296557</a>
