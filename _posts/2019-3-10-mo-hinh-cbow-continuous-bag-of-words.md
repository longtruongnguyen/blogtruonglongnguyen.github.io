---
layout: post
title: Mô hình CBOW (Continuous Bag of Words)
description: Ý tưởng chính của mô hình CBOW là dự đoán từ mục tiêu dựa vào các từ ngữ cảnh xung quanh nó trong một phạm vi nhất định.
keywords: mô hình CBOW, Continuous Bag of Words, mô hình Word2Vec, nhúng từ CBOW
author: Nguyễn Trường Long
---

Ý tưởng chính của [mô hình CBOW](https://nguyentruonglong.net/mo-hinh-cbow-continuous-bag-of-words.html) là dự đoán từ mục tiêu dựa vào các từ ngữ cảnh xung quanh nó trong một phạm vi nhất định. Cho từ mục tiêu $${w_c}$$ tại vị trí $c$, khi đó đầu vào là các từ ngữ cảnh {% raw %}$$\left( {{w_{c - m}},...,{w_{c - 1}},{w_{c + 1}},...{w_{c + m}}} \right)$${% endraw %} xung quanh từ $${w_c}$$ trong phạm vi $$m$$.

<figure class="image">
  <img src="https://nguyentruonglong.net/images/CBOWInputOutput.png" alt="Ảnh minh họa đầu vào và đầu ra của mô hình CBOW">
  <figcaption><center><i>Ảnh minh họa đầu vào và đầu ra của mô hình CBOW trên câu văn bản "I have a big dog and horse" với $m = 1$</i></center></figcaption>
</figure>

[Mô hình CBOW](https://nguyentruonglong.net/mo-hinh-cbow-continuous-bag-of-words.html) tổng quát được thể hiện trong hình bên dưới với kích thước đầu vào gồm $C$ từ ngữ cảnh, $V$ là kích thước của tập từ vựng và hyperparameter $N$ là kích thước của hidden layer. Các unit thuộc các layer kế cận nhau được kết nối theo kiểu fully connected.

<figure class="image">
  <img src="https://nguyentruonglong.net/images/GeneralCBOW.png" alt="Ảnh minh họa cho mô hình CBOW ở dạng tổng quát">
  <figcaption><center><i>Ảnh minh họa cho mô hình CBOW ở dạng tổng quát</i></center></figcaption>
</figure>

Mỗi từ đầu vào ở vị trí thứ $k$ trong tập từ vựng được biểu diễn bằng một one-hot vector có dạng:
{% raw %}
$$\begin{align}
	{x^{\left( k \right)}} = \left[ {\begin{array}{*{20}{c}}
		{{x_1}}\\
		{{x_2}}\\
		\vdots \\
		{{x_k}}\\
		\vdots \\
		{{x_V}}
		\end{array}} \right]
\end{align}$$
{% endraw %}
Tương ứng với mỗi vector $${x^{\left( k \right)}}$$ chỉ có một phần tử $${x_k}$$ của nó có giá trị bằng 1 và giá trị của tất cả các phần tử còn lại đều bằng 0. Các trọng số giữa input layer và hidden layer cũng được biểu diễn thành ma trận $W$ kích thước $$V \times N$$ như sau:
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

Mỗi hàng của ma trận $W$ là một biểu diễn vector $${v_w}$$ có số chiều là $N$ tương ứng với một từ $w$ trong tập từ vựng. Ma trận h với kích thước $$N \times 1$$ có dạng như sau:
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
Mỗi phần tử của ma trận $h$ tương ứng với output của mỗi hidden layer unit. Activation function của các hidden layer unit đều là hàm tuyến tính {% raw %}$$\varphi \left( x \right) = x$${% endraw %}. Ta có:
{% raw %}
$$\begin{align}
	\begin{array}{l}
	{W^T}{x^{\left( k \right)}} = \left[ {\begin{array}{*{20}{c}}
		{{w_{11}}}&{{w_{21}}}& \cdots &{{w_{{\rm{V1}}}}}\\
		{{w_{12}}}&{{w_{22}}}& \cdots &{{w_{{\rm{V2}}}}}\\
		\vdots & \vdots & \ddots & \vdots \\
		{{w_{{\rm{1N}}}}}&{{w_{{\rm{2N}}}}}& \ldots &{{w_{{\rm{VN}}}}}
		\end{array}} \right]\left[ {\begin{array}{*{20}{c}}
		{{x_1}}\\
		{{x_2}}\\
		\vdots \\
		{{x_k}}\\
		\vdots \\
		{{x_V}}
		\end{array}} \right]\\
	= \left[ {\begin{array}{*{20}{c}}
		{{w_{{\rm{k}}1}}{x_k}}\\
		{{w_{{\rm{k}}2}}{x_k}}\\
		\vdots \\
		{{w_{{\rm{kN}}}}{x_k}}
		\end{array}} \right] = \left[ {\begin{array}{*{20}{c}}
		{{w_{{\rm{k}}1}}}\\
		{{w_{{\rm{k}}2}}}\\
		\vdots \\
		{{w_{{\rm{kN}}}}}
		\end{array}} \right] = W_{\left( {k, \cdot } \right)}^T = v_{{w_k}}^T
	\end{array}
\end{align}$$
{% endraw %}

Sử dụng kết quả này, ta tính được $h$ như sau:
{% raw %}
$$\begin{align}
&h = \frac{1}{C}{W^T}\left( {{x^{\left( 1 \right)}} + {x^{\left( 2 \right)}} + ... + {x^{\left( C \right)}}} \right)\\
&= \frac{1}{C}\left( {v_{{w_{I,1}}}^T + v_{{w_{I,2}}}^T + ... + v_{{w_{I,C}}}^T} \right)\\
&= \frac{1}{C}{\left( {{v_{{w_{I,1}}}} + {v_{{w_{I,2}}}} + ... + {v_{{w_{I,C}}}}} \right)^T}
\end{align}$$
{% endraw %}
Trong đó các one-hot vector {% raw %}$${x^{\left( 1 \right)}},...,{x^{\left( C \right)}}$${% endraw %} tương ứng lần lượt với các từ ngữ cảnh đầu vào {% raw %}$${{w_{I,1}},...,{w_{I,C}}}$${% endraw %} và {% raw %}$${{w_O}}$${% endraw %} là từ ở đầu ra của mô hình. Từ hidden layer đến  output layer là các trọng số được biểu diễn bằng một ma trận {% raw %}$${W^{'}} = \left\{ {w_{ij}^{'}} \right\}$${% endraw %} khác với kích thước {% raw %}$$N \times V$${% endraw %}. Chúng ta sẽ tính điểm số ${u_j}$ cho mỗi từ thứ $j$ trong tập từ vựng theo công thức sau:
{% raw %}
$$\begin{equation}
{u_j} = v{_{{w_j}}^{'}}^{T}h
\end{equation}$$
{% endraw %}
Trong đó {% raw %}$$v_{{w_j}}^{'}$${% endraw %} là cột thứ $j$ của ma trận {% raw %}$${W^{'}}$${% endraw %}. Điểm số ${u_j}$ chính là thước đo độ khớp giữa $C$ từ ngữ cảnh đầu vào cho trước và từ ${w_j}$. Chúng ta sẽ sử dụng hàm softmax để chuẩn hóa phân phối hậu nghiệm (posterior distribution) của mỗi từ trong tập từ vựng như sau:
{% raw %}
$$\begin{equation}
{p\left( {{w_O}|{w_{I,1}},...,{w_{I,C}}} \right)} = {y_j} = \frac{{\exp \left( {{u_j}} \right)}}{{\sum\limits_{{j^{'}} = 1}^V {\exp \left( {{u_{{j^{'}}}}} \right)} }}
\end{equation}$$
{% endraw %}
Trong đó {% raw %}$${y_j}$${% endraw %} cũng chính là output của unit thứ {% raw %}$$j$${% endraw %} trong output layer. Mục tiêu của quá trình huấn luyện là điều chỉnh các trọng số để cực đại hóa hàm phân phối bên trên đối với từ {% raw %}$${w_O}$${% endraw %} và các từ ngữ cảnh {% raw %}$${w_{I,1}},...,{w_{I,C}}$${% endraw %} cho trước:

