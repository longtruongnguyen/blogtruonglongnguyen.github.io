---
layout: post
title: Mô hình Skip-gram (Continuous Skip-gram)
description: Ý tưởng chính của mô hình Skip-gram là dự đoán từ các từ ngữ cảnh xung quanh dựa vào từ mục tiêu đầu vào trong một phạm vi nhất định.
keywords: mô hình Skip-gram, Skip-gram Model, mô hình Word2Vec, nhúng từ Skip-gram, Continuous Skip-gram Model
author: Nguyễn Trường Long
---

Ý tưởng của [mô hình Skip-gram](https://nguyentruonglong.net/mo-hinh-skip-gram.html) đối lập với [CBOW](https://nguyentruonglong.net/mo-hinh-cbow-continuous-bag-of-words.html), các từ mục tiêu bây giờ trở thành đầu vào và các từ ngữ cảnh trong câu trở thành đầu ra. Cho từ mục tiêu $${w_c}$$ tại vị trí $c$ trong câu văn bản, khi đó đầu vào của [mô hình Skip-gram](https://nguyentruonglong.net/mo-hinh-skip-gram.html) cũng chính là từ mục tiêu $${w_c}$$ và đầu ra của mô hình là các từ ngữ cảnh {% raw %}$$\left( {{w_{c - m}},...,{w_{c - 1}},{w_{c + 1}},...{w_{c + m}}} \right)$${% endraw %} xung quanh từ $${w_c}$$ trong phạm vi $$m$$.

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/SkipGram.png" alt="Ảnh minh họa cho mô hình Skip-gram ở dạng tổng quát">
  <figcaption><i>Ảnh minh họa cho mô hình Skip-gram ở dạng tổng quát</i></figcaption>
</center>
</figure>

Gọi {% raw %}$${v_{{w_I}}}$${% endraw %} là vector đầu vào đại diện cho từ đầu vào duy nhất ${w_I}$. Các từ trong câu đầu vào của mô hình được chuyển về dưới dạng vector one-hot ${x^{\left( k \right)}}$. Ma trận $W$ với kích thước $V\times N$ là ma trận trọng số từ lớp đầu vào đến lớp ẩn có dạng như sau:

{% raw %}
$$\begin{align}
	{W_{V \times N}} = \left[ {\begin{array}{*{20}{c}}
		{{w_{11}}}&{{w_{12}}}& \cdots &{{w_{1N}}}\\
		{{w_{21}}}&{{w_{22}}}& \cdots &{{w_{2N}}}\\
		\vdots & \vdots & \ddots & \vdots \\
		{{w_{{\rm{V1}}}}}&{{w_{{\rm{V2}}}}}& \ldots &{{w_{{\rm{VN}}}}}
		\end{array}} \right]
\end{align}$$
{% endraw %}

Trong ma trận $W$, mỗi hàng thứ $i$ của ma trận chính là vector đại diện tương ứng cho từ thứ $i$ trong tập từ vựng. Ma trận này thu được sau khi huấn luyện là kết quả cần quan tâm do chứa các vector đại diện cho các từ trong tập từ vựng. Ma trận $h$ của lớp ẩn kích thước là $N\times 1$ với $N$ do chúng ta định nghĩa có dạng như sau:

{% raw %}
$$\begin{align}
h = \left[ {\begin{array}{*{20}{c}}
	{{h_1}}\\
	{{h_2}}\\
	\vdots \\
	{{h_N}}
	\end{array}} \right]
\end{align}$$
{% endraw %}

Ma trận $W'$ có chiều $N\times V$ là ma trận trọng số từ lớp ẩn đến lớp đầu ra. Trong đầu ra thay vì chỉ có một phân phối, chúng ta tạo ra $C$ phân phối. Gọi $y_{c, j}$ là phần tử thứ $j$ trong vector đầu ra thứ $c$ với $c = 1, 2,... C$. Do ${x^{\left( k \right)}}$ là vector one-hot đầu vào duy nhất nên $h$ được tính như sau:
{% raw %}
$$\begin{equation}
h = W_{\left( {k, \cdot } \right)}^T = v{}_{{w_I}}^T
\end{equation}$$
{% endraw %}
Giá trị của $y_{c,j}$ biểu diễn cho xác suất xuất hiện của từ thứ $j$ trong tập từ vựng gồm $V$ từ ở đầu ra thứ $c$ được tính như sau:
{% raw %}
$$\begin{equation}
p\left( {{w_{c,j}} = {w_{O,c}}|{w_I}} \right) = {y_{c,j}} = \frac{{\exp \left( {{u_{c,j}}} \right)}}{{\sum\limits_{j' = 1}^V {\exp \left( {{u_{j'}}} \right)} }}
\end{equation}$$
{% endraw %}
Trong đó ${w_{c,j}}$ là từ thứ $j$ trong tập từ vựng gồm $V$ từ tương ứng ở đầu ra thứ $c$ và ${w_{O,c}}$ là từ ngữ cảnh đầu ra thứ $c$ hiện tại. Do các đầu ra đều sử dụng chung các trọng số nên $u_{c, j}$ được tính bằng công thức sau:
{% raw %}
$$\begin{align}
{u_{c,j}} = {u_j} = {v{_{{w_j}}^{'}}^T} \cdot h \text{  với  } c = 1,2,...,C
\end{align}$$
{% endraw %}
Trong đó {% raw %}$$v{_{{w_j}}^{'}}$${% endraw %} là vector đầu ra của từ thứ $j$ trong tập từ vựng ${w_j}$ và lấy từ cột tương ứng của ma trận trọng số $W'$. Hàm mất mát $E$ được cho bởi công thức sau:
{% raw %}
$$\begin{align}
E &=  - \log p\left( {{w_{O,1}},{w_{O,2}},...,{w_{O,C}}|{w_I}} \right)\\
&= - \log \prod\limits_{c = 1}^C {\frac{{\exp \left( {{u_{c,j_c^*}}} \right)}}{{\sum\limits_{j' = 1}^V {\exp \left( {{u_{j'}}} \right)} }}}\\
&=  - \sum\limits_{c = 1}^C {{u_{j_c^*}}}  + C \cdot \log \sum\limits_{j' = 1}^V {\exp \left( {{u_{j'}}} \right)}
\end{align}$$
{% endraw %}
Trong đó $j^{*}_{c}$ là vị trí hiện tại của từ ngữ cảnh thứ $c$ trong tập từ vựng. Các trọng số từ lớp ẩn đến lớp đầu ra trong ma trận $W'$ được cập nhật theo phương trình sau:
{% raw %}
$$\begin{align}
{v{_{{w_j}}^{'}}^{\left( {new} \right)}} = {v{_{{w_j}}^{'}}^{\left( {old} \right)}} - \eta  \cdot E{I_j} \cdot h \text{  với  } j = 1,2,...,V
\end{align}$$
{% endraw %}
Trong đó $E{I_j}$ được tính như sau:
{% raw %}
$$\begin{align}
	E{I_j} = \sum\limits_{c = 1}^C {\frac{{\partial E}}{{\partial {u_{c,j}}}}}
\end{align}$$
{% endraw %}
Tiếp đến các trọng số trong ma trận $W$ từ lớp đầu vào đến lớp ẩn được cập nhật như sau:
{% raw %}
$$\begin{equation}
{v_{{w_I}}}^{\left( {new} \right)} = {v_{{w_I}}}^{\left( {old} \right)} - \eta  \cdot E{H^T}
\end{equation}$$
{% endraw %}
Trong đó $EH$ là một vector có $N$ chiều và mỗi phần tử của nó được tính như sau:
{% raw %}
$$\begin{align}
	E{H_i} = \sum\limits_{j = 1}^V {E{I_j} \cdot w_{ij}^{'}}
\end{align}$$
{% endraw %}
