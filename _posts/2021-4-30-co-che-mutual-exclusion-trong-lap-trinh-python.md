---
layout: post
title: Cơ chế Mutual Exclusion trong lập trình Python
description: Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm.
keywords: Cơ chế Mutual Exclusion, Mutual Exclusion, mutex, loại trừ tương hỗ, khóa loại trừ lẫn nhau, lập trình Python, Python, lập trình đồng thời, lập trình đa luồng, lập trình multithreading, multiprocessing python, critical section
excerpt: Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm.
author: Nguyễn Trường Long
---

### Giới thiệu về mutual exclusion

Mutual exclusion (khóa loại trừ lẫn nhau) là một cơ chế thường được sử dụng để đồng bộ hóa các tiến trình cần truy cập vào một số tài nguyên được chia sẻ trong các chương trình song song (parallel program). Cơ chế này ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ để tránh xảy ra các vấn đề race condition. Nó quy định rằng nếu một tiến trình khóa một tài nguyên, thì một tiến trình khác muốn truy cập vào nó sẽ cần phải đợi cho đến khi tiến trình đầu tiên mở khóa. Khi tiến trình thứ hai này nắm giữ tài nguyên được chia sẻ, nó cũng sẽ tiến hành khóa tài nguyên này lại cho đến khi nó xử lý hoàn tất và quy trình này cứ lặp lại tiếp tục.

Khái niệm này được sử dụng trong lập trình cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm. Khi một tiến trình hoặc luồng nắm giữ một tài nguyên, nó phải khóa quyền truy cập vào tài nguyên được chia sẻ từ các tiến trình hoặc luồng khác để ngăn chặn các truy cập đồng thời vào cùng một tài nguyên. Đến khi giải phóng tài nguyên được chia sẻ, tiến trình hoặc luồng sẽ rời khỏi critical section và cho phép các luồng hoặc tiến trình khác tiến vào critical section.

### Vấn đề critical section

{% highlight python %}
from multiprocessing import Process, Lock
import time

class CricticalSection():
    def __init__(self):
        # Khởi tạo lock trong multiprocessing module
        self.lock = Lock()

    def process_1(self):
        while True:
            print("Entry Section 1")
            self.lock.acquire()

            self.criticalsection()  # Bắt đầu crictical section (process 1)
            # Tăng giá trị của semaphore để cho phép tiến trình khác tiến vào critical section
            self.lock.release()

            print("Critical Section over for process 1")
            time.sleep(3)

    def process_2(self):
        while True:
            print("Entry Section 2")
            self.lock.acquire()

            self.criticalsection()  # Bắt đầu crictical section (process 2)
            # Tăng giá trị của semaphore để cho phép tiến trình khác tiến vào critical section
            self.lock.release()

            print("Critical Section over for process 2")
            time.sleep(3)

    def criticalsection(self):
        print("Entered Critical Section! Perform operation on shared resource")

    def main(self):
        t1 = Process(target=self.process_1)  # Gọi đến process 1
        t1.start()
        t2 = Process(target=self.process_2)  # Gọi đến process 2
        t2.start()

if __name__ == "__main__":
    c = CricticalSection()
    c.main()
{% endhighlight %}

Output của chương trình trên sẽ là:
{% highlight text %}
Entry Section 2
Entered Critical Section! Perform operation on shared resource
Critical Section over for process 2
Entry Section 1
Entered Critical Section! Perform operation on shared resource
Critical Section over for process 1
Entry Section 2
Entered Critical Section! Perform operation on shared resource
Critical Section over for process 2
Entry Section 1
Entered Critical Section! Perform operation on shared resource
Critical Section over for process 1
Entry Section 2
Entered Critical Section! Perform operation on shared resource
Critical Section over for process 2
Entry Section 1
Entered Critical Section! Perform operation on shared resource
Critical Section over for process 1
Entry Section 2
Entered Critical Section! Perform operation on shared resource
Critical Section over for process 2
{% endhighlight %}

### Mutual exclusion trong single computer system và distributed system

### Tài liệu tham khảo

* <a href="https://www.sciencedirect.com/topics/computer-science/mutual-exclusion" target="_blank">https://www.sciencedirect.com/topics/computer-science/mutual-exclusion</a>
* <a href="https://www.geeksforgeeks.org/mutual-exclusion-in-synchronization" target="_blank">https://www.geeksforgeeks.org/mutual-exclusion-in-synchronization</a>
* <a href="https://docs.python.org/3/library/multiprocessing.html" target="_blank">https://docs.python.org/3/library/multiprocessing.html</a>