{% raw %}
$$\begin{align}
	&\max \left( {p\left( {{w_O}|{w_{I,1}},...,{w_{I,C}}} \right)} \right) = \max \left( {\log \left( {p\left( {{w_O}|{w_{I,1}},...,{w_{I,C}}} \right)} \right)} \right)\\
	&= \min \left( { - \log \left( {p\left( {{w_O}|{w_{I,1}},...,{w_{I,C}}} \right)} \right)} \right)\\
	&= \min \left( E \right)
\end{align}$$
{% endraw %}
Trong đó $E$ là hàm lỗi cần được cực tiểu hóa và có công thức như sau:
{% raw %}
$$\begin{align}
&E =  - \log \left( {p\left( {{w_O}|{w_{I,1}},...,{w_{I,C}}} \right)} \right)\\
  &=  - {u_{{j^*}}} + \log \left( {\sum\limits_{{j^{'}} = 1}^V {\exp \left( {{u_{{j^{'}}}}} \right)} } \right)\\
  &=  - {v{_{{w_O}}^{'}}^T}h + \log \left( {\sum\limits_{{j^{'}} = 1}^V {\exp \left( {v{_{{w_j}}^{'}}^T}h \right)} } \right)
\end{align}$$
{% endraw %}
Trong đó ${j^*}$ là vị trí hiện có của từ đầu ra trong output layer. Phương trình cập nhật các trọng số từ hidden layer đến output layer:
{% raw %}
$$\begin{align}
v{_{{{w_j}}^{'}}^{\left( {new} \right)}} = v{_{{{w_j}}^{'}}^{\left( {old} \right)}} - \eta  \cdot \frac{{\partial E}}{{\partial {u_j}}} \cdot h \text{  với  } j = 1,2,...,V
\end{align}$$
{% endraw %}
Phương trình cập nhật các trọng số từ input layer đến hidden layer:
{% raw %}
$$\begin{align}
{v_{{w_c}}}^{\left( {new} \right)} = {v_{{w_c}}}^{\left( {old} \right)} - \frac{1}{C} \cdot \eta \cdot {\left( {\frac{{\partial E}}{{\partial {h_i}}}} \right)^T} \text{  với  } c = 1,2,...,C
\end{align}$$
{% endraw %}
Trong đó {% raw %}$${v_{{w_c}}}$${% endraw %} là input vector tương ứng với từ thứ $c$ trong $C$ từ ngữ cảnh đầu vào và $\eta$ là learning rate.
Sau khi quá trình huấn luyện hoàn tất, chúng ta thu được kết quả cuối cùng của ma trận $W$ và ma trận {% raw %}$$W^{'}$${% endraw %}. Tương ứng với mỗi từ ${w_j}$ trong tập từ vựng đều tồn tại {% raw %}$$v_{{w_j}}$${% endraw %} và {% raw %}$$v_{{w_j}}^{'}$${% endraw %} là hai vector khác nhau cùng đại diện cho nó. Vector {% raw %}$$v_{{w_j}}$${% endraw %} được gọi là input vector và tương ứng với hàng thứ $j$ trong ma trận $W$. Vector {% raw %}$$v_{{w_j}}^{'}$${% endraw %} được gọi là output vector và tương ứng với cột thứ $j$ trong ma trận {% raw %}$$W^{'}$${% endraw %}. Quá trình huấn luyện cho các input vector tốn ít chi phí hơn trong khi quá trình huấn luyện output vector tốn khá nhiều chi phí.
