---
layout: post
title: Giải thích chi tiết về mạng Long Short-Term Memory (LSTM)
description: Mạng LSTM được thiết kế để giải quyết các bài toán về phụ thuộc xa (long-term dependencies) trong mạng RNN do bị ảnh hưởng bởi vấn đề gradient biến mất.
excerpt: Mạng LSTM là một phiên bản mở rộng của mạng RNN, được đề xuất vào năm 1997 bởi Sepp Hochreiter và Jürgen Schmidhuber. LSTM được thiết kế để giải quyết các bài toán về phụ thuộc xa (long-term dependencies) trong mạng RNN do bị ảnh hưởng bởi vấn đề gradient biến mất.
keywords: LSTM, mạng LSTM, mạng nơ-ron LSTM, mạng Long Short-Term Memory, mạng nơ-ron hồi quy LSTM, LSTM neural network, Long Short Term Memory, mạng RNN, học sâu, deep learning
author: Nguyễn Trường Long
---

### Giới thiệu về Recurrent Neural Network

Trước khi đi sâu vào giải thích chi tiết mạng [LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html), mình sẽ giới thiệu sơ qua về mạng nơ-ron hồi quy (Recurrent Neural Network - RNN). Đây là mạng nơ-ron nhân tạo được thiết kế cho việc xử lý các loại dữ liệu có dạng chuỗi tuần tự.

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/TypesofRNN.jpg" alt="Các loại mạng RNN chính">
  <figcaption><i>Hình 1: Các loại mạng RNN chính</i></figcaption>
</center>
</figure>

Dựa trên số lượng xử lý của chuỗi đầu vào và chuỗi đầu ra, người ta chia mạng RNN thành 4 loại chính:

- <strong><i>One to One RNN</i></strong>
- <strong><i>One to Many RNN</i></strong>
- <strong><i>Many to One RNN</i></strong>
- <strong><i>Many to Many RNN</i></strong>


Trong mạng RNN, trạng thái ẩn tại mỗi bước thời gian sẽ được tính toán dựa vào dữ liệu đầu vào tại bước thời gian tương ứng và các thông tin có được từ bước thời gian trước đó, tạo khả năng ghi nhớ các thông tin đã được tính toán ở những bước thời gian trước cho mạng. <i>Hình 2</i> biễu diễn kiến trúc của một mạng RNN cơ bản cho tác vụ ánh xạ một chuỗi đầu vào thành chuỗi đầu ra với cùng một độ dài khi được duỗi ra.

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/RNNUnfold.png" alt="Kiến trúc của một mạng RNN cơ bản khi được duỗi ra">
  <figcaption><i>Hình 2: Kiến trúc của một mạng RNN cơ bản khi được duỗi ra. Nguồn: Ian Goodfellow</i></figcaption>
</center>
</figure>

Trong <i>Hình 1</i>, xét tại mỗi bước thời gian $t$ theo chiều từ dưới lên trên, {% raw %}$${x^{\left( t \right)}}$${% endraw %} là giá trị đầu vào, {% raw %}$${h^{\left( t \right)}}$${% endraw %} là trạng thái ẩn, {% raw %}$${o^{\left( t \right)}}$${% endraw %} là giá trị đầu ra. $U$, $W$, $V$ là các ma trận trọng số của mạng RNN. $L$ là hàm tính mất mát giữa giá trị đầu ra {% raw %}$${o^{\left( t \right)}}$${% endraw %} từ mạng RNN và giá trị đầu ra chuẩn {% raw %}$${y^{\left( t \right)}}$${% endraw %} từ tập dữ liệu.


Đi sâu vào kiến trúc chi tiết hơn, chúng ta xem các vector {% raw %}$${x^{\left( 1 \right)}},{x^{\left( 2 \right)}},...,{x^{\left( \tau  \right)}}$${% endraw %} đại diện cho các phần tử trong chuỗi dữ liệu đầu vào, tại mỗi bước thời gian $t$, mạng RNN nhận lần lượt từng vector $x^{(t)}$ và thực hiện những tính toán để ánh xạ thành chuỗi đầu ra được mô tả bởi các phương trình sau:

