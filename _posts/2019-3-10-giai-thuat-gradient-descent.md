---
layout: post
title: Giải thuật Gradient Descent
description: Ý tưởng của giải thuật gradient descent là chúng ta sẽ bắt đầu tại một điểm tùy ý, sau đó di chuyển dọc theo hướng ngược lại của gradient tại điểm đó, tiếp tục lặp lại quá trình này cho đến khi hy vọng có thể hội tụ tại điểm dừng.
thumbnail: https://nguyentruonglong.net/images/understanding-gradient-descent.png
keywords: "gradient descent, giải thuật gradient descent, gradient"
author: Nguyễn Trường Long
---

Trong toán học, gradient là một trường hợp tổng quát của đạo hàm. Trong khi đạo hàm được định nghĩa trên các hàm số đơn biến và có giá trị vô hướng, gradient có giá trị là một vector. Giống như đạo hàm, gradient biểu diễn độ dốc tiếp tuyến (tangent) của đồ thị hàm số. Gradient của một hàm đa biến {% raw %}$$f\left( {{x_1},..,{x_M}} \right)$${% endraw %} là một vector chứa tất cả các đạo hàm riêng phần (partial derivatives) của hàm $$f$$ và được ký hiệu là $$\nabla f$$. Phần tử $$i$$ trong gradient là đạo hàm riêng phần của hàm $$f$$ theo biến $${x_i}$$.

Cho hàm {% raw %}$$f:{\mathbb{R}^n} \to \mathbb{R}$${% endraw %} là hàm lồi và khả vi, bài toán chúng ta cần giải quyết là tìm $${x^*}$$ sao cho:
{% raw %}
$$\begin{align}
f\left( {{x^*}} \right) = \min f\left( x \right)
\end{align}$$
{% endraw %}

Xem xét bài toán trên, như chúng ta đã biết rằng để tìm cực tiểu của một hàm lồi, ta cần phải tìm điểm dừng của hàm số đó. Trong toán học, điểm dừng (stationary point) của một hàm khả vi là điểm mà mọi phần tử của gradient tại điểm đó đều bằng $$0$$. Ý tưởng của phương pháp [gradient descent](https://nguyentruonglong.net/giai-thuat-gradient-descent.html) là chúng ta sẽ bắt đầu tại một điểm tùy ý, sau đó di chuyển dọc theo hướng ngược lại của gradient tại điểm đó, tiếp tục lặp lại quá trình này cho đến khi hy vọng có thể hội tụ tại điểm dừng. Hình bên dưới đã minh họa ý tưởng này.

![](https://nguyentruonglong.net/images/understanding-gradient-descent.png)

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

Quá trình lặp dừng lại tại một số điểm hoặc khi thỏa mãn điều kiện mà bài toán chúng ta cần giải quyết đặt ra. Với độ chính xác $\varepsilon  > 0$ cho trước, [giải thuật gradient descent](https://nguyentruonglong.net/giai-thuat-gradient-descent.html) có thể được trình bày cụ thể như sau:

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
