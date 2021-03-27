---
layout: post
title: Cơ chế Mutual Exclusion trong lập trình Python
description: Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm.
keywords: Cơ chế Mutual Exclusion, Mutual Exclusion, mutex, loại trừ tương hỗ, lập trình Python, Python, lập trình đồng thời, lập trình đa luồng, lập trình multithreading, lập trình multithreading, critical section
excerpt: Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm.
author: Nguyễn Trường Long
---

Mutual exclusion là một cơ chế ngăn chặn việc truy cập đồng thời vào tài nguyên được chia sẻ. Khái niệm này được sử dụng trong lập trình đồng thời cùng với critical section, quy định rằng chỉ có một tiến trình hoặc luồng chứa critical section tại một thời điểm. Khi một tiến trình hoặc luồng nắm giữ một tài nguyên, nó phải khóa quyền truy cập vào tài nguyên được chia sẻ từ các tiến trình hoặc luồng khác để ngăn chặn các truy cập đồng thời vào cùng một tài nguyên. Đến khi giải phóng tài nguyên được chia sẻ, tiến trình hoặc luồng sẽ rời khỏi critical section và cho phép các luồng hoặc tiến trình khác tiến vào critical section.
