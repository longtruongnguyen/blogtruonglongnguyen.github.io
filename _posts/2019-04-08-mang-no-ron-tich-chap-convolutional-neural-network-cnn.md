---
layout: post
title: Mạng nơ-ron tích chập (Convolutional Neural Network - CNN)
description: Convolutional Neural Network có kiến trúc khá giống một mạng nơ-ron truyền thẳng thông thường, bao gồm các nơ-ron có khả năng tự tối ưu hóa thông qua quá trình học.
excerpt: Đối với một số loại dữ liệu, đặc biệt là dữ liệu ở dạng hình ảnh, mạng nơ-ron truyền thẳng nhiều lớp tỏ ra không hiệu quả để đáp ứng xử lý tốt. Để áp dụng mạng nơ-ron truyền thẳng nhiều lớp cho việc xử lý các dữ liệu ở dạng hình ảnh, chúng ta cần phải chuyển đổi được hình ảnh về dưới dạng vector.
keywords: mạng tích chập cnn, mạng cnn, Convolutional Neural Network, mạng Convolutional Neural Network, mạng nơ-ron tích chập CNN, mạng nơ-ron tích chập
author: Nguyễn Trường Long
---

[Mạng nơ-ron tích chập (Convolutional Neural Networks - CNN)](https://nguyentruonglong.net/mang-no-ron-tich-chap-convolutional-neural-network-cnn.html) là một loại mạng neural network đã đạt được nhiều thành tựu trong các bài toán có liên quan đến hình ảnh như nhận dạng hình ảnh (image recognition) và phân lớp hình ảnh (image classification) hiện nay. Ngoài ra, [mạng CNN](https://nguyentruonglong.net/mang-no-ron-tich-chap-convolutional-neural-network-cnn.html) còn được ứng dụng trong các bài toán xử lý ngôn tự nhiên (natural language processing) như phát hiện thư rác (spam detection), phân loại văn bản (topic categorization),...

Các mạng nơ-ron truyền thẳng nhiều lớp nhiều lớp (multilayer perceptron) chỉ được xây dựng để nhận dữ liệu đầu vào dưới dạng vector. Đối với một số loại dữ liệu, đặc biệt là dữ liệu ở dạng hình ảnh, mạng nơ-ron truyền thẳng nhiều lớp tỏ ra không hiệu quả để đáp ứng xử lý tốt. Để áp dụng mạng nơ-ron truyền thẳng nhiều lớp cho việc xử lý các dữ liệu ở dạng hình ảnh, chúng ta cần phải chuyển đổi được hình ảnh về dưới dạng vector. Điều này thường gây ra sự mất mát nhiều thông tin trong dữ liệu gốc ban đầu. [Mạng CNN](https://nguyentruonglong.net/mang-no-ron-tich-chap-convolutional-neural-network-cnn.html) được giới thiệu bởi LeCun đã loại bỏ việc trích xuất một cách thủ công các đặc trưng.

[Mạng CNN](https://nguyentruonglong.net/mang-no-ron-tich-chap-convolutional-neural-network-cnn.html) được có kiến trúc được cấu tạo bởi một số loại layer bao gồm:
- Convolutional layer
- Pooling layer
- Fully connected layer

### Toán tử tích chập (convolution operation)

### Convolutional layer
Sự tích chập riêng biệt giữa hai hàm $f$ và $g$ được định nghĩa như sau:
{% raw %}
$$\left( {f * g} \right)\left( x \right) = \sum\limits_t {f\left( t \right)} g\left( {x + t} \right)$$
{% endraw %}

Đối với tín hiệu 2 chiều như hình ảnh, chúng ta xem xét 2D-convolutions:
{% raw %}
$$\left( {K * I} \right)\left( {i,j} \right) = \sum\limits_{m,n} {K\left( {m,n} \right)} I\left( {i + n,j + m} \right)$$
{% endraw %}

<figure class="image">
  <img src="https://nguyentruonglong.net/images/2DConvolution.png" alt="Ví dụ minh họa về 2D-Convolution">
  <figcaption><center><i>Một ví dụ minh họa về 2D-Convolution</i></center></figcaption>
</figure>


(Bài viết đang trong quá trình hoàn thiện)