{% raw %}$$
\begin{align}
&{h^{\left( t \right)}} = \tanh \left( {U{x^{\left( t \right)}} + W{h^{\left( {t - 1} \right)}} + b} \right)\\
&{o^{\left( t \right)}} = V{h^{\left( t \right)}} + c\\
&\hat{y}^{(t)} = {\rm{softmax}}\left( {{o^{\left( t \right)}}} \right)\\
\end{align}
$${% endraw %}

Trong đó:
- $x^{(t)}$: Giá trị đầu vào tại bước thời gian $t$
- $h^{(t)}$: Trạng thái ẩn tại bước thời gian $t$
- $o^{(t)}$: Giá trị đầu ra tại bước thời gian $t$
- $\hat{y}^{(t)}$: Vector xác suất đã chuẩn hóa qua hàm softmax tại bước thời gian $t$
- $U$, $V$, $W$: Các ma trận trọng số trong mạng RNN tương ứng với các kết nối theo chiều lần lượt là từ đầu vào đến trạng thái ẩn, từ trạng thái ẩn đến đầu ra và từ trạng thái ẩn đến trạng thái ẩn
- $b$, $c$: Độ lệch (bias)

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/IllustrationofRNN.png" alt="Kiến trúc chi tiết của một mạng RNN tại mỗi bước thời gian">
  <figcaption><i>Hình 3: Kiến trúc chi tiết của một mạng RNN tại mỗi bước thời gian. Nguồn: Nikhil Ketkar</i></figcaption>
</center>
</figure>

### Các vấn đề về gradient trong quá trình huấn luyện

Gradient biến mất (Vanishing Gradient Problem) và gradient bùng nổ (Exploding Gradient Problem) là những vấn đề gặp phải khi sử dụng các kỹ thuật tối ưu hóa trọng số dựa trên gradient để huấn luyện mạng nơ-ron. Các vấn đề này thường gặp phải do việc lựa chọn các hàm kích hoạt không hợp lý hoặc số lượng các lớp ẩn của mạng quá lớn. Đặc biệt, các vấn đề này thường hay xuất hiện trong quá trình huấn luyện các mạng nơ-ron hồi quy. Trong thuật toán BPTT, khi chúng ta càng quay lùi về các bước thời gian trước đó thì các giá trị gradient càng giảm dần, điều này làm giảm tốc độ hội tụ của các trọng số do sự thay đổi hầu như rất nhỏ. Trong một số trường hợp khác, các gradient có giá trị rất lớn khiến cho quá trình cập nhật các trọng số bị phân kỳ và vấn đề này được gọi là gradient bùng nổ. Các vấn đề về gradient biến mất thường được quan tâm hơn vấn đề gradient bùng nổ do vấn đề gradient biến mất khó có thể được nhận biết trong khi gradient bùng nổ có thể dễ dàng quan sát và nhận biết hơn. Có nhiều nghiên cứu đề xuất các giải pháp để giải quyết những vấn đề này như lựa chọn hàm kích hoạt hợp lý, thiết lập các kích thước cho mạng hợp lý hoặc khởi tạo các trọng số ban đầu phù hợp khi huấn luyện. Một trong các giải pháp cụ thể có thể chỉ ra là thuật toán Truncated BPTT, một biến thể cải tiến của BPTT được áp dụng trong quá trình huấn luyện mạng nơ-ron hồi quy trên các chuỗi dài. Ngoài ra, cơ chế của [mạng LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html) được đề xuất đã khắc phục được các vấn đề này sẽ được giới thiệu trong phần tiếp theo.

Mạng RNN bị ảnh hưởng bởi khả năng ghi nhớ ngắn hạn (short-term memory). Nếu dữ liệu đầu vào là một chuỗi trình tự dài, mạng RNN sẽ gặp khó khăn trong việc chuyển tải thông tin từ các bước thời gian đầu tiên đến các bước sau đó. Ví dụ trong bài toán phân loại văn bản, nếu chúng ta đang cố gắng xử lý một đoạn văn bản dài để thực hiện phân loại, mạng RNN có thể bỏ sót nhiều thông tin quan trọng ngay từ những bước đầu.

