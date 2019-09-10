---
layout: post
title: Thuật toán Gradient Descent
description: Ý tưởng của thuật toán gradient descent là chúng ta sẽ bắt đầu tại một điểm tùy ý, sau đó di chuyển dọc theo hướng ngược lại của gradient tại điểm đó, tiếp tục lặp lại quá trình này cho đến khi hy vọng có thể hội tụ tại điểm dừng.
excerpt: Trong toán học, gradient là một trường hợp tổng quát của đạo hàm. Trong khi đạo hàm được định nghĩa trên các hàm số đơn biến và có giá trị vô hướng, gradient có giá trị là một vector. Giống như đạo hàm, gradient biểu diễn độ dốc tiếp tuyến (tangent) của đồ thị hàm số. Gradient của một hàm đa biến là một vector chứa tất cả các đạo hàm riêng phần (partial derivatives) của hàm đó.
thumbnail: https://nguyentruonglong.net/images/understanding-gradient-descent.png
keywords: thuật toán gradient descent, gradient descent, giải thuật gradient descent, phương pháp gradient descent, gradient
author: Nguyễn Trường Long
---

### Giới thiệu thuật toán gradient descent
Trong toán học, gradient là một trường hợp tổng quát của đạo hàm. Trong khi đạo hàm được định nghĩa trên các hàm số đơn biến và có giá trị vô hướng, gradient có giá trị là một vector. Giống như đạo hàm, gradient biểu diễn độ dốc tiếp tuyến (tangent) của đồ thị hàm số. Gradient của một hàm đa biến {% raw %}$$f\left( {{x_1},..,{x_M}} \right)$${% endraw %} là một vector chứa tất cả các đạo hàm riêng phần (partial derivatives) của hàm $$f$$ và được ký hiệu là $$\nabla f$$. Phần tử $$i$$ trong gradient là đạo hàm riêng phần của hàm $$f$$ theo biến $${x_i}$$.

Cho hàm {% raw %}$$f:{\mathbb{R}^n} \to \mathbb{R}$${% endraw %} là hàm lồi và khả vi, bài toán chúng ta cần giải quyết là tìm $${x^*}$$ sao cho:
{% raw %}
$$\begin{align}
f\left( {{x^*}} \right) = \min f\left( x \right)
\end{align}$$
{% endraw %}

Xem xét bài toán trên, như chúng ta đã biết rằng để tìm cực tiểu của một hàm lồi, ta cần phải tìm điểm dừng của hàm số đó. Trong toán học, điểm dừng (stationary point) của một hàm khả vi là điểm mà mọi phần tử của gradient tại điểm đó đều bằng $$0$$. Ý tưởng của [phương pháp gradient descent](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) là chúng ta sẽ bắt đầu tại một điểm tùy ý, sau đó di chuyển dọc theo hướng ngược lại của gradient tại điểm đó, tiếp tục lặp lại quá trình này cho đến khi hy vọng có thể hội tụ tại điểm dừng. Hình bên dưới đã minh họa ý tưởng này.

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/understanding-gradient-descent.png" alt="Ảnh minh họa cho quá trình lặp của thuật toán gradient descent trong không gian 2 chiều">
  <figcaption>
	  <i>Ảnh minh họa cho quá trình lặp của thuật toán gradient descent trong không gian 2 chiều</i>
  </figcaption>
</center>
</figure>

Cụ thể hơn, chúng ta sẽ xác định hướng và kích thước di chuyển thông qua mô tả bằng các công thức toán học. Bắt đầu tại một điểm {% raw %}$${x^{\left( 0 \right)}} \in {\mathbb{R}^n}$${% endraw %} bất kỳ, chúng ta sẽ di chuyển theo hướng {% raw %}$$\nabla f\left( {{x^{\left( k \right)}}} \right)$${% endraw %} tại mỗi lần lặp $k \ge 0$ với kích thước lặp ${t_k}$ (step size) tới điểm tiếp theo {% raw %}$${x^{\left( {k + 1} \right)}}$${% endraw %}. Quá trình lặp này được tóm gọn trong công thức sau đây:
{% raw %}
$$\begin{align}
	{x^{\left( {k + 1} \right)}} = {x^{\left( k \right)}} - {t_k}\nabla f\left( {{x^{\left( k \right)}}} \right)
\end{align}$$
{% endraw %}

Chúng ta có thể lựa chọn kích thước lặp cố định ${t_k} = t$ với t là một số dương hoặc kích thước lặp được ước lượng tại mỗi lần lặp thông qua công thức sau:
{% raw %}
$$\begin{align}
{t_k} = \arg {\min _{t \ge 0}}f\left( {{x^{\left( k \right)}} - t\nabla f\left( {{x^{\left( k \right)}}} \right)} \right)
\end{align}$$
{% endraw %}

Quá trình lặp dừng lại tại một số điểm hoặc khi thỏa mãn điều kiện mà bài toán chúng ta cần giải quyết đặt ra. Với độ chính xác $\varepsilon  > 0$ cho trước, [thuật toán gradient descent](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) có thể được trình bày cụ thể như sau:

