---
layout: post
title: Giải thích chi tiết về mạng Long Short-Term Memory (LSTM)
description: LSTM được thiết kế để giải quyết các bài toán về phụ thuộc xa (long-term dependencies) trong RNN do bị ảnh hưởng bởi vấn đề gradient biến mất.
excerpt: LSTM là một phiên bản mở rộng của mạng RNN, được đề xuất vào năm 1997 bởi Sepp Hochreiter và Jürgen Schmidhuber. LSTM được thiết kế để giải quyết các bài toán về phụ thuộc xa (long-term dependencies) trong mạng RNN do bị ảnh hưởng bởi vấn đề gradient biến mất. Có thể hiểu một cách đơn giản là mạng RNN cơ bản trong thực tế không có khả năng ghi nhớ thông tin từ các bước có khoảng cách xa và do đó những phần tử đầu tiên trong chuỗi đầu vào không có nhiều ảnh hưởng đến các kết quả tính toán dự đoán phần tử cho chuỗi đầu ra trong các bước sau.
keywords: Long Short Term Memory, mạng LSTM, mạng RNN, học sâu, deep learning
author: Nguyễn Trường Long
---