### Cơ chế hoạt động của mạng LSTM

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/LSTMstepbystep.gif" alt="Minh hoạ quá trình xử lý dữ liệu của mạng LSTM">
  <figcaption><i>Hình 4: Minh hoạ quá trình xử lý dữ liệu của mạng LSTM</i></figcaption>
</center>
</figure>

[LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html) là một phiên bản mở rộng của mạng RNN, được đề xuất vào năm 1997 bởi Sepp Hochreiter và Jürgen Schmidhuber. [LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html) được thiết kế để giải quyết các bài toán về phụ thuộc xa (long-term dependencies) trong mạng RNN do bị ảnh hưởng bởi vấn đề gradient biến mất.

Giả sử khi xem một bộ phim dài tập, chúng ta ghi nhớ bối cảnh phim đã diễn ra ở những tập trước đó, kết hợp xử lý với thông tin của tập phim hiện tại hoặc khi đọc sách, chúng ta ghi nhớ điều gì đã xảy ra ở chương trước, kết hợp thành mạch thông tin để hiểu và tiếp thu cho nội dung hiện tại. Tương tự như vậy, khi các mạng RNN hoạt động, thông tin trước đó được ghi nhớ và sử dụng lại để xử lý cho đầu vào hiện tại. Tuy nhiên thì mạng RNN không thể ghi nhớ thông tin ở các bước có khoảng cách khá xa trước đó do vấn đề gradient biến mất. Do đó những phần tử đầu tiên trong chuỗi đầu vào không có nhiều ảnh hưởng đến các kết quả tính toán dự đoán phần tử cho chuỗi đầu ra trong các bước sau. [Mạng LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html) với các kết nối phản hồi (feedback connection) giúp khắc phục nhược điểm này.

<figure class="image">
<center>
  <img src="https://nguyentruonglong.net/images/LSTMCell.png" alt="Sơ đồ biểu diễn kiến trúc bên trong của một tế bào LSTM">
  <figcaption><i>Hình 5: Sơ đồ biểu diễn kiến trúc bên trong của một tế bào LSTM</i></figcaption>
</center>
</figure>

[Mạng LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html) có thể bao gồm nhiều tế bào [LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html) (LSTM memory cell) liên kết với nhau và kiến trúc cụ thể của mỗi tế bào được biểu diễn như trong <i>Hình 2</i>. Ý tưởng của [LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html) là bổ sung thêm trạng thái bên trong tế bào (cell internal state) {% raw %}$$s_t$${% endraw %} và ba cổng sàng lọc các thông tin đầu vào và đầu ra cho tế bào bao gồm forget gate $${f_t}$$, input gate $${i_t}$$ và output gate $${o_t}$$. Tại mỗi bước thời gian $t$, các cổng đều lần lượt nhận giá trị đầu vào ${x_t}$ (đại diện cho một phần tử trong chuỗi đầu vào) và giá trị $ {h_{t - 1}} $ có được từ đầu ra của memory cell từ bước thời gian trước đó $t-1$. Các cổng đều đóng vai trò có nhiệm vụ sàng lọc thông tin với mỗi mục đích khác nhau:

- <strong><i>Forget gate</i></strong>: Có nhiệm vụ loại bỏ những thông tin không cần thiết nhận được khỏi cell internal state
- <strong><i>Input gate</i></strong>: Có nhiệm vụ chọn lọc những thông tin cần thiết nào được thêm vào cell internal state
- <strong><i>Output gate</i></strong>: Có nhiệm vụ xác định những thông tin nào từ cell internal state được sử dụng như đầu ra

Trước khi trình bày các phương trình mô tả cơ chế hoạt động bên trong của một tế bào [LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html), chúng ta sẽ thống nhất quy ước một số ký hiệu được sử dụng sau đây:
- ${x_{t}}$ là vector đầu vào tại mỗi bước thời gian $t$

- {% raw %}$${W_{f,x}},{W_{f,h}},{W_{\mathop s\limits^ \sim  ,x}},{W_{\mathop s\limits^ \sim  ,h}},{W_{i,x}},{W_{i,h}},{W_{o,x}},{W_{o,h}}$${% endraw %} là các ma trận trọng số trong mỗi tế bào [LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html).

- {% raw %}$${b_f},{b_{\mathop s\limits^ \sim  }},{b_i},{b_o}$${% endraw %} là các vector bias.