{% raw %}
$$\begin{array}{l}
1:\,\,{\rm{Guess}}\,\,{x^{\left( 0 \right)}},\,\,{\rm{set}}\,\,k \leftarrow 0\\
2:\,\,{\rm{while}}\,\,\left\| {\nabla f\left( {{x^{\left( k \right)}}} \right)} \right\| \ge \varepsilon \,\,{\rm{do}}\\
3:\,\,\,\,\,\,\,\,\,\,\,\,{x^{\left( {k + 1} \right)}} = {x^{\left( k \right)}} - {t_k}\nabla f\left( {{x^{\left( k \right)}}} \right)\\
4:\,\,\,\,\,\,\,\,\,\,\,\,k \leftarrow k + 1\\
5:\,\,{\rm{end}}\,{\rm{while}}\\
6:\,\,{\rm{return}}\,\,{x^{\left( k \right)}}
\end{array}$$
{% endraw %}

### Ứng dụng thuật toán gradient descent trong machine learning

Trong quá trình huấn luyện các [mô hình mạng nơ-ron](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html), [thuật toán gradient descent](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) được sử dụng để xác định bộ trọng số $w$ sao cho hàm mất mát {% raw %}$$E\left( w \right)$${% endraw %} đạt cực tiểu. Trong phạm vi của bài viết này, mình sẽ trình bày những ý tưởng tổng quát về quá trình áp dụng [thuật toán gradient descent](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) trong machine learning và không tập trung đi quá sâu chi tiết về mặt toán học.

Xét hàm mất mát {% raw %}$$E\left( w \right)$${% endraw %} là một hàm khả vi (differentiable) và liên tục (continuously) với tham số là bộ trọng số $w$. Hàm {% raw %}$$E\left( w \right)$${% endraw %} sẽ ánh xạ bộ trọng số $w$ sang số thực. Chúng ta sẽ tìm {% raw %}$$w^*$${% endraw %} thỏa mãn điều kiện:

{% raw %}
$$\begin{align}
\nabla E\left( {{w^*}} \right) = 0
\end{align}$$
{% endraw %}

Trong đó, $\nabla$ là toán tử gradient:

{% raw %}
$$\begin{align}
\nabla  = {\left[ {\frac{\partial }{{\partial {w_1}}},\frac{\partial }{{\partial {w_2}}},...,\frac{\partial }{{\partial {w_M}}}} \right]^T}
\end{align}$$
{% endraw %}

{% raw %}$$\nabla E\left( w \right)$${% endraw %} là gradient của hàm mất mát:

{% raw %}
$$\begin{align}
\nabla {\rm E}\left( w \right) = {\left[ {\frac{{\partial E}}{{\partial {w_1}}},\frac{{\partial E}}{{\partial {w_2}}},...,\frac{{\partial E}}{{\partial {w_M}}}} \right]^T}
\end{align}$$
{% endraw %}

Chúng ta bắt đầu bằng cách tạo một ước đoán ngẫu nhiên ban đầu là {% raw %}$$w\left( 0 \right)$${% endraw %}, sau đó cập nhật các trọng số này sao cho giá trị hàm mất mát {% raw %}$${\rm E}\left( w \right)$${% endraw %} được giảm dần tại mỗi lần lặp của thuật toán:

{% raw %}
$$\begin{align}
E\left( {w\left( {n + 1} \right)} \right) < E\left( {w\left( n \right)} \right)
\end{align}$$
{% endraw %}

Trong đó {% raw %}$$w\left( n \right)$${% endraw %} là giá trị cũ của bộ trọng số và {% raw %}$$w\left( {n + 1} \right)$${% endraw %} là giá trị mới được cập nhật.

[Thuật toán gradient descent](https://nguyentruonglong.net/thuat-toan-gradient-descent.html) sẽ điều chỉnh bộ trọng số $w$ sao cho hàm mất mát ngày càng đạt giá trị tối thiểu. Việc điều chỉnh bộ trọng số $w$ tại mỗi lần lặp của thuật toán được áp dụng theo hướng ngược lại với vector gradient:

{% raw %}
$$\begin{align}
w\left( {n + 1} \right) = w\left( n \right) - \eta \nabla {\rm E}\left( {w\left( n \right)} \right)
\end{align}$$
{% endraw %}

Trong đó $\eta$ là một số thực dương được gọi là learning rate hoặc step size. {% raw %}$$\nabla E\left( {w\left( n \right)} \right)$${% endraw %} là vector gradient tại điểm {% raw %}$${w\left( n \right)}$${% endraw %}. Giá trị learning rate có ảnh hưởng rất lớn đến việc hội tụ của [thuật toán gradient descent](https://nguyentruonglong.net/thuat-toan-gradient-descent.html). Nếu learning rate nhỏ, thuật toán sẽ hội tụ chậm, nếu learning rate lớn, thuật toán sẽ hội tụ tiến nhanh đến mục tiêu. Tuy nhiên khi learning rate vượt qua một ngưỡng quan trọng nhất định, thuật toán sẽ dẫn đến hiện tượng phân kỳ.
