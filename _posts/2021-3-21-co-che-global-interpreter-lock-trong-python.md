---
layout: post
title: Cơ chế Global Interpreter Lock trong Python
description: 
keywords:
excerpt:
author: Nguyễn Trường Long
---

### Giới thiệu về cơ chế Global Interpreter Lock

Python chung cấp các module hỗ trợ cho cả xử lý đa luồng và xử lý đa tiến trình.

Trong ngôn ngữ lập trình Python tồn tại một cơ chế được gọi là Global Interpreter Lock (GIL). Cơ chế này không cho phép tăng hiệu suất của các chương trình đa luồng lên nhiều và thậm chí có thể làm giảm hiệu suất của một số chương trình đa luồng.

Cơ chế GIL quy định rằng Python chỉ sử dụng một luồng duy nhất để thực thi các lệnh lập trình trong một chương trình. Điều này có nghĩa là trong Python tại một thời điểm chỉ có một luồng duy nhất được thực thi. Hiệu suất của một chương trình đơn luồng và chương trình đa luồng là tương đương nhau trong Python.

### Cơ chế GIL đối với I/O-bound và CPU-bound

### Tài liệu tham khảo

* <a href="https://www.geeksforgeeks.org/what-is-the-python-global-interpreter-lock-gil/" target="_blank">https://www.geeksforgeeks.org/what-is-the-python-global-interpreter-lock-gil/</a>