- {% raw %}$${f_t},{i_t},{o_t}$${% endraw %} lần lượt chứa các giá trị kích hoạt lần lượt cho các cổng forget gate, input gate và output gate tương ứng.

- {% raw %}$${s_t},\mathop s\limits^ \sim  $${% endraw %} lần lượt là các vector đại diện cho cell internal state và candidate value.

- ${h_{t}}$ là giá trị đầu ra của tế bào [LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html).

Trong quá trình lan truyền xuôi (forward pass), cell internal state $${s_t}$$ và giá trị đầu ra ${h_{t}}$ được tính như sau:

- Ở bước đầu tiên, tế bào [LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html) quyết định những thông tin nào cần được loại bỏ từ cell internal state ở bước thời gian trước đó $${s_{t - 1}}$$. Activation value $${f_{t}}$$ của forget gate tại bước thời gian $t$ được tính dựa trên giá trị đầu vào hiện tại $${x_{t}}$$, giá trị đầu ra $${h_{t-1}}$$ từ tế bào [LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html) ở bước trước đó và bias $${b_f}$$ của forget gate. Hàm sigmoid function biến đổi tất cả activation value về miền có giá trị trong khoảng từ $0$ (hoàn toàn quên) và $1$ (hoàn toàn ghi nhớ):

	{% raw %}
	$$\begin{equation}
	{f_t} = \sigma \left( {{W_{f,x}}{x_t} + {W_{f,h}}{h_{t - 1}} + {b_f}} \right)
	\end{equation}
	$${% endraw %}

- Ở bước thứ hai, tế bào [LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html) quyết định những thông tin nào cần được thêm vào cell internal state $${s_{t}}$$. Bước này bao gồm hai quá trình tính toán đối với {% raw %}$$\mathop {{s_t}}\limits^ \sim  $$ và $${f_{t}}$${% endraw %}. Candidate value {% raw %}$$\mathop {{s_t}}\limits^ \sim  $${% endraw %} biểu diễn những thông tin tiềm năng cần được thêm vào cell internal state được tính như sau:

	{% raw %}
	$$\begin{equation}
	\mathop {{s_t}}\limits^ \sim   = \tanh \left( {{W_{\mathop s\limits^ \sim  ,x}}{x_t} + {W_{\mathop s\limits^ \sim  ,h}}{h_{t - 1}} + {b_{\mathop s\limits^ \sim  }}} \right)
	\end{equation}
	$${% endraw %}

	Activation value $${i_t}$$ của input gate theo đó cũng được tính như sau:

	{% raw %}
	$$\begin{equation}
	{i_t} = \tanh \left( {{W_{i,x}}{x_t} + {W_{i,h}}{h_{t - 1}} + {b_i}} \right)
	\end{equation}
	$${% endraw %}

- Ở bước thứ ba, giá trị mới của cell internal state $${s_{t}}$$ được tính dựa trên kết quả tính toán thu được từ các bước trước với phép nhân Hadamard theo từng phần tử (Hadamard product) được ký hiệu bằng $$ \circ $$:

	{% raw %}
	$$\begin{equation}
	{s_t} = {f_t} \circ {s_{t - 1}} + {i_t} \circ \mathop {{s_t}}\limits^ \sim
	\end{equation}
	$${% endraw %}

