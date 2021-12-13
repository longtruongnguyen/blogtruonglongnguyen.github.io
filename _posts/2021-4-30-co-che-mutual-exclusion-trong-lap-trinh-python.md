---
layout: post
title: Cơ chế Mutual Exclusion trong lập trình Python
description: Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm.
keywords: Cơ chế Mutual Exclusion, Mutual Exclusion, mutex, loại trừ tương hỗ, khóa loại trừ lẫn nhau, lập trình Python, Python, lập trình đồng thời, lập trình đa luồng, lập trình multithreading, multiprocessing python, critical section
excerpt: Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm.
author: Nguyễn Trường Long
---

### Giới thiệu về mutual exclusion

[Mutual exclusion (khóa loại trừ lẫn nhau)](https://nguyentruonglong.net/co-che-mutual-exclusion-trong-lap-trinh-python.html) là một cơ chế thường được sử dụng để đồng bộ hóa các tiến trình hoặc luồng cần truy cập vào một số tài nguyên được chia sẻ trong các chương trình. Cơ chế này ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ để tránh xảy ra các vấn đề <strong><i>race condition</i></strong>. Nó quy định rằng nếu một tiến trình hoặc luồng khóa một tài nguyên, thì một tiến trình hoặc luồng khác muốn truy cập vào nó sẽ cần phải đợi cho đến khi tiến trình đầu tiên mở khóa. Khi tiến trình hoặc luồng thứ hai này nắm giữ tài nguyên được chia sẻ, nó cũng sẽ tiến hành khóa tài nguyên này lại cho đến khi nó xử lý hoàn tất và quy trình này cứ lặp lại tiếp tục.

Khái niệm này được sử dụng trong lập trình cùng với <strong><i>critical section</i></strong>, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm. Khi một tiến trình hoặc luồng nắm giữ một tài nguyên, nó phải khóa quyền truy cập vào tài nguyên được chia sẻ từ các tiến trình hoặc luồng khác để ngăn chặn các truy cập đồng thời vào cùng một tài nguyên. Đến khi giải phóng tài nguyên được chia sẻ, tiến trình hoặc luồng sẽ rời khỏi <strong><i>critical section</i></strong> và cho phép các tiến trình hoặc luồng khác tiến vào <strong><i>critical section</i></strong>.

### Vấn đề critical section

Mình có tham khảo ý tưởng từ một đoạn code mẫu <a href="https://cppsecrets.com/users/120612197115104981111171149751485164103109971051084699111109/Python-Implementation-of-Mutual-Exclusion-with-semaphore.php" target="_blank">tại đây</a> và thêm thắt chỉnh sửa một chút để chúng ta dễ hình dung hơn cho từng trường hợp cụ thể. Với trường hợp nhiều luồng truy cập vào cùng tài nguyên được chia sẻ trong <strong><i>multithreading</i></strong>, hãy cùng nhau xét ví dụ sau:

{% highlight python %}
from threading import Thread

class CricticalSection():

    def thread_1(self):
        for _ in range(1000000):
            self.criticalsection()  # Thực thi trong crictical section (thread 1)

    def thread_2(self):
        for _ in range(1000000):
            self.criticalsection()  # Thực thi trong crictical section (thread 2)

    def criticalsection(self):
        global x
        x += 1

    def main(self, step):
        global x
        x = 0
        t1 = Thread(target=self.thread_1)  # Gọi đến thread 1
        t1.start()
        t2 = Thread(target=self.thread_2)  # Gọi đến thread 2
        t2.start()

        t1.join()
        t2.join()

        print(f'Step {step + 1}: x = {x}')

if __name__ == '__main__':
    c = CricticalSection()
    for i in range(10):
        c.main(step=i)
{% endhighlight %}

Output của chương trình trên tại lần đầu tiên chạy chương trình mình thu được như sau:

{% highlight text %}
Step 1: x = 1609593
Step 2: x = 1675511
Step 3: x = 1714802
Step 4: x = 1761148
Step 5: x = 1890098
Step 6: x = 1817904
Step 7: x = 1628041
Step 8: x = 1669174
Step 9: x = 1806681
Step 10: x = 1849179
{% endhighlight %}

Thử chạy lại chương trình trên một lần nữa và quan sát. Kết quả mình thu được lại hoàn toàn khác so với lần chạy đầu tiên:

{% highlight text %}
Step 1: x = 1682482
Step 2: x = 1531211
Step 3: x = 1481805
Step 4: x = 1733795
Step 5: x = 1348640
Step 6: x = 1570863
Step 7: x = 1509799
Step 8: x = 1702471
Step 9: x = 1676963
Step 10: x = 1762260
{% endhighlight %}

Với trường hợp nhiều tiến trình truy cập vào cùng tài nguyên được chia sẻ trong <strong><i>multiprocessing</i></strong>, hãy đến với ví dụ sau với một chút biến thể nhỏ so với ví dụ đầu tiên:

{% highlight python %}
from multiprocessing import Process

class CricticalSection():

    def process_1(self, x):
        for _ in range(10000):
            self.criticalsection(x) # Thực thi trong crictical section (process 1)

    def process_2(self, x):
        for _ in range(10000):
            self.criticalsection(x) # Thực thi trong crictical section (process 2)

    def criticalsection(self, x):
        x.value += 1

    def main(self, step):
        x = multiprocessing.Value('i', 0)
        t1 = Process(target=self.process_1, args=(x,))  # Gọi đến process 1
        t1.start()
        t2 = Process(target=self.process_2, args=(x,))  # Gọi đến process 2
        t2.start()

        t1.join()
        t2.join()

        print(f'Step {step + 1}: x = {x.value}')


if __name__ == '__main__':
    c = CricticalSection()
    for i in range(10):
        c.main(step=i)
{% endhighlight %}

Trong ví dụ trên có sử dụng ctypes object là <strong><i>multiprocessing.Value</i></strong> để tạo shared memory cho các tiến trình khác nhau, chúng ta có thể tham khảo chi tiết hơn <a href="https://www.kite.com/python/docs/multiprocessing.Value" target="_blank">tại đây</a>. Output của chương trình trên tại lần chạy đầu tiên thu được như sau:

{% highlight text %}
Step 1: x = 11571
Step 2: x = 11779
Step 3: x = 10834
Step 4: x = 11760
Step 5: x = 19729
Step 6: x = 18965
Step 7: x = 11355
Step 8: x = 19504
Step 9: x = 19224
Step 10: x = 12202
{% endhighlight %}

Tại lần chạy tiếp theo kết quả vẫn là hoàn toàn khác biệt so với lần đầu:

{% highlight text %}
Step 1: x = 10661
Step 2: x = 12165
Step 3: x = 15036
Step 4: x = 19132
Step 5: x = 11817
Step 6: x = 10217
Step 7: x = 14314
Step 8: x = 10497
Step 9: x = 17631
Step 10: x = 14249
{% endhighlight %}

Khi nhiều tiến trình hoặc luồng cùng truy cập vào một đoạn mã giống nhau thì đoạn mã đó được gọi là <strong><i>critical section</i></strong>. <strong><i>Critical section</i></strong> chứa các biến hoặc tài nguyên chung cần được đồng bộ hóa để duy trì tính nhất quán của biến dữ liệu. Trong 2 ví dụ trên, khi một tiến trình hoặc luồng cố gắng thay đổi giá trị của dữ liệu được chia sẻ cùng lúc khi một tiến trình hoặc luồng khác cố gắng đọc giá trị, kết quả cuối cùng là không thể đoán trước được. Chúng ta thấy <strong><i>critical section</i></strong> không được duy trì tính nhất quán trong quá trình đọc và ghi dữ liệu liệu dẫn đến xung đột.

### Tổng quát hoá cơ chế Mutual exclusion (Semaphore)

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/SemaphoreFlags.jpg" alt="Semaphore và ứng dụng trong đời sống">
  <figcaption>
	  <i>Semaphore và ứng dụng trong đời sống</i>
  </figcaption>
</center>
</figure>

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/SemaphoreSharedResource.png" alt="Cơ chế semaphore trong khoa học máy tính">
  <figcaption>
	  <i>Cơ chế semaphore trong khoa học máy tính</i>
  </figcaption>
</center>
</figure>

Trong khoa học máy tính, semaphore hiểu đơn giản chỉ là một biến đếm với giá trị có thể thay đổi (tăng hoặc giảm) tùy thuộc vào nhu cầu do người lập trình xác định. Biến đếm này kiểm soát quá trình truy cập của các luồng hoặc tiến trình vào một tài nguyên dùng chung để tránh xảy ra các vấn đề <strong><i>critical section</i></strong>.

### Xây dựng cơ chế Mutual exclusion bằng semaphore trong Python

Với ví dụ ở trường hợp nhiều luồng cùng tranh chấp sử dụng tài nguyên chung, chúng ta sẽ sử dụng <strong><i>semaphore</i></strong> với 2 phương thức là <strong><i>acquire()</i></strong> và <strong><i>release()</i></strong> để khoá tài nguyên chung lại, chỉ cho phép một luồng được thực thi trên vùng tài nguyên chung này tại một thời điểm.

{% highlight python %}
import threading
from threading import Thread

class CricticalSection():
    def __init__(self):
        self.sem = threading.Semaphore()  # Khởi tạo semaphore

    def thread_1(self):
        for _ in range(1000000):
            self.criticalsection()  # Thực thi trong crictical section (thread 1)

    def thread_2(self):
        for _ in range(1000000):
            self.criticalsection()  # Thực thi trong crictical section (thread 2)

    def criticalsection(self):
        self.sem.acquire()
        global x
        x += 1
        self.sem.release()

    def main(self, step):
        global x
        x = 0
        t1 = Thread(target=self.thread_1)  # Gọi đến thread 1
        t1.start()
        t2 = Thread(target=self.thread_2)  # Gọi đến thread 2
        t2.start()

        t1.join()
        t2.join()

        print(f'Step {step + 1}: x = {x}')

if __name__ == '__main__':
    c = CricticalSection()
    for i in range(10):
        c.main(step=i)

{% endhighlight %}

Output của chương trình trên tại mọi lần thực thi đều thu được kết quả như sau:

{% highlight text %}
Step 1: x = 2000000
Step 2: x = 2000000
Step 3: x = 2000000
Step 4: x = 2000000
Step 5: x = 2000000
Step 6: x = 2000000
Step 7: x = 2000000
Step 8: x = 2000000
Step 9: x = 2000000
Step 10: x = 2000000
{% endhighlight %}


### Tài liệu tham khảo

* <a href="https://www.sciencedirect.com/topics/computer-science/mutual-exclusion" target="_blank">https://www.sciencedirect.com/topics/computer-science/mutual-exclusion</a>
* <a href="https://www.geeksforgeeks.org/mutual-exclusion-in-synchronization" target="_blank">https://www.geeksforgeeks.org/mutual-exclusion-in-synchronization</a>
* <a href="https://docs.python.org/3/library/multiprocessing.html" target="_blank">https://docs.python.org/3/library/multiprocessing.html</a>
* <a href="https://en.wikipedia.org/wiki/Semaphore_(programming)" target="_blank">https://en.wikipedia.org/wiki/Semaphore_(programming)</a>
* <a href="https://www.geeksforgeeks.org/g-fact-70" target="_blank">https://www.geeksforgeeks.org/g-fact-70</a>
