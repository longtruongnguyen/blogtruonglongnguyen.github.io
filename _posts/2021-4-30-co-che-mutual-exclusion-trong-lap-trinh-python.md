---
layout: post
title: Cơ chế Mutual Exclusion trong lập trình Python
description: Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm.
keywords: Cơ chế Mutual Exclusion, Mutual Exclusion, mutex, loại trừ tương hỗ, lập trình Python, Python, lập trình đồng thời, lập trình đa luồng, lập trình multithreading, lập trình multithreading, critical section
excerpt: Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm.
author: Nguyễn Trường Long
---

Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm. Khi một tiến trình hoặc luồng nắm giữ một tài nguyên, nó phải khóa quyền truy cập vào tài nguyên được chia sẻ từ các tiến trình hoặc luồng khác để ngăn chặn các truy cập đồng thời vào cùng một tài nguyên. Đến khi giải phóng tài nguyên được chia sẻ, tiến trình hoặc luồng sẽ rời khỏi critical section và cho phép các luồng hoặc tiến trình khác tiến vào critical section.

{% highlight python %}
import threading
import time

class CricticalSection():
    def __init__(self):
        # Khởi tạo semaphore sử dụng Semaphore class trong threading module
        self.sem = threading.Semaphore()

    def thread_1(self):
        while True:
            print("Entry Section 1")
            self.sem.acquire()      # Giảm giá trị của semahpore

            self.criticalsection()  # Bắt đầu crictical section (thread 1)
            # Tăng giá trị của semaphore để cho phép luồng khác tiến vào critical section
            self.sem.release()

            print("Critical Section over for thread 1")
            time.sleep(3)

    def thread_2(self):
        while True:
            print("Entry Section 2")
            self.sem.acquire()      # Giảm giá trị của semahpore

            self.criticalsection()  # Bắt đầu crictical section (thread 2)
            # Tăng giá trị của semaphore để cho phép luồng khác tiến vào critical section
            self.sem.release()

            print("Critical Section over for thread 2")
            time.sleep(3)

    def criticalsection(self):
        print(" Entered Critical Section! Perform operation on shared resource")

    def main(self):
        t1 = threading.Thread(target=self.thread_1)  # Gọi đến thread 1
        t1.start()
        t2 = threading.Thread(target=self.thread_2)  # Gọi đến thread 2
        t2.start()

if __name__ == "__main__":
    c = CricticalSection()
    c.main()
{% endhighlight %}