- Ở bước cuối cùng, giá trị đầu ra $${h_{t}}$$ của tế bào [LSTM](https://nguyentruonglong.net/giai-thich-chi-tiet-ve-mang-long-short-term-memory-lstm.html) được tính toán dựa theo hai phương trình sau:

	{% raw %}
	$$\begin{equation}
	{o_t} = \sigma \left( {{W_{o,x}}{x_t} + {W_{o,h}}{h_{t - 1}} + {b_o}} \right)
	\end{equation}
	$${% endraw %}

	{% raw %}
	$$\begin{equation}
	{h_t} = {o_t} \circ \tanh \left( {{s_t}} \right)
	\end{equation}
	$${% endraw %}

### Tài liệu tham khảo

* <a href="https://towardsdatascience.com/illustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21" target="_blank">https://towardsdatascience.com/illustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21</a>
* <a href="https://towardsdatascience.com/lstm-networks-a-detailed-explanation-8fae6aefc7f9" target="_blank">https://towardsdatascience.com/lstm-networks-a-detailed-explanation-8fae6aefc7f9</a>
* <a href="https://iq.opengenus.org/types-of-rnn" target="_blank">https://iq.opengenus.org/types-of-rnn</a>


<!--
{% raw %}
$$\begin{equation}
4hi + 4h + 4{h^2} = 4\left( {hi + h + {h^2}} \right) = 4\left( {h\left( {i + 1} \right) + {h^2}} \right)
\end{equation}
$${% endraw %}

- Forget gate: Có nhiệm vụ loại bỏ những thông tin không cần thiết nhận được khỏi cell internal state và có phương trình như sau:

	{% raw %}
	$$\begin{equation}
	f^{(t)}_{i} = \sigma \Bigg( \sum_{j} U^{f}_{i,j}x^{(t)}_{j} + \sum_{j} W^{f}_{i,j}h^{(t-1)}_{j} + b^{f}_{i} \Bigg)
	\end{equation}$$
	{% endraw %}

	Trong đó, {% raw %}$$f_i^{\left( t \right)}$${% endraw %} là forget gate của tế bào $i$ tại bước thời gian $t$, vector $x^{(t)}$ là giá trị đầu vào tại bước thời gian $t$, các ma trận {% raw %}$${U^f},\,{W^f},\,{b^f}$${% endraw %} lần lượt là ma trận trọng số đầu vào, ma trận trọng số hồi quy và bias tương ứng cho forget gate. Hàm kích hoạt là hàm logistic sigmoid trả về các giá trị gần $1$ cho thông tin cần lưu giữ và gần $0$ cho thông tin cần loại bỏ.
	
- Input gate: Có nhiệm vụ chọn lọc những thông tin đầu vào nào cần được cập nhật:

	{% raw %}
	$$\begin{equation}
		g^{(t)}_{i} = \sigma \Bigg( \sum_{j} U^{g}_{i,j}x^{(t)}_{j} + \sum_{j} W^{g}_{i,j}h^{(t-1)}_{j} + b^{g}_{i} \Bigg)
	\end{equation}$$
	{% endraw %}

	Trạng thái bên trong tế bào đóng vai trò như một bộ nhớ của mạng LSTM xuyên suốt qua các bước thời gian theo đó cũng được cập nhật như sau:

	{% raw %}
	$$\begin{equation}
	s^{(t)}_{i} = f^{(t)}_{i}s^{(t-1)}_{i} + g^{(t)}_{i}\sigma \Bigg( \sum_{j} U_{i,j}x^{(t)}_{j} + \sum_{j} W_{i,j}h^{(t-1)}_{j} + b_{i} \Bigg)
	\end{equation}$$
	{% endraw %}

- Output gate: Có nhiệm vụ sàng lọc kiểm soát những thông tin cho đầu ra:

	{% raw %}
	$$\begin{equation}
		q^{(t)}_{i} = \sigma \Bigg( \sum_{j} U^{o}_{i,j}x^{(t)}_{j} + \sum_{j} W^{o}_{i,j}h^{(t-1)}_{j} + b^{o}_{i} \Bigg)
	\end{equation}$$
	{% endraw %}

	Trong đó, {% raw %}$${U^o},\,{W^o},\,{b^o}$${% endraw %} là các ma trận trọng số đầu vào, ma trận trọng số hồi quy và bias tương ứng. Cuối cùng, giá trị đầu ra {% raw %}$$h_i^{\left( t \right)}$${% endraw %} của tế bào LSTM được tính như sau:

	{% raw %}
	$$\begin{equation}
			h_i^{\left( t \right)} = \tanh \left( {s_i^{\left( t \right)}} \right)q_i^{\left( t \right)}
	\end{equation}$$
	{% endraw %}

LSTM đã được chứng minh rằng có khả năng giải quyết bài toán phụ thuộc xa tốt hơn các mạng RNN cơ bản có kiến trúc đơn giản hơn. Từ khi ra đời cho đến nay, LSTM đã trở nên nổi tiếng và đạt được những thành tựu tuyệt vời trong nhiều lĩnh vực.
-->
