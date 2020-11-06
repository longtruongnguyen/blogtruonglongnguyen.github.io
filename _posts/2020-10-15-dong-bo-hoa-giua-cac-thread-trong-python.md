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

* Có 5 nhà triết học ngồi xung quanh một chiếc bàn tròn
* Mỗi nhà triết học có một bát mỳ Ý và một chiếc nĩa được đặt giữa mỗi cặp nhà triết học kề nhau
* Mỗi nhà triết học chỉ có hai trạng thái luân phiên nhau là suy nghĩ và ăn mỳ
* Tuy nhiên, một nhà triết học chỉ có thể ăn mỳ khi họ cả cả nĩa đặt bên trái và nĩa đặt bên phải của họ
* Mỗi một chiếc nĩa chỉ được sử dụng bởi một nhà triết học tại một thời điểm, do đó một nhà triết học chỉ sử dụng được nĩa khi nó hiện đang chưa được sử dụng bởi nhà triết học khác
* Sau khi một nhà triết học ăn mỳ xong cần đặt cả hai nĩa trở về vị trí gốc ban đầu để các nhà triết học còn lại có thể sử dụng
* Một nhà triết học không thể bắt đầu ăn mỳ khi họ chưa lấy được đầy đủ cả hai nĩa bên trái lẫn bên phải
* Giả sử việc ăn uống của mỗi nhà triết học này là không bị giới hạn và không một nhà triết học nào có thể biết liệu khi nào những người còn lại có thể muốn ăn mỳ hoặc suy nghĩ
* Hãy thiết kế một thuật toán sao cho mỗi nhà triết học có thể tiếp tục mãi mãi giữa hai trạng thái suy nghĩ và ăn mỳ mà không bị nhịn đói


<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/DiningPhilosophersProblem.png" alt="Ảnh minh họa cho bài toán buổi ăn tối của các triết gia">
  <figcaption>
	  <i>Ảnh minh họa cho bài toán buổi ăn tối của các triết gia. Nguồn: O'Reilly</i>
  </figcaption>
</center>
</figure>

Trong bài toán này, mỗi cái nĩa đại diện cho tài nguyên của hệ thống và mỗi nhà triết học đại diện cho một tiến trình. Những vấn đề mà các nhà triết học này có thể gặp phải tương tự như những vấn đề trong lập trình máy tính khi nhiều tiến trình cần quyền truy cập độc quyền vào các tài nguyên dùng chung.

### Vấn đề Deadlock

Chúng ta có thể thấy một tình huống có thể phát sinh với bài toán đặt ra là tất cả 5 nhà triết học đều chọn nĩa bên trái và ngồi suy nghĩ cho đến khi lấy được nĩa bên phải để có thể ăn mỳ. Điều này dẫn đến trạng thái bế tắc, hay còn được gọi là deadlock, là trạng thái mà mỗi nhà triết học đã chọn cái nĩa ở bên trái đang đợi cái nĩa ở bên phải dẫn đến không có sự kiện nào tiếp theo có thể xảy ra. Có thể khái quát một cách tổng quát rằng deadlock xảy ra khi mỗi tiến trình (process) nắm giữ một tài nguyên và đợi được cấp tài nguyên từ bất kỳ tiến trình nào khác.

### Vấn đề Livelock

### Vấn đề Starvation

Giả sử chúng ta bổ sung thêm một quy tắc vào tập hợp các quy tắc trong bài toán trên là các nhà triết học nếu đang nắm giữ một nĩa sẽ phải đặt nĩa này xuống sau mười phút chờ đợi nếu vẫn chưa nắm giữ được nĩa còn lại, sau đó đợi thêm mười phút nữa để bắt đầu lại quá trình lấy nĩa. Nếu tất cả năm triết gia xuất hiện trong phòng ăn cùng một lúc và mỗi người này cầm chiếc nĩa bên trái cùng một lúc, các nhà triết học sẽ đợi mười phút cho đến khi tất cả đặt nĩa xuống và sau đó đợi thêm mười phút nữa trước khi tất cả cùng bắt đầu lại quá trình cầm nĩa lên.

Khái quát hóa một cách tổng quát thì tình trạng đói tài nguyên (resource starvation) có thể xảy ra do sự thiếu hụt tài nguyên máy tính hoặc do nhiều tiến trình đang cạnh tranh nắm giữ cho cùng một tài nguyên máy tính. Trong thực tế, tình trạng đói tài nguyên có thể xảy ra do lỗi trong việc thiết kế các thuật toán lập lịch hoặc thuật toán loại trừ tương hỗ, nhưng cũng có thể do rò rỉ tài nguyên và cũng có thể xảy ra qua hình thức tấn công có tên gọi là "fork bomb".


### Tài liệu tham khảo
* <a href="http://www.cse.hcmut.edu.vn/~sonsys/OS_CQA01/Lecture07.pdf" target="_blank">http://www.cse.hcmut.edu.vn/~sonsys/OS_CQA01/Lecture07.pdf</a>
* <a href="https://www.geeksforgeeks.org/difference-between-deadlock-and-starvation-in-os/" target="_blank">https://www.geeksforgeeks.org/difference-between-deadlock-and-starvation-in-os/</a>
* <a href="https://en.wikipedia.org/wiki/Dining_philosophers_problem" target="_blank">https://en.wikipedia.org/wiki/Dining_philosophers_problem</a>
* <a href="https://en.wikipedia.org/wiki/Starvation_(computer_science)" target="_blank">https://en.wikipedia.org/wiki/Starvation_(computer_science)</a>
* <a href="https://csrc.nist.gov/glossary/term/Resource_Starvation" target="_blank">https://csrc.nist.gov/glossary/term/Resource_Starvation</a>
* <a href="https://www.geeksforgeeks.org/deadlock-starvation-and-livelock/" target="_blank">https://www.geeksforgeeks.org/deadlock-starvation-and-livelock/</a>



