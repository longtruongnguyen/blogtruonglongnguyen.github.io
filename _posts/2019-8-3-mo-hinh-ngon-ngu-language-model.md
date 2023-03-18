---
layout: post
title: Mô hình ngôn ngữ (language model)
description: Mô hình ngôn ngữ là mô hình mà sẽ tính toán phân phối xác suất của một chuỗi các token trong các ngôn ngữ tự nhiên của con người.
excerpt: Mô hình ngôn ngữ là mô hình mà tính toán phân phối xác suất của một chuỗi các token trong ngôn ngữ tự nhiên và có nghĩa là mô hình cho phép dự đoán khả năng xuất hiện của chuỗi token này trong ngôn ngữ của nó. Tùy thuộc vào cách thức mô hình được thiết kế, các token này có thể là các từ, các ký tự hoặc thậm chí là các byte.
keywords: mô hình ngôn ngữ, language model, xử lý ngôn ngữ tự nhiên, mô hình ngôn ngữ n-grams, xấp xỉ Markov, học máy
author: Nguyễn Trường Long
---

[Mô hình ngôn ngữ](https://nguyentruonglong.net/mo-hinh-ngon-ngu-language-model.html) là mô hình mà tính toán phân phối xác suất của một chuỗi các token trong ngôn ngữ tự nhiên {% raw %}
$$P\left( {{w_1},{w_2},{w_3},...,{w_\tau }} \right)$${% endraw %}. [Mô hình ngôn ngữ](https://nguyentruonglong.net/mo-hinh-ngon-ngu-language-model.html) thường được xây dựng trên cơ sở dữ liệu văn bản lớn để học cấu trúc và quy luật của ngôn ngữ và sau đó sử dụng cấu trúc đó để đưa ra dự đoán cho các token trong một câu mới. Điều này có nghĩa là mô hình cho phép dự đoán khả năng xuất hiện của chuỗi token này trong ngôn ngữ của nó. Tùy thuộc vào cách thức mô hình được thiết kế, các token này có thể là các từ, các ký tự hoặc thậm chí là các byte.

Để tính xác suất của một chuỗi các token liên tiếp, chúng ta áp dụng quy tắc xác suất dây chuyền (chain rule of probability) tổng quát để phân tách như sau:

{% raw %}
$$\begin{align}
	P\left( {{w_1},{w_2},{w_3},...,{w_\tau }} \right) = P\left( {{w_1}} \right)P\left( {{w_2}|{w_1}} \right)P\left( {{w_3}|{w_1},{w_2}} \right)...P\left( {{w_\tau }|{w_1},...,{w_{\tau  - 1}}} \right)
\end{align}$$
{% endraw %}

Quy tắc dây chuyền này cho chúng ta thấy được mối liên hệ giữa xác suất của một chuỗi các token và xác suất của một token đối với các token đứng trước nó. Ví dụ, để tính xác suất của câu "I am happy today", ta có thể sử dụng quy tắc xác suất dây chuyền và tính như sau:

{% raw %}
$$\begin{align}
\textrm( P("I am happy today") = P("I") * P("am" | "I") * P("happy" | "I am") * P("today" | "I am happy"))
\end{align}$$
{% endraw %}

Nhưng trong thực tế, quy tắc dây chuyền này tỏ ra không hữu ích vì chúng ta không thể nào có thể tính hết được tất cả các xác suất của một token được cho trước bởi các chuỗi token dài liên tiếp. Do đó xác suất này có thể được xây dựng từ một mô hình ngôn ngữ sử dụng một số kỹ thuật phổ biến sau:

 - [N-gram Language Models](https://web.stanford.edu/~jurafsky/slp3/3.pdf): Đây là phương pháp đơn giản nhất để xây dựng một mô hình ngôn ngữ. Mô hình này đưa ra dự đoán xác suất của một token dựa trên các token đã xuất hiện trước đó trong câu, được gọi là n-gram. N-gram là một chuỗi gồm n token liên tiếp trong câu.
- [Neural Language Models](https://towardsdatascience.com/neural-language-models-32bec14d01dc): Đây là phương pháp phổ biến và hiệu quả nhất để xây dựng mô hình ngôn ngữ. [Neural Language Models](https://towardsdatascience.com/neural-language-models-32bec14d01dc) sử dụng các mạng neural để học cấu trúc của ngôn ngữ và đưa ra dự đoán cho từ tiếp theo trong câu dựa trên các token đã xuất hiện trước đó trong câu. Một số kiến trúc mạng neural phổ biến được sử dụng để xây dựng mô hình ngôn ngữ là Recurrent Neural Networks (RNNs) và Transformers.
- [Statistical Language Models](http://mlwiki.org/index.php/Statistical_Language_Models): Phương pháp này sử dụng các phương pháp thống kê để xây dựng mô hình ngôn ngữ. Các phương pháp này sử dụng các thuật toán như Maximum Likelihood Estimation (MLE) và Expectation-Maximization (EM) để tối đa hóa xác suất của các token trong ngôn ngữ.
- [Rule-based Language Models]([https://www.igi-global.com/dictionary/rule-based-languages/25655](https://meta-guide.com/natural-language/nlp/statistical-nlp/rule-based-language-modeling): Phương pháp này sử dụng các luật ngữ pháp và cú pháp để xây dựng mô hình ngôn ngữ. Các luật này được thiết lập bởi các chuyên gia ngôn ngữ và được sử dụng để phân tích câu để đưa ra dự đoán cho các token trong câu tiếp theo.

### Mô hình N-grams

Một ý tưởng từ mô hình n-grams là thay vì sử dụng cách phân tích bằng quy tắc dây chuyền như trên. N-gram là một phương pháp xác định xác suất của một từ dựa trên các từ trước đó trong câu hoặc trong văn bản. N-gram đặc trưng cho việc xác định mối liên hệ giữa các từ trong một văn bản.

N-grams là một phương pháp dự đoán xác suất của một từ dựa trên n từ trước đó. N-grams được tính bằng cách tách văn bản thành các chuỗi liên tiếp của n từ, sau đó tính xác suất của từ tiếp theo dựa trên các chuỗi n-grams trước đó. Một n-gram trước tiên được phân tách thành các chuỗi gồm n từ liên tiếp trong một văn bản. Ví dụ, trong trường hợp của bigrams (n=2), xác suất của một từ sẽ dựa trên từ trước đó trong câu. Ví dụ, trong văn bản "The quick brown fox jumps over the lazy dog", có thể tạo ra các n-gram với n = 2 bằng cách tách các từ ra thành các cặp liên tiếp, cho kết quả như sau:

- "The quick"
- "quick brown"
- "brown fox"
- "fox jumps"
- "jumps over"
- "over the"
- "the lazy"
- "lazy dog"

Các n-gram có thể được sử dụng để xác định xác suất xuất hiện của một từ tiếp theo trong văn bản dựa trên n-gram trước đó. N-gram là một trong những phương pháp được sử dụng rộng rãi để xây dựng mô hình ngôn ngữ trong xử lý ngôn ngữ tự nhiên và các ứng dụng liên quan đến ngôn ngữ như nhận dạng giọng nói, dịch thuật, tóm tắt văn bản, và tổng hợp tiếng nói.

### Xấp xỉ Markov

Xấp xỉ Markov (approximate Markov) là một kỹ thuật trong [mô hình ngôn ngữ](https://nguyentruonglong.net/mo-hinh-ngon-ngu-language-model.html) để dự đoán từ tiếp theo trong một chuỗi từ với giả định rằng từ hiện tại chỉ phụ thuộc vào một số lượng nhỏ các từ trước đó. Xấp xỉ Markov thường được sử dụng để xác định xác suất của một từ tiếp theo trong một chuỗi văn bản, dựa trên từ đứng trước nó.

Cụ thể, xấp xỉ Markov ứng dụng giả định Markov rằng xác suất của một từ xuất hiện trong một chuỗi chỉ phụ thuộc vào một số lượng nhỏ các từ trước đó. Xấp xỉ Markov sử dụng thuật toán xác định xác suất của một từ tiếp theo dựa trên các từ đã xuất hiện trước đó. Thuật toán này sử dụng một bộ từ điển để lưu trữ thông tin liên quan đến các từ đã xuất hiện trong chuỗi văn bản.

Ví dụ, giả sử chúng ta có chuỗi văn bản "tôi yêu học tập". Khi sử dụng xấp xỉ Markov với giả định rằng xác suất của từ tiếp theo phụ thuộc vào 2 từ trước đó, ta có thể tính toán xác suất của từ "học" trong câu trên bằng cách sử dụng xác suất của cặp từ "yêu học". Nếu trong bộ từ điển có nhiều câu chứa cặp từ "yêu học", và hầu hết trong số đó đều có từ "học" đứng sau, thì xấp xỉ Markov sẽ ước tính xác suất của từ "học" là khá cao.

Chúng ta có thể tính bằng xấp xỉ Markov bậc $n$:
{% raw %}
$$\begin{align}
	P\left( {{w_t }|{w_1},...,{w_{t  - 1}}} \right) \approx P\left( {{w_t }|{w_{t  - n}},{w_{t  - \left( {n - 1} \right)}},...,{w_{t  - 2}},{w_{t  - 1}}} \right)
\end{align}$$
{% endraw %}

Điều này có nghĩa là xác suất xuất hiện tiếp theo của token {% raw %}$${{w_t }}$${% endraw %} với chuỗi token cho trước {% raw %}
$${{w_1},{w_2},...,{w_{t  - 1}}}$${% endraw %} chỉ phụ thuộc vào $n$ token đứng liền trước nó với $n$ vừa đủ nhỏ $\left( {n < t } \right)$ thay vì toàn bộ chuỗi token {% raw %}$${{w_1},{w_2},...,{w_{t  - 1}}}$${% endraw %}. Do đó phân phối xác suất của chuỗi {% raw %}$$\left( {{w_1},{w_2},...,{w_\tau }} \right)$${% endraw %} sẽ được tính bằng công thức:
{% raw %}
$$\begin{align}
	P\left( {{w_1},{w_2},...,{w_\tau }} \right) \approx \prod\limits_{t = 1}^\tau  {P\left( {{w_t}|{w_{t - \left( {n - 1} \right)}},...,{w_{t - 2}},{w_{t - 1}}} \right)}
\end{align}$$
{% endraw %}

Dựa vào công thức trên, chúng ta có thể xây dựng mô hình ngôn ngữ n-grams bằng cách thống kê các chuỗi có ít hơn $n+1$ token liên tiếp trong kho ngữ liệu văn bản lớn theo công thức ước lượng hợp lý cực đại (maximum likelihood estimation):

{% raw %}
$$\begin{align}
	P\left( {{w_t}|{w_{t - \left( {n - 1} \right)}},...,{w_{t - 2}},{w_{t - 1}}} \right) = \frac{{C\left( {{w_{t - \left( {n - 1} \right)}},...,{w_{t - 2}},{w_{t - 1}},{w_t}} \right)}}{{C\left( {{w_{t - \left( {n - 1} \right)}},...,{w_{t - 2}},{w_{t - 1}}} \right)}}
\end{align}$$
{% endraw %}

Xấp xỉ Markov là một trong những phương pháp phổ biến nhất được sử dụng trong mô hình ngôn ngữ, nhất là khi xử lý văn bản tự nhiên. Tuy nhiên, nó còn có một số hạn chế, ví dụ như nó không xử lý được các từ mang tính phân loại hoặc không xử lý được các từ đa nghĩa.

#### Ứng dụng

[Mô hình ngôn ngữ](https://nguyentruonglong.net/mo-hinh-ngon-ngu-language-model.html) được sử dụng rộng rãi trong xử lý ngôn ngữ tự nhiên để thực hiện các tác vụ như dịch máy, tự động tóm tắt, phân tích cảm xúc, phân loại văn bản, gợi ý từ,...
