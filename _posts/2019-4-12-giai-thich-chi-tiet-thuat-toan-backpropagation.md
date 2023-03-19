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

[Thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) là một phương pháp tính toán đạo hàm ngược (reverse of differentiation) được áp dụng trong [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html), giúp tính toán các đạo hàm cần thiết để tối ưu hóa các tham số trong mô hình.

Ý tưởng đầu tiên về [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) được đề xuất bởi Paul Werbos vào năm 1974 trong bài báo "Beyond Regression: New Tools for Prediction and Analysis in the Behavioral Sciences". Tuy nhiên ý tưởng này chưa được biết đến rộng rãi cho đến khi nó được các tác giả David Rumelhart, Geoffrey Hinton và Ronald Williams phát triển và áp dụng vào [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html) trong bài báo "Learning representations by back-propagating errors" vào năm 1986. Bài báo này đã giúp cho [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) trở thành một phương pháp quan trọng để huấn luyện các mô hình [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html).

Kể từ đó thì [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) đã được sử dụng rộng rãi trong các ứng dụng của machine learning và deep learning. Tuy nhiên thuật toán này cũng gặp phải một số hạn chế như độ chính xác kém và khả năng vượt qua các vấn đề như vanishing gradient hay exploding gradient. Do đó hiện nay có nhiều biến thể của thuật toán Backpropagation được phát triển để giải quyết những hạn chế này. Một số biến thể cải tiến của [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) tiêu biểu bao gồm:

 - <i>Weight Decay</i>: Kỹ thuật này giúp tránh overfitting bằng cách thêm một chi phí phạt vào hàm mất mát để giảm giá trị của các tham số trong mô hình. Điều này giúp giảm khả năng mô hình bị overfitting và cải thiện năng lực dự đoán của mô hình.
 - <i>Batch Normalization</i>: Đây là một kỹ thuật khác để giúp cho quá trình huấn luyện nhanh hơn và ổn định hơn bằng cách chuẩn hóa giá trị đầu vào cho mỗi layer trong mạng nơ-ron. Batch Normalization giúp giảm hiện tượng overfitting trong quá trình huấn luyện.
 - <i>Adaptive Moment Estimation</i>: Đây là một biến thể khác của [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html), kết hợp giữa momentum và adaptive learning rate để cải thiện tốc độ học của mô hình. Nó tự động điều chỉnh learning rate cho từng tham số và giúp tăng tốc quá trình huấn luyện.
 - <i>Stochastic Gradient Descent with Momentum</i>: Biến thể này kết hợp giữa [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) và momentum để giảm thiểu việc rơi vào các điểm cực tiểu cục bộ. Nó sử dụng một hệ số momentum để giảm độ dao động của [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) và giúp giữ cho quá trình huấn luyện ổn định hơn.
 - <i>Nesterov Accelerated Gradient</i>: Biến thể này cũng kết hợp giữa [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) và momentum, nhưng sử dụng hệ số momentum với phương pháp Nesterov. Nó giúp cải thiện tốc độ hội tụ và giảm thiểu sự dao động của [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html).

### Ý tưởng của thuật toán Backpropagation

[Thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) được sử dụng để tính toán đạo hàm của hàm mất mát theo các tham số trong mô hình machine learning khi áp dụng [thuật toán gradient descent](https://nguyentruonglong.net/thuat-toan-gradient-descent.html). Trong mô hình machine learning thì số lượng tham số có thể là rất lớn, đôi khi lên đến hàng triệu tham số. Tính toán đạo hàm của hàm mất mát theo từng tham số bằng cách sử dụng công thức tính đạo hàm bình thường có thể rất phức tạp và tốn kém về thời gian và chi phí tính toán. [Thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) được thiết kế để tính toán đạo hàm của hàm mất mát theo từng tham số một cách hiệu quả hơn bằng cách sử dụng kỹ thuật lan truyền ngược (backward propagation) thông qua các lớp (layers) của mô hình. Quá trình tính toán đạo hàm này giúp [thuật toán gradient descent](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) điều chỉnh các tham số mô hình sao cho giá trị của hàm mất mát giảm dần theo thời gian, giúp tối ưu hóa hiệu suất huấn luyện cho mô hình.

Trong [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html), [quy tắc chuỗi đạo hàm (chain rule)](https://en.wikipedia.org/wiki/Chain_rule) được áp dụng để tính toán đạo hàm của hàm mất mát đối với từng trọng số của [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html). Quy tắc này cho phép chúng ta tính toán [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) của hàm mất mát theo từng trọng số. [Quy tắc chuỗi đạo hàm](https://en.wikipedia.org/wiki/Chain_rule) là một công cụ quan trọng trong tính toán đạo hàm của các hàm số phức tạp. Giả sử chúng ta có một hàm số {% raw %}$$f(x)$${% endraw %} có dạng hàm hợp:

{% raw %}
$$\begin{align}
f(x) = g(h(x))
\end{align}$$
{% endraw %}

Trong đó {% raw %}$$h(x)$${% endraw %} và {% raw %}$$g(x)$${% endraw %} là các hàm số có thể tính đạo hàm được. Theo [quy tắc chuỗi đạo hàm](https://en.wikipedia.org/wiki/Chain_rule), đạo hàm của {% raw %}$$f(x)$${% endraw %} theo {% raw %}$$x$${% endraw %} có thể tính được như sau:

{% raw %}
$$\begin{align}
\frac{df}{dx} = \frac{dg}{dh}\cdot\frac{dh}{dx}
\end{align}$$
{% endraw %}

Tức là chúng ta tính đạo hàm của hàm {% raw %}$$g(x)$${% endraw %} theo hàm số trung gian {% raw %}$$h(x)$${% endraw %}, và sau đó tính đạo hàm của {% raw %}$$h(x)$${% endraw %} theo {% raw %}$$x$${% endraw %}. Quy tắc này có thể được áp dụng đệ qui nếu hàm số {% raw %}$$f(x)$${% endraw %} phức tạp hơn và có nhiều hàm số trung gian.

Khi áp dụng [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) trong huấn luyện mô hình [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html), chúng ta cần tính toán đạo hàm của hàm mất mát theo các trọng số của mạng. <i>Hãy hình dung các lớp trong một [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html) giống như một một hàm hợp có nhiều lớp hàm trung gian phức tạp bên trong. Do đó hàm mất mát cho mô hình [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html) này cũng là một dạng hàm hợp phức tạp với nhiều lớp hàm trung gian tương tự</i>. Để tính đạo hàm này, chúng ta sử dụng [quy tắc chuỗi đạo hàm](https://en.wikipedia.org/wiki/Chain_rule) để tính toán đạo hàm của các hàm số trung gian trong quá trình lan truyền ngược từ đầu ra đến đầu vào của mạng. Việc tính toán [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) là rất quan trọng trong [thuật toán Gradient Descent](https://nguyentruonglong.net/thuat-toan-gradient-descent.html), được sử dụng để cập nhật trọng số của [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html) trong quá trình huấn luyện. Khi tính toán [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) bằng [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html), quy tắc chuỗi đạo hàm được áp dụng liên tiếp cho mỗi lớp trong [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html), bắt đầu từ lớp cuối cùng đến lớp đầu tiên.

[Thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) hoạt động bằng cách lan truyền giá trị [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) từ đầu ra của mô hình trở lại đầu vào để tính toán đạo hàm. [Thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) được chia thành hai pha:

 - <i>Pha feedforward (lan truyền tiến)</i>: Trong pha này, giá trị đầu vào được lan truyền qua [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html) để tính toán giá trị đầu ra. Các giá trị đầu ra này được sử dụng để tính toán giá trị hàm mất mát và [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) của hàm mất mát theo giá trị đầu ra của mô hình.
 - <i>Pha backpropagation (lan truyền ngược)</i>: Trong pha này, giá trị [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) tính được ở pha feedforward được lan truyền ngược lại từ đầu ra đến đầu vào của mô hình để tính toán [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) của hàm mất mát theo từng trọng số của mô hình. Quá trình lan truyền ngược được thực hiện bằng cách sử dụng [quy tắc chuỗi đạo hàm](https://en.wikipedia.org/wiki/Chain_rule) và tính toán đạo hàm theo từng lớp của mô hình [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html).

Quá trình lan truyền ngược được thực hiện như sau:

 - Tính toán [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) của hàm mất mát theo giá trị đầu ra của mô hình.
 - Lan truyền ngược giá trị [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) này từ đầu ra đến đầu vào của mô hình bằng cách sử dụng quy tắc chuỗi để tính toán giá trị [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) của hàm mất mát theo từng lớp của mô hình [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html).
 - Sử dụng giá trị [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) tính được ở bước trước để cập nhật các trọng số của mô hình bằng thuật toán [gradient descent](https://nguyentruonglong.net/thuat-toan-gradient-descent.html).

Với [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) thì việc tính toán [gradient](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) của hàm mất mát theo từng trọng số trong mô hình [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html) trở nên dễ dàng và hiệu quả hơn, giúp cho việc huấn luyện mô hình trở nên nhanh chóng và chính xác hơn.

### Tài liệu tham khảo

