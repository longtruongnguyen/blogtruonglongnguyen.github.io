---
layout: post
title: Giải thích chi tiết thuật toán Backpropagation
description: Thuật toán Backpropagation được sử dụng để tính toán đạo hàm của hàm mất mát theo các tham số trong mô hình machine learning khi áp dụng thuật toán gradient descent. 
excerpt: Trong mô hình machine learning, số lượng tham số có thể rất lớn, đôi khi lên đến hàng triệu tham số. Tính toán đạo hàm của hàm mất mát theo từng tham số bằng cách sử dụng công thức tính đạo hàm bình thường có thể rất phức tạp và tốn kém về thời gian tính toán. Thuật toán Backpropagation được thiết kế để tính toán đạo hàm của hàm mất mát theo từng tham số một cách hiệu quả hơn.
thumbnail:
keywords: thuật toán backpropagation, giải thuật backpropagation, backpropagation, học máy, trí tuệ nhân tạo, deep learning, machine learning
author: Nguyễn Trường Long
---

### Giới thiệu về thuật toán Backpropagation
