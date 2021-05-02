---
layout: post
title: Cơ chế Mutual Exclusion trong lập trình Python
description: Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm.
keywords: Cơ chế Mutual Exclusion, Mutual Exclusion, mutex, loại trừ tương hỗ, khóa loại trừ lẫn nhau, lập trình Python, Python, lập trình đồng thời, lập trình đa luồng, lập trình multithreading, multiprocessing python, critical section
excerpt: Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm.
author: Nguyễn Trường Long
---

### Giới thiệu về mutual exclusion

Mutual exclusion (khóa loại trừ lẫn nhau) là một cơ chế thường được sử dụng để đồng bộ hóa các tiến trình hoặc luồng cần truy cập vào một số tài nguyên được chia sẻ trong các chương trình. Cơ chế này ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ để tránh xảy ra các vấn đề race condition. Nó quy định rằng nếu một tiến trình hoặc luồng khóa một tài nguyên, thì một tiến trình khác muốn truy cập vào nó sẽ cần phải đợi cho đến khi tiến trình đầu tiên mở khóa. Khi tiến trình hoặc luồng thứ hai này nắm giữ tài nguyên được chia sẻ, nó cũng sẽ tiến hành khóa tài nguyên này lại cho đến khi nó xử lý hoàn tất và quy trình này cứ lặp lại tiếp tục.

Khái niệm này được sử dụng trong lập trình cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm. Khi một tiến trình hoặc luồng nắm giữ một tài nguyên, nó phải khóa quyền truy cập vào tài nguyên được chia sẻ từ các tiến trình hoặc luồng khác để ngăn chặn các truy cập đồng thời vào cùng một tài nguyên. Đến khi giải phóng tài nguyên được chia sẻ, tiến trình hoặc luồng sẽ rời khỏi critical section và cho phép các tiến trình hoặc luồng khác tiến vào critical section.

### Vấn đề critical section

{% highlight python %}
import threading

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

    def main(self):
        global x
        x = 0
        t1 = threading.Thread(target=self.thread_1)  # Gọi đến thread 1
        t1.start()
        t2 = threading.Thread(target=self.thread_2)  # Gọi đến thread 2
        t2.start()

        t1.join()
        t2.join()


if __name__ == '__main__':
    c = CricticalSection()
    for i in range(10):
        c.main()
        print(f'Step {i + 1}: x = {x}')
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

Thử chạy lại chương trình trên một lần nữa. Kết quả mình thu được lại hoàn toàn khác so với lần chạy đầu tiên:
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

### Mutual exclusion trong single computer system và distributed system

### Tài liệu tham khảo

* <a href="https://www.sciencedirect.com/topics/computer-science/mutual-exclusion" target="_blank">https://www.sciencedirect.com/topics/computer-science/mutual-exclusion</a>
* <a href="https://www.geeksforgeeks.org/mutual-exclusion-in-synchronization" target="_blank">https://www.geeksforgeeks.org/mutual-exclusion-in-synchronization</a>
* <a href="https://docs.python.org/3/library/multiprocessing.html" target="_blank">https://docs.python.org/3/library/multiprocessing.html</a>

