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
[Thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) là một phương pháp lan truyền ngược (reverse-mode autodiff) được áp dụng trong [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html), giúp tính toán các đạo hàm cần thiết để tối ưu hóa các tham số trong mô hình.

Ý tưởng đầu tiên về [thuật toán Backpropagation](https://nguyentruonglong.net/giai-thich-chi-tiet-thuat-toan-backpropagation.html) được đề xuất bởi Paul Werbos vào năm 1974 trong bài "Beyond Regression: New Tools for Prediction and Analysis in the Behavioral Sciences". Sau đó, David Rumelhart, Geoffrey Hinton và Ronald Williams phổ biến rộng rãi thông qua bài "Learning representations by back-propagating errors" (1986), biến backprop thành phương pháp trung tâm để huấn luyện [mạng nơ-ron nhân tạo](https://nguyentruonglong.net/ly-thuyet-ve-mang-no-ron-nhan-tao-artificial-neural-network-ann.html).

Kể từ đó, backprop được sử dụng rộng rãi trong machine learning và deep learning. Dù vậy, mô hình có thể gặp hiện tượng **vanishing/exploding gradient**, khiến huấn luyện khó khăn. Vì thế có nhiều cải tiến/biến thể và kỹ thuật hỗ trợ:
 - *Weight Decay (L2 regularization)*: thêm hạng phạt vào hàm chi phí để giảm độ lớn trọng số, giúp giảm overfitting.
 - *Batch Normalization*: chuẩn hoá kích hoạt theo mini-batch, giúp huấn luyện nhanh và ổn định hơn.
 - *Adaptive Moment Estimation (Adam)*: kết hợp momentum và adaptive learning rate để thích nghi theo từng tham số.
 - *Stochastic Gradient Descent with Momentum*: thêm quán tính để giảm dao động, cải thiện hội tụ.
 - *Nesterov Accelerated Gradient*: nhìn “trước” theo hướng momentum để tinh chỉnh bước cập nhật, hội tụ tốt hơn.

---
### Ý tưởng của thuật toán Backpropagation
Backprop được dùng để tính đạo hàm của hàm mất mát theo các tham số khi áp dụng [gradient descent](https://nguyentruonglong.net/thuat-toan-gradient-descent.html). Số lượng tham số có thể rất lớn, nếu áp dụng trực tiếp quy tắc đạo hàm sẽ không hiệu quả. Backprop dùng **quy tắc chuỗi** để lan truyền gradient từ đầu ra về đầu vào qua từng lớp, nhờ đó tính gradient **hiệu quả** cho tất cả trọng số/bias.

Quy tắc chuỗi cho hàm hợp:
{% raw %}
$$
f(x)=g(h(x)) \quad\Rightarrow\quad \frac{df}{dx}=\frac{dg}{dh}\cdot\frac{dh}{dx}.
$$
{% endraw %}

**Giải thích chi tiết**: Hãy tưởng tượng bạn đang điều chỉnh công thức nấu một món súp. Hàm hợp \( f(x) = g(h(x)) \) giống như việc bạn nêm gia vị (h(x)) rồi nấu súp (g). Nếu món súp quá mặn, bạn cần biết cách điều chỉnh lượng muối (x). Quy tắc chuỗi giúp bạn hiểu rằng: để giảm độ mặn của súp (df/dx), bạn cần xem độ mặn thay đổi thế nào khi thêm gia vị (dg/dh) và gia vị thay đổi thế nào khi thêm muối (dh/dx). Trong mạng nơ-ron, toàn bộ mô hình là một hàm hợp nhiều lớp, giống như nhiều bước nấu ăn liên tiếp. Áp dụng quy tắc chuỗi từ lớp cuối (đầu ra, tức món súp) về lớp đầu (đầu vào, tức nguyên liệu), bạn tính được cách điều chỉnh từng tham số để món súp ngon hơn.

---
### Quy trình 2 pha của Backpropagation
 - **Pha feedforward (lan truyền tiến)**: tính đầu ra của từng lớp để nhận dự đoán và giá trị mất mát. Ví dụ, bạn nhập nguyên liệu (đầu vào), qua các bước chế biến (các lớp ẩn), và cuối cùng ra món ăn (đầu ra).
 - **Pha backpropagation (lan truyền ngược)**: dùng quy tắc chuỗi để tính gradient của mất mát theo từng tham số, từ lớp cuối cùng ngược về lớp đầu. Như việc bạn nếm món ăn, thấy không ngon, rồi quay ngược lại từng bước chế biến để tìm ra cần điều chỉnh gì.

---
### Hàm mất mát và hàm chi phí
Với một mẫu, dùng **mất mát bình phương**:
{% raw %}
$$
L(y,\hat{y})=\frac{1}{2}\,(y-\hat{y})^2.
$$
{% endraw %}

**Giải thích chi tiết**: Hàm mất mát \( L(y, \hat{y}) \) đo lường mức độ sai lệch giữa giá trị dự đoán (\( \hat{y} \)) và giá trị thực (\( y \)). Công thức \( \frac{1}{2}(y - \hat{y})^2 \) được chọn vì nó đơn giản và có đạo hàm dễ tính. Hệ số \( \frac{1}{2} \) giúp đạo hàm không có số 2, làm tính toán gọn hơn. Ví dụ, nếu bạn dự đoán nhiệt độ là 25°C (\( \hat{y} \)) nhưng thực tế là 30°C (\( y \)), mất mát là \( \frac{1}{2}(30 - 25)^2 = \frac{1}{2} \cdot 25 = 12.5 \). Mất mát này giống như điểm số phạt cho dự đoán sai, giúp bạn biết cần điều chỉnh mô hình thế nào.

Với tập huấn luyện kích thước {% raw %}$m${% endraw %}, **hàm chi phí** (dùng trung bình mini-batch hay toàn bộ):
{% raw %}
$$
J(W,b)=\frac{1}{m}\sum_{i=1}^{m} L\!\left(y^{(i)},\hat{y}^{(i)}\right).
$$
{% endraw %}

**Giải thích chi tiết**: Hàm chi phí \( J(W, b) \) là trung bình của mất mát trên tất cả mẫu trong tập huấn luyện. Nếu bạn có 100 mẫu, bạn tính mất mát cho từng mẫu (như ví dụ nhiệt độ ở trên), rồi lấy trung bình để có cái nhìn tổng quát về hiệu suất mô hình. Ví dụ, nếu bạn dự đoán nhiệt độ cho 3 ngày, với mất mát lần lượt là 12.5, 8.0, và 15.0, thì hàm chi phí là \( \frac{12.5 + 8.0 + 15.0}{3} \approx 11.83 \). Con số này giúp bạn biết mô hình sai lệch trung bình bao nhiêu, từ đó điều chỉnh trọng số \( W \) và bias \( b \).

---
### Kiến trúc ví dụ và ký hiệu
- **Đầu vào**: {% raw %}$\mathbf{x}=[x_1,x_2]^\top=(0.2,\,0.4)^\top${% endraw %}.
- **Lớp ẩn** (2 nơ-ron, sigmoid):
  {% raw %}$\mathbf{z}^{[1]}=W^{[1]}\mathbf{x}+ \mathbf{b}^{[1]}${% endraw %},
  {% raw %}$\mathbf{a}^{[1]}=\sigma\!\bigl(\mathbf{z}^{[1]}\bigr)${% endraw %}.
- **Lớp ra** (1 nơ-ron, sigmoid):
  {% raw %}$z^{[2]}=W^{[2]}\mathbf{a}^{[1]}+b^{[2]},\quad \hat{y}=a^{[2]}=\sigma\!\bigl(z^{[2]}\bigr)${% endraw %}.
- **Hàm kích hoạt** sigmoid: {% raw %}$\sigma(z)=\frac{1}{1+e^{-z}},\quad \sigma'(z)=\sigma(z)\,(1-\sigma(z))${% endraw %}.

**Giải thích chi tiết**: Mạng nơ-ron này giống như một dây chuyền sản xuất nhỏ. Đầu vào \( \mathbf{x} = [0.2, 0.4]^\top \) là nguyên liệu thô (ví dụ, đặc điểm của một hình ảnh). Lớp ẩn (2 nơ-ron) giống như hai công nhân chế biến nguyên liệu này, sử dụng trọng số \( W^{[1]} \) và bias \( \mathbf{b}^{[1]} \) để tạo ra giá trị trung gian \( \mathbf{z}^{[1]} \), rồi áp dụng hàm sigmoid để “nén” giá trị vào khoảng [0,1], cho ra \( \mathbf{a}^{[1]} \). Lớp ra (1 nơ-ron) tổng hợp kết quả từ lớp ẩn, thêm bias \( b^{[2]} \), và dùng sigmoid để đưa ra dự đoán cuối cùng \( \hat{y} \). Hàm sigmoid \( \sigma(z) = \frac{1}{1+e^{-z}} \) giống như một bộ lọc, chuyển mọi giá trị thành số giữa 0 và 1, hữu ích cho bài toán phân loại nhị phân (ví dụ, dự đoán “mèo” hay “không phải mèo”).

Trọng số/bias:
{% raw %}
$$
W^{[1]}=
\begin{bmatrix}
0.10 & -0.20\\
0.30 & 0.25
\end{bmatrix},\quad
\mathbf{b}^{[1]}=
\begin{bmatrix}
0.01\\
-0.02
\end{bmatrix},\quad
W^{[2]}=
\begin{bmatrix}
0.80 & 0.90
\end{bmatrix},\quad
b^{[2]}=0.10.
$$
{% endraw %}
Mục tiêu: {% raw %}$y=1.0${% endraw %}.

**Giải thích chi tiết**: Trọng số \( W^{[1]} \) và bias \( \mathbf{b}^{[1]} \) là “công thức” mà lớp ẩn dùng để xử lý đầu vào. Ví dụ, \( W^{[1]} \) giống như cách công nhân quyết định trộn bao nhiêu nguyên liệu \( x_1 \) và \( x_2 \). Bias \( \mathbf{b}^{[1]} \) là một điều chỉnh thêm, như thêm một chút muối cố định vào món ăn. Tương tự, \( W^{[2]} \) và \( b^{[2]} \) là công thức cho lớp ra. Mục tiêu \( y = 1.0 \) nghĩa là bạn muốn mô hình dự đoán chính xác giá trị 1 (ví dụ, hình ảnh là “mèo”).

#### Minh họa kiến trúc mạng cho ví dụ
<pre class="mermaid">
graph TD
  X1([x1=0.2]) --> H1((Hidden 1))
  X2([x2=0.4]) --> H1
  X1 --> H2((Hidden 2))
  X2 --> H2
  H1 --> Y((Output ŷ))
  H2 --> Y
  subgraph InputLayer
    X1
    X2
  end
  subgraph HiddenLayer
    H1
    H2
  end
  subgraph OutputLayer
    Y
  end
</pre>

**Giải thích chi tiết**: Hình minh họa giống như sơ đồ dây chuyền sản xuất. Hai đầu vào \( x_1 = 0.2 \), \( x_2 = 0.4 \) đi vào hai nơ-ron ẩn (Hidden 1, Hidden 2), mỗi nơ-ron xử lý đầu vào bằng trọng số và bias riêng, rồi gửi kết quả đến nơ-ron đầu ra, tạo ra dự đoán \( \hat{y} \). Đây là mô hình mạng nơ-ron đơn giản với một lớp ẩn.

---
### Bước 1: Pha Feedforward
{% raw %}
$$
\begin{aligned}
z^{[1]}_1 &= 0.10\cdot 0.2 + (-0.20)\cdot 0.4 + 0.01 = -0.05,\\
z^{[1]}_2 &= 0.30\cdot 0.2 + \phantom{(-)}0.25\cdot 0.4 - 0.02 = 0.14,\\[2pt]
a^{[1]}_1 &= \sigma(-0.05)=0.487503,\\
a^{[1]}_2 &= \sigma(0.14)=0.534943.
\end{aligned}
$$
{% endraw %}
Lớp ra:
{% raw %}
$$
\begin{aligned}
z^{[2]} &= 0.80\cdot 0.487503 + 0.90\cdot 0.534943 + 0.10 = 0.971451,\\
\hat{y}=a^{[2]} &= \sigma(0.971451)=0.725409.
\end{aligned}
$$
{% endraw %}
Mất mát:
{% raw %}
$$
L=\frac{1}{2}(1.0-0.725409)^2=0.037700.
$$
{% endraw %}

**Giải thích chi tiết**: Trong pha feedforward, bạn cho nguyên liệu (đầu vào) đi qua dây chuyền để tạo ra sản phẩm (đầu ra). Đầu tiên, tại lớp ẩn, nơ-ron 1 tính \( z^{[1]}_1 = 0.10 \cdot 0.2 + (-0.20) \cdot 0.4 + 0.01 = -0.05 \), như công nhân trộn nguyên liệu với tỉ lệ nhất định. Sau đó, áp dụng sigmoid để được \( a^{[1]}_1 = \sigma(-0.05) \approx 0.487503 \), giống như “nén” kết quả để dễ xử lý. Tương tự cho nơ-ron 2. Tại lớp ra, kết quả từ lớp ẩn được kết hợp: \( z^{[2]} = 0.80 \cdot 0.487503 + 0.90 \cdot 0.534943 + 0.10 \approx 0.971451 \), rồi qua sigmoid để được \( \hat{y} \approx 0.725409 \). Cuối cùng, mất mát \( L = \frac{1}{2}(1.0 - 0.725409)^2 \approx 0.037700 \) cho biết dự đoán sai lệch so với mục tiêu \( y = 1.0 \).

---
### Bước 2: Tính độ lỗi tại lớp ra
{% raw %}
$$
\delta^{[2]}=(\hat{y}-y)\,\hat{y}(1-\hat{y})
=(0.725409-1.0)\times 0.725409\times 0.274591
=-0.054696.
$$
{% endraw %}

**Giải thích chi tiết**: Độ lỗi \( \delta^{[2]} \) cho biết mức độ sai lệch của dự đoán tại lớp ra. Công thức \( (\hat{y} - y) \) là sai số (0.725409 - 1.0 = -0.274591), tức dự đoán thấp hơn mục tiêu. Nhân với \( \hat{y}(1 - \hat{y}) = \sigma'(z^{[2]}) \), đạo hàm của sigmoid, để tính ảnh hưởng của \( z^{[2]} \) lên sai số. Kết quả \( \delta^{[2]} \approx -0.054696 \) giống như tín hiệu báo rằng đầu ra sai bao nhiêu và cần điều chỉnh thế nào. Ví dụ, nếu món súp quá nhạt, \( \delta^{[2]} \) cho bạn biết cần thêm bao nhiêu muối.

---
### Bước 3: Gradient tại lớp ra
{% raw %}
$$
\frac{\partial L}{\partial W^{[2]}}=\delta^{[2]}\,\bigl(\mathbf{a}^{[1]}\bigr)^\top,\qquad
\frac{\partial L}{\partial b^{[2]}}=\delta^{[2]}.
$$
{% endraw %}
Kết quả:
{% raw %}
$$
\frac{\partial L}{\partial W^{[2]}}
=\begin{bmatrix}
-0.026665 &\ -0.029259
\end{bmatrix},\qquad
\frac{\partial L}{\partial b^{[2]}}=-0.054696.
$$
{% endraw %}

**Giải thích chi tiết**: Gradient \( \frac{\partial L}{\partial W^{[2]}} \) cho biết cần điều chỉnh trọng số \( W^{[2]} \) bao nhiêu để giảm mất mát. Công thức \( \delta^{[2]} \cdot (\mathbf{a}^{[1]})^\top \) nhân độ lỗi với đầu vào của lớp ra (kích hoạt từ lớp ẩn). Ví dụ, \( \delta^{[2]} \cdot a^{[1]}_1 = -0.054696 \cdot 0.487503 \approx -0.026665 \), nghĩa là trọng số liên kết với \( a^{[1]}_1 \) cần điều chỉnh một chút. Gradient của bias \( \frac{\partial L}{\partial b^{[2]}} = \delta^{[2]} \approx -0.054696 \), vì bias không phụ thuộc vào đầu vào, chỉ lấy độ lỗi trực tiếp. Đây giống như quyết định thêm bao nhiêu muối cố định vào món súp.

---
### Bước 4: Lan truyền ngược về lớp ẩn
{% raw %}
$$
\delta^{[1]}_j=\bigl(W^{[2]}_j\,\delta^{[2]}\bigr)\; a^{[1]}_j(1-a^{[1]}_j).
$$
{% endraw %}
Kết quả:
{% raw %}
$$
\delta^{[1]}_1=-0.010932,\qquad
\delta^{[1]}_2=-0.012247.
$$
{% endraw %}

**Giải thích chi tiết**: Bước này lan truyền độ lỗi từ lớp ra về lớp ẩn. Công thức \( W^{[2]}_j \cdot \delta^{[2]} \) phân bổ lỗi từ lớp ra cho nơ-ron ẩn, vì \( W^{[2]}_j \) là trọng số kết nối nơ-ron ẩn \( j \) với lớp ra. Nhân với \( a^{[1]}_j (1 - a^{[1]}_j) \), đạo hàm sigmoid, để tính ảnh hưởng của nơ-ron ẩn lên lỗi. Ví dụ, cho nơ-ron ẩn 1: \( \delta^{[1]}_1 = (0.80 \cdot -0.054696) \cdot 0.487503 \cdot (1 - 0.487503) \approx -0.010932 \). Đây giống như việc bạn quay lại công nhân chế biến, nói rằng món súp sai vì họ trộn sai nguyên liệu, và cần điều chỉnh thế nào.

---
### Bước 5: Gradient tại lớp ẩn
{% raw %}
$$
\frac{\partial L}{\partial W^{[1]}}=\boldsymbol{\delta}^{[1]}\, \mathbf{x}^\top,\qquad
\frac{\partial L}{\partial \mathbf{b}^{[1]}}=\boldsymbol{\delta}^{[1]}.
$$
{% endraw %}
Kết quả:
{% raw %}
$$
\frac{\partial L}{\partial W^{[1]}}=
\begin{bmatrix}
-0.002186 & -0.004373\\
-0.002449 & -0.004899
\end{bmatrix},\qquad
\frac{\partial L}{\partial \mathbf{b}^{[1]}}=
\begin{bmatrix}
-0.010932\\
-0.012247
\end{bmatrix}.
$$
{% endraw %}

**Giải thích chi tiết**: Gradient \( \frac{\partial L}{\partial W^{[1]}} \) tính cách điều chỉnh trọng số lớp ẩn. Nhân \( \boldsymbol{\delta}^{[1]} \) với \( \mathbf{x}^\top \) để biết đầu vào \( x_1, x_2 \) ảnh hưởng thế nào đến lỗi. Ví dụ, \( \delta^{[1]}_1 \cdot x_1 = -0.010932 \cdot 0.2 \approx -0.002186 \). Gradient của bias \( \frac{\partial L}{\partial \mathbf{b}^{[1]}} \) lấy trực tiếp \( \boldsymbol{\delta}^{[1]} \), vì bias không phụ thuộc vào đầu vào. Đây giống như việc bạn bảo công nhân điều chỉnh tỉ lệ trộn nguyên liệu và lượng muối cố định.

---
### Bước 6–9: Đạo hàm theo từng trọng số
- {% raw %}$\frac{\partial L}{\partial w_3}=\delta^{[1]}_1\,x_1=-0.002186${% endraw %}
- {% raw %}$\frac{\partial L}{\partial w_4}=\delta^{[1]}_1\,x_2=-0.004373${% endraw %}
- {% raw %}$\frac{\partial L}{\partial w_5}=\delta^{[1]}_2\,x_1=-0.002449${% endraw %}
- {% raw %}$\frac{\partial L}{\partial w_6}=\delta^{[1]}_2\,x_2=-0.004899${% endraw %}

**Giải thích chi tiết**: Các trọng số riêng lẻ \( w_3, w_4, w_5, w_6 \) trong \( W^{[1]} \) được tính gradient cụ thể. Ví dụ, \( w_3 \) là trọng số từ \( x_1 \) đến nơ-ron ẩn 1, nên gradient là \( \delta^{[1]}_1 \cdot x_1 \). Đây giống như việc bạn xác định chính xác công nhân nào cần điều chỉnh bao nhiêu nguyên liệu \( x_1 \) hay \( x_2 \).

---
### Bước 10: Cập nhật tham số
Với {% raw %}$\alpha=0.1${% endraw %}:
- Lớp ra:
{% raw %}
$$
W^{[2]} \leftarrow
\begin{bmatrix}
0.802666 & 0.902926
\end{bmatrix},\qquad
b^{[2]}\leftarrow 0.105470.
$$
{% endraw %}
- Lớp ẩn:
{% raw %}
$$
W^{[1]}=
\begin{bmatrix}
0.100219 & -0.199563\\
0.300245 & \phantom{-}0.250490
\end{bmatrix},\qquad
\mathbf{b}^{[1]}=
\begin{bmatrix}
0.011093\\
-0.018775
\end{bmatrix}.
$$
{% endraw %}

**Giải thích chi tiết**: Sau khi tính gradient, bạn cập nhật trọng số và bias bằng cách trừ đi gradient nhân với tốc độ học \( \alpha = 0.1 \). Công thức là \( W \leftarrow W - \alpha \cdot \frac{\partial L}{\partial W} \). Ví dụ, \( W^{[2]}_1 = 0.80 - 0.1 \cdot (-0.026665) \approx 0.802666 \). Đây giống như việc bạn điều chỉnh công thức nấu ăn dựa trên sai lầm trước đó, với \( \alpha \) quyết định bạn thay đổi mạnh hay nhẹ.

---
### Công thức tổng quát (vector hoá)
{% raw %}
$$
\mathbf{Z}^{[l]} = W^{[l]}\mathbf{A}^{[l-1]}+\mathbf{b}^{[l]},\quad
\mathbf{A}^{[l]}=g^{[l]}\!\bigl(\mathbf{Z}^{[l]}\bigr).
$$
$$
\boldsymbol{\delta}^{[L]}=\frac{\partial J}{\partial \mathbf{A}^{[L]}}\odot g'^{[L]}\!\bigl(\mathbf{Z}^{[L]}\bigr),\qquad
\boldsymbol{\delta}^{[l]}=\bigl(W^{[l+1]}\bigr)^\top \boldsymbol{\delta}^{[l+1]}\odot g'^{[l]}\!\bigl(\mathbf{Z}^{[l]}\bigr).
$$
$$
\frac{\partial J}{\partial W^{[l]}}=\frac{1}{m}\,\boldsymbol{\delta}^{[l]}\,\bigl(\mathbf{A}^{[l-1]}\bigr)^\top,\qquad
\frac{\partial J}{\partial \mathbf{b}^{[l]}}=\frac{1}{m}\,\sum_{i=1}^{m}\boldsymbol{\delta}^{[l](i)}.
$$
{% endraw %}

**Giải thích chi tiết**: Các công thức này tổng quát hóa backpropagation cho mạng nhiều lớp. \( \mathbf{Z}^{[l]} \) là giá trị trước kích hoạt tại lớp \( l \), như nguyên liệu thô trước khi chế biến. \( \mathbf{A}^{[l]} \) là giá trị sau kích hoạt, như nguyên liệu đã được nấu chín. Độ lỗi \( \boldsymbol{\delta}^{[L]} \) tại lớp cuối tính từ đạo hàm của hàm chi phí và đạo hàm hàm kích hoạt. Độ lỗi lan truyền ngược về lớp trước bằng \( (W^{[l+1]})^\top \boldsymbol{\delta}^{[l+1]} \), giống như phân bổ trách nhiệm lỗi ngược lại dây chuyền. Gradient của trọng số và bias được tính bằng cách nhân độ lỗi với đầu vào trước đó, trung bình trên \( m \) mẫu, như cách bạn tổng hợp sai lầm từ nhiều món ăn để điều chỉnh công thức.

---
### Ghi chú áp dụng thực tế
- Khởi tạo: Kỹ thuật Xavier/He giúp giảm vanishing/exploding gradient.
- Chuẩn hoá: Phương pháp BatchNorm tăng ổn định và tốc độ hội tụ.
- Tối ưu: Các biến thể SGD+Momentum, Nesterov, Adam thường được dùng.
- Ổn định: Có thể áp dụng Gradient clipping, chuẩn hoá dữ liệu, chọn batch size hợp lý.

---
### Tài liệu tham khảo
- Paul Werbos (1974) — *Beyond Regression: New Tools for Prediction and Analysis in the Behavioral Sciences*.
- Rumelhart, Hinton, Williams (1986) — *Learning representations by back-propagating errors*.
