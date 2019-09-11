---
layout: post
title: Giải thích chi tiết về mạng Long Short-Term Memory (LSTM)
description: LSTM được thiết kế để giải quyết các bài toán về phụ thuộc xa (long-term dependencies) trong RNN do bị ảnh hưởng bởi vấn đề gradient biến mất.
excerpt: LSTM là một phiên bản mở rộng của mạng RNN, được đề xuất vào năm 1997 bởi Sepp Hochreiter và Jürgen Schmidhuber. LSTM được thiết kế để giải quyết các bài toán về phụ thuộc xa (long-term dependencies) trong mạng RNN do bị ảnh hưởng bởi vấn đề gradient biến mất. Có thể hiểu một cách đơn giản là mạng RNN cơ bản trong thực tế không có khả năng ghi nhớ thông tin từ các bước có khoảng cách xa và do đó những phần tử đầu tiên trong chuỗi đầu vào không có nhiều ảnh hưởng đến các kết quả tính toán dự đoán phần tử cho chuỗi đầu ra trong các bước sau.
keywords: Long Short Term Memory, mạng LSTM, mạng RNN, học sâu, deep learning
author: Nguyễn Trường Long
---

### Các vấn đề về gradient trong quá trình huấn luyện

Gradient biến mất (Vanishing Gradient Problem) và gradient bùng nổ (Exploding Gradient Problem) là những vấn đề gặp phải khi sử dụng các kỹ thuật tối ưu hóa trọng số dựa trên gradient để huấn luyện mạng nơ-ron. Các vấn đề này thường gặp phải do việc lựa chọn các hàm kích hoạt không hợp lý hoặc số lượng các lớp ẩn của mạng quá lớn. Đặc biệt, các vấn đề này thường hay xuất hiện trong quá trình huấn luyện các mạng nơ-ron hồi quy. Trong thuật toán BPTT, khi chúng ta càng quay lùi về các bước thời gian trước đó thì các giá trị gradient càng giảm dần, điều này làm giảm tốc độ hội tụ của các trọng số do sự thay đổi hầu như rất nhỏ. Trong một số trường hợp khác, các gradient có giá trị rất lớn khiến cho quá trình cập nhật các trọng số bị phân kỳ và vấn đề này được gọi là gradient bùng nổ. Các vấn đề về gradient biến mất thường được quan tâm hơn vấn đề gradient bùng nổ do vấn đề gradient biến mất khó có thể được nhận biết trong khi gradient bùng nổ có thể dễ dàng quan sát và nhận biết hơn. Có nhiều nghiên cứu đề xuất các giải pháp để giải quyết những vấn đề này như lựa chọn hàm kích hoạt hợp lý, thiết lập các kích thước cho mạng hợp lý hoặc khởi tạo các trọng số ban đầu phù hợp khi huấn luyện. Một trong các giải pháp cụ thể có thể chỉ ra là thuật toán Truncated BPTT, một biến thể cải tiến của BPTT được áp dụng trong quá trình huấn luyện mạng nơ-ron hồi quy trên các chuỗi dài. Ngoài ra, mạng Long Short-Term Memory được giới thiệu trong những phần tiếp theo đã khắc phục được các vấn đề này.

### Cơ chế hoạt động của mạng LSTM

LSTM là một phiên bản mở rộng của mạng RNN, được đề xuất vào năm 1997 bởi Sepp Hochreiter và Jürgen Schmidhuber. LSTM được thiết kế để giải quyết các bài toán về phụ thuộc xa (long-term dependencies) trong mạng RNN do bị ảnh hưởng bởi vấn đề gradient biến mất. Có thể hiểu một cách đơn giản là mạng RNN cơ bản trong thực tế không có khả năng ghi nhớ thông tin từ các bước có khoảng cách xa và do đó những phần tử đầu tiên trong chuỗi đầu vào không có nhiều ảnh hưởng đến các kết quả tính toán dự đoán phần tử cho chuỗi đầu ra trong các bước sau.

Mạng LSTM bao gồm nhiều tế bào LSTM liên kết với nhau với kiến trúc cụ thể của mỗi tế bào được biểu diễn trong hình.

Ý tưởng của LSTM là bổ sung thêm trạng thái bên trong tế bào (cell internal state) {% raw %}$$s_i^{\left( t \right)}$${% endraw %} và ba cổng sàng lọc các thông tin đầu vào và đầu ra cho tế bào bao gồm forget gate, input gate và output gate:

- Forget gate: Có nhiệm vụ loại bỏ những thông tin không cần thiết nhận được và có phương trình như sau:

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

